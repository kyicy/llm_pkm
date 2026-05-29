# Rust Password Hashing

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-hashing.md](../../raw/rust/ardan-hashing.md)

## Overview

Storing passwords in plain text is a security risk. Rust provides the `sha2` crate (among others) for hashing passwords before storage. For production use, consider more robust solutions like `argon2` or `bcrypt` with proper salting.

## Adding the sha2 Crate

```toml
[dependencies]
sha2 = "0"
```

## Creating a Hash Function

```rust
pub fn hash_password(password: &str) -> String {
    use sha2::Digest;
    let mut hasher = sha2::Sha256::new();
    hasher.update(password);
    format!("{:X}", hasher.finalize())
}
```

- `{:X}` formats the hash in uppercase hexadecimal
- `sha2::Digest` is the trait that provides `update()` and `finalize()`

> **Note on salting**: In production, you should not use a direct hash. Add salt — manipulate the password in some way before hashing. There are entire books on password salting best practices.

## Hashing at Construction

Automatically hash passwords in the constructor:

```rust
impl User {
    pub fn new(username: &str, password: &str, action: LoginAction) -> Self {
        Self {
            username: username.to_string(),
            password: hash_password(password),
            action,
        }
    }
}
```

## Hashing for Comparison

Hash incoming passwords before comparing with stored hashes:

```rust
pub fn login(users: &HashMap<String, User>, username: &str, password: &str) -> Option<LoginAction> {
    let username = username.trim().to_lowercase();
    let password = hash_password(password.trim());

    users
        .get(&username)
        .filter(|user| user.password == password)
        .map(|user| user.action.clone())
}
```

## Serialized Output

With hashing enabled, the serialized JSON contains hash values instead of plain text:

```json
{
  "bob": {
    "username": "bob",
    "password": "5E884898DA28047151D0E56F8DC6292773603D0D6AABBDD62A11EF721D1542D8",
    "action": { "Accept": "User" }
  }
}
```

## See Also

- [Rust Serde Serialization](rust-serde-serialization.md) — serializing hashed passwords to JSON
- [Rust Hashmaps](rust-hashmaps.md) — storing user data with hashed passwords
- [Rust CLI Applications](rust-cli-applications.md) — user management CLI with password change
