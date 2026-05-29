# Hash maps (Dictionaries)

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Vectors are great, but they order data exactly as it was inserted. Using `find` requires that Rust read each record in turn. `HashMap` is like a `Dictionary` type in other languages.

First, `HashMap` isn't included in the default namespace:

```rust
use std::collections::HashMap;
```

Let's decorate the `User` structure with `Clone` and `Debug`:

```rust
#[derive(Clone, Debug)]
pub struct User {
    pub username: String,
    pub password: String,
    pub action: LoginAction,
}
```

Replace `get_users()` with one that creates a `HashMap`:

```rust
pub fn get_users() -> HashMap<String, User> {
    let mut result = HashMap::new();
    result.insert("herbert".to_string(), User::new("herbert", "password", LoginAction::Accept(Role::Admin)));
    result
}
```

There's no convenient "insert" macro for `HashMap`. We can transform a vector of users into a `HashMap` with the iterator/collect approach:

```rust
let users = vec![
    User::new("herbert", "password", LoginAction::Accept(Role::Admin)),
    User::new("bob", "password", LoginAction::Accept(Role::User)),
    User::new("fred", "password", LoginAction::Denied(DeniedReason::PasswordExpired)),
];

users
    .iter()
    .map(|user| (user.username.clone(), user.clone()))
    .collect()
```

To save memory, you can use `drain`:

```rust
users
    .drain(0..)
    .map(|user| ( user.username.clone(), user ))
    .collect()
```

`drain` removes each entry from the vector and passes the removed records to an iterator.

## Accessing HashMap Data

Refactored login function using `HashMap`:

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

### Vector vs HashMap Performance

Insert performance (1,000,000 elements):
```
Inserting 1000000 elements into a vector  took  146894 usecs
Inserting 1000000 elements into a HashMap took 1942095 usecs
```

Search performance (finding second-to-last element):
```
Vector search took 29205 usecs
HashMap search took 4 usecs
```

> Use the right tool for the right job. If you are searching your data heavily, a `HashMap` is a great choice. If you are manipulating data, `Vec` is usually the right choice.
