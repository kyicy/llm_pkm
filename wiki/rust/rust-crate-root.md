# Rust Crate Root

> Sources: Ardan Ultimate Rust Foundations, 2025

## Overview

A **crate** is Rust's fundamental compilation unit. Every crate has a **root file** that serves as its entry point: `lib.rs` for library crates and `main.rs` for binary crates. The crate root defines the module tree — all code in the crate is organized relative to this root file.

## Crate Root vs Package

A **package** (defined by `Cargo.toml`) can contain one or more crates. The crate root is always a source file, never a configuration file:

```
my_project/
├── Cargo.toml          ← Package definition (metadata, dependencies)
└── src/
    ├── lib.rs          ← Crate root for the library crate
    └── main.rs         ← Crate root for the binary crate (separate crate)
```

When a package has both `lib.rs` and `main.rs`, they are **two independent crates** sharing the same `Cargo.toml`. They can see each other only through explicit `[dependencies]` in `Cargo.toml`.

## The `crate` Keyword

In Rust's path system, `crate` is a keyword that refers to the **current crate's root**. It is used in two ways:

### Path prefix

`crate::` denotes an absolute path starting from the crate root:

```rust
// lib.rs (crate root)
mod authentication;

// Inside authentication/mod.rs:
use crate::config::AppConfig;  // starts from lib.rs root
// NOT: use my_package::config::AppConfig;  ← wrong, crate name not used
```

### Visibility modifier

`pub(crate)` makes an item visible to all code within the current crate, but hidden from external consumers:

```rust
pub fn login() { }          // Public: external crates can use it
pub(crate) fn setup() { }   // Crate-internal: only code in this crate can use it
fn helper() { }             // Private: only the current module can use it
```

The `crate` in `pub(crate)` is the same keyword used in paths — it always refers to the current crate root, not the package name.

## Related Path Keywords

| Keyword | Meaning |
|---------|---------|
| `crate::` | Absolute path from crate root |
| `super::` | Relative path to parent module |
| `self::` | Relative path to current module |

## Key Takeaways

- A **crate** is defined by its root file (`lib.rs` or `main.rs`), not by `Cargo.toml`
- `crate` in `pub(crate)` and `crate::` is a **Rust keyword**, not a package name
- A single package can contain multiple crates (lib + bin)
- The crate root is always a `.rs` source file

## See Also

- [Rust Modules and Visibility](rust-modules-and-visibility.md) — organizing code within a crate
- [Rust Library Crates](rust-library-crates.md) — library crate structure and `lib.rs`
- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — Cargo.toml and package structure
