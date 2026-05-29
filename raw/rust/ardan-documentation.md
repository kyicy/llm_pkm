# Documentation

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

## Library Header Documentation

Use `//!` for crate-level documentation at the top of `lib.rs`:

```rust
//! # Authentication
//!
//! This module provides user validation and role assignment.
```

## Warning About Missing Documentation

Add this directive to emit warnings for undocumented public items:

```rust
#![warn(missing_docs)]
```

The `#!` means "do this for the whole crate."

## Documenting Functions

Use `///` for documentation comments. They support Markdown:

```rust
/// `hash_password` applies a SHA256 digest hash to a string, and returns a
/// string containing the hashed string, in hexadecimal format.
///
/// ## Arguments
///
/// * `password` - the password to hash.
pub fn hash_password(password: &str) -> String {
    use sha2::Digest;
    let mut hasher = sha2::Sha256::new();
    hasher.update(password);
    format!("{:X}", hasher.finalize())
}
```

## Documentation Examples

You can include code examples that run as tests:

```rust
/// ```
/// use docs::hash_password;
/// println!("{}", hash_password("test"));
/// ```
```

Run `cargo test` — the example executes as a doc test. This ensures documentation stays synced with code.
