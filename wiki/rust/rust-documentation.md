# Rust Documentation

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-documentation.md](../../raw/rust/ardan-documentation.md)

## Overview

Rust has built-in documentation tooling. Documentation comments use Markdown and can include code examples that are automatically run as tests. Documentation is generated with `cargo doc` and published on docs.rs.

## Doc Comment Types

| Syntax | Scope | Example |
|--------|-------|---------|
| `///` | Documents the next item (function, struct, etc.) | `/// Does important work` |
| `//!` | Documents the containing item (crate, module) | `//! # My Crate` |

## Crate-Level Documentation

Use `//!` at the top of `lib.rs`:

```rust
//! # Authentication
//!
//! This library provides user validation and role assignment.
```

## Function Documentation

Use `///` with Markdown:

```rust
/// `hash_password` applies a SHA256 digest hash to a string.
///
/// ## Arguments
///
/// * `password` - the password to hash.
pub fn hash_password(password: &str) -> String {
    // ...
}
```

## Warning About Missing Documentation

Add this directive to emit warnings for undocumented public items:

```rust
#![warn(missing_docs)]
```

## Doc Tests

Code examples in doc comments run as tests with `cargo test`:

```rust
/// ```
/// use my_lib::hash_password;
/// let hash = hash_password("test");
/// assert_eq!(hash.len(), 64);  // SHA-256 produces 64 hex chars
/// ```
```

This ensures documentation stays synchronized with code.

## Generating Documentation

```bash
$ cargo doc     # generates HTML docs in target/doc/
$ cargo doc --open  # generates and opens in browser
```

## See Also

- [Rust Testing](rust-testing.md) — unit tests and integration tests
- [Rust Modules and Visibility](rust-modules-and-visibility.md) — structuring code for clear documentation
