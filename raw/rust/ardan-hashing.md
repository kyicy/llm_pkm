# Hashing Passwords

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

You probably don't want to be saving passwords in plain text. Let's add `sha2` as a dependency:

```toml
[dependencies]
serde = { version = "1.0.152", features = [ "derive" ] }
serde_json = "1.0.92"
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

`{:X}` in `format!` means "print in hexadecimal format".

> Add salt! Normally, you wouldn't just use a direct hash — you'd manipulate `password` in some way.

## Hashing New User Passwords

Update the `User` constructor to automatically hash passwords:

```rust
impl User {
    pub fn new(username: &str, password: &str, action: LoginAction) -> Self {
        Self {
            username: username.to_string(),
            password: hash_password(password),
            action
        }
    }
}
```

Update the `login` function to hash incoming passwords before comparison:

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
