# Serialization/Deserialization

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

There's a wonderful Rust package called `serde` for handling serialization/deserialization. It is format-agnostic, and needs an additional dependency for whatever format you require. We'll use `serde_json`.

## Dependencies

```
cargo add serde
cargo add serde_json
```

You'll notice that `cargo add` mentioned some "features". We actually want the `derive` feature of Serde:

```toml
serde = { version = "1.0.152", features = [ "derive" ] }
serde_json = "1.0.92"
```

## Making Types Serializable & Deserializable

```rust
use serde::{Serialize, Deserialize};

#[derive(Clone, Debug, Serialize, Deserialize)]
pub struct User {
    pub username: String,
    pub password: String,
    pub action: LoginAction,
}
```

Every type contained within the structure *also* has to support `Serialize` and `Deserialize`:

```rust
#[derive(PartialEq, Debug, Clone, Serialize, Deserialize)]
pub enum Role {
    Admin, User, Limited
}

#[derive(PartialEq, Debug, Clone, Serialize, Deserialize)]
pub enum DeniedReason {
    PasswordExpired,
    AccountLocked{reason: String},
}

#[derive(PartialEq, Debug, Clone, Serialize, Deserialize)]
pub enum LoginAction {
    Accept(Role),
    Denied(DeniedReason),
}
```

## Making Some Initial Data

```rust
pub fn build_users_file() {
    use std::io::Write;

    let users = get_users();
    let json = serde_json::to_string(&users).unwrap();
    let mut f = std::fs::File::create("users.json").unwrap();
    f.write_all(json.as_bytes()).unwrap();
}
```

Note: `File` uses "RAII" — Resource Allocation Is Initialization. When `File` drops out of scope, the file is closed.

For pretty-printed JSON:

```rust
let json = serde_json::to_string_pretty(&users).unwrap();
```

## Deserializing Data

```rust
pub fn get_users() -> HashMap<String, User> {
    let json = std::fs::read_to_string("users.json").unwrap();
    serde_json::from_str(&json).unwrap()
}
```
