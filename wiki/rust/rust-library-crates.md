# Rust Library Crates

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [hello-world.md](../../raw/rust/hello-world.md); [ardan-hello-library.md](../../raw/rust/ardan-hello-library.md); [ardan-modules.md](../../raw/rust/ardan-modules.md)

## Overview

A library crate is a package designed to be shared and used by other programs, rather than executed directly. Library crates use `lib.rs` instead of `main.rs` and require public visibility annotations on items that should be accessible to external consumers.

## Creating a Library Crate

Use `cargo new` with the `--lib` flag:

```bash
$ cargo new --lib authentication
     Created library `authentication` package
```

This creates a `lib.rs` file instead of `main.rs`, signaling that the package is a library.

## Default Library Template

Cargo generates a default library crate with an example function and test:

```rust
pub fn add(left: usize, right: usize) -> usize {
    left + right
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        let result = add(2, 2);
        assert_eq!(result, 4);
    }
}
```

## Function Syntax

```rust
// `pub` makes the function public — accessible from outside the library
pub fn add(left: usize, right: usize) -> usize {
    left + right  // No "return" needed; last expression is returned
}
```

Key points:
- **`pub`**: Visibility modifier. Without it, functions are private by default.
- **Implicit return**: The last expression in a function is its return value.
- **Explicit `return`**: Also valid but Clippy prefers the short form. Early returns are acceptable.

## Adding a Library as a Dependency

To use a library from another crate, add it as a path dependency in `Cargo.toml`:

```toml
[dependencies]
authentication = { path = "../authentication" }
```

Other dependency specifications:
- **Version**: `library = "1"` (SemVer — latest in 1.x.y)
- **Git**: `library = { git = "https://github.com/user/repo.git" }`

## Importing and Using a Library

```rust
use authentication::greet_user;

fn main() {
    println!("{}", greet_user("Herbert"));
}
```

### Library + Binary in One Crate

A project with both `main.rs` and `lib.rs` can be executed and used as a library. This is useful for attaching unit tests and benchmarks to an executable.

## Modules and Visibility

Libraries can organize code into modules. Modules are private by default:

```rust
mod user {
    pub struct User { ... }
}

pub use user::User;  // re-export for external consumers
```

Key visibility modifiers:
- `pub` — accessible anywhere
- `pub(crate)` — accessible within the crate only
- default — private to the module

See [Rust Modules and Visibility](rust-modules-and-visibility.md) for detailed coverage.

## Terminology

- **Library**: Shared code, generic term
- **Crate**: A Cargo-managed bundle of code (may be a library or binary)
- **Module**: A section inside a crate (declared with `mod`)

## See Also

- [Rust Crate Root](rust-crate-root.md) — crate root, `pub(crate)`, and the `crate` keyword
- [Rust Modules and Visibility](rust-modules-and-visibility.md) — organizing library code with modules
- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — Cargo.toml structure and project types
- [Rust Cargo Workspaces](rust-cargo-workspaces.md) — organizing libraries and executables together
- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — feature flags for conditional compilation
- [Rust Testing](rust-testing.md) — unit testing in library crates
