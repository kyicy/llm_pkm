# Rust Serde Serialization

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-serialization.md](../../raw/rust/ardan-serialization.md)

## Overview

Serde is Rust's framework for serialization and deserialization. It is format-agnostic — you pair it with a format crate (e.g., `serde_json`) to handle specific data formats. Serde is one of the most widely used crates in the Rust ecosystem.

## Setup

Add Serde and a format crate as dependencies:

```bash
$ cargo add serde
$ cargo add serde_json
```

Enable the `derive` feature for automatic implementation:

```toml
[dependencies]
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
```

## Deriving Serialize and Deserialize

Import the traits and annotate types:

```rust
use serde::{Serialize, Deserialize};

#[derive(Clone, Debug, Serialize, Deserialize)]
pub struct User {
    pub username: String,
    pub password: String,
    pub action: LoginAction,
}
```

Every contained type must also implement `Serialize` and `Deserialize`:

```rust
#[derive(Serialize, Deserialize)]
pub enum Role { Admin, User, Limited }

#[derive(Serialize, Deserialize)]
pub enum LoginAction {
    Accept(Role),
    Denied(DeniedReason),
}
```

## Serializing to JSON

```rust
use std::io::Write;

let users = get_users();

// Compact JSON
let json = serde_json::to_string(&users).unwrap();

// Pretty-printed JSON
let json = serde_json::to_string_pretty(&users).unwrap();

let mut f = std::fs::File::create("users.json").unwrap();
f.write_all(json.as_bytes()).unwrap();
```

Output (pretty-printed):

```json
{
  "bob": {
    "username": "bob",
    "password": "password",
    "action": { "Accept": "User" }
  }
}
```

## Deserializing from JSON

```rust
pub fn get_users() -> HashMap<String, User> {
    let json = std::fs::read_to_string("users.json").unwrap();
    serde_json::from_str(&json).unwrap()
}
```

This loads the file and deserializes directly into a `HashMap<String, User>`.

## File Lifecycle

Rust's `File` type uses RAII (Resource Acquisition Is Initialization). When a `File` drops out of scope, it is automatically closed:

```rust
{
    let mut f = std::fs::File::create("users.json").unwrap();
    f.write_all(json.as_bytes()).unwrap();
} // file is automatically closed here
```

## See Also

- [Rust Hashmaps](rust-hashmaps.md) — HashMap as a serializable data structure
- [Rust Password Hashing](rust-password-hashing.md) — hashing passwords before serialization
- [Rust CLI Applications](rust-cli-applications.md) — building CLI tools that read/write serialized data
