# Rust Hashmaps

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-hashmaps.md](../../raw/rust/ardan-hashmaps.md)

## Overview

`HashMap<K, V>` stores key-value pairs and provides O(1) average-case lookup. It is the Rust equivalent of dictionaries or associative arrays in other languages. `HashMap` is not in the prelude and must be imported explicitly.

## Import and Basic Usage

```rust
use std::collections::HashMap;
```

### Inserting

```rust
let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```

### Accessing

```rust
let team_name = String::from("Blue");
let score = scores.get(&team_name); // Option<&i32>
```

## Using HashMap for User Storage

A practical pattern: keying users by username for fast lookup.

```rust
#[derive(Clone, Debug)]
pub struct User {
    pub username: String,
    pub password: String,
    pub action: LoginAction,
}

pub fn get_users() -> HashMap<String, User> {
    let mut result = HashMap::new();
    result.insert("herbert".to_string(), User::new("herbert", ...));
    result
}
```

### Transforming Vectors to HashMaps

Use iterators and `collect` to transform a `Vec` into a `HashMap`:

```rust
let users = vec![
    User::new("herbert", "password", LoginAction::Accept(Role::Admin)),
    User::new("bob", "password", LoginAction::Accept(Role::User)),
    User::new("fred", "password", LoginAction::Denied(DeniedReason::PasswordExpired)),
];

let map: HashMap<String, User> = users
    .iter()
    .map(|user| (user.username.clone(), user.clone()))
    .collect();
```

For memory efficiency, use `drain` to avoid cloning each user:

```rust
users
    .drain(0..)
    .map(|user| (user.username.clone(), user))
    .collect()
```

`drain` removes entries from the vector and passes ownership to the iterator.

## Lookup Patterns

### Basic lookup with password check

```rust
pub fn login(users: &HashMap<String, User>, username: &str, password: &str) -> Option<LoginAction> {
    let username = username.trim().to_lowercase();
    let password = password.trim();

    users
        .get(&username)
        .filter(|user| user.password == password)
        .map(|user| user.action.clone())
}
```

### Checking for key existence

```rust
if users.contains_key(&username) {
    println!("{username} already exists, aborting.");
}
```

### Mutable access

```rust
if let Some(mut user) = users.get_mut(&username) {
    user.password = hash_password(&new_password);
}
```

## Performance: HashMap vs Vec

### Insert Performance (1,000,000 elements)

| Structure | Time |
|-----------|------|
| `Vec` | ~147,000 µs |
| `HashMap` | ~1,942,000 µs |

HashMap inserts require generating a hash key — an order of magnitude slower.

### Search Performance (finding second-to-last of 1,000,000)

| Structure | Time |
|-----------|------|
| `Vec` (`.iter().find()`) | ~29,205 µs |
| `HashMap` (`.get()`) | ~4 µs |

HashMap searches are thousands of times faster for large datasets.

> Use the right tool for the right job. `HashMap` for searching, `Vec` for manipulating data.

## See Also

- [Rust Vectors](rust-vectors.md) — sequential data storage
- [Rust Password Hashing](rust-password-hashing.md) — storing hashed passwords in HashMaps
- [Rust Serde Serialization](rust-serde-serialization.md) — serializing HashMaps to JSON
