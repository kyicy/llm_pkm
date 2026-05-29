# Rust Cargo and Project Setup

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-hello-world.md](../../raw/rust/ardan-hello-world.md); [setup-rust.md](../../raw/rust/setup-rust.md); [setup-ide.md](../../raw/rust/setup-ide.md)

## Overview

Cargo is Rust's build system and package manager. It handles compilation, dependency management, testing, documentation generation, and more. Most Rust projects are created and managed through Cargo, which provides consistent project structure and build configurations.

## Creating a New Project

Use `cargo new` to bootstrap a new Rust project:

```bash
$ cargo new my_project
     Created binary (application) `my_project` package
```

This creates:
- `Cargo.toml` — the project manifest
- `src/main.rs` — the source entry point
- `.gitignore` — excludes `target/` directory
- `.git/` — an initialized Git repository (if not already inside one)

`cargo init` does the same thing as `cargo new`, but can be run inside an existing directory.

### The `--vcs` Flag

By default, `cargo new` initializes a Git repository. Control this with `--vcs`:

```bash
$ cargo new --vcs none my_project   # No VCS initialization
$ cargo new --vcs hg                # Mercurial
$ cargo new --vcs pijul             # Pijul
$ cargo new --vcs fossil            # Fossil
```

If you are already inside a Git workspace, `cargo new` won't create another repository — it detects the existing VCS root.

## Cargo.toml Structure

Every Cargo project has a `Cargo.toml` manifest:

```toml
[package]
name = "my_project"
version = "0.1.0"
edition = "2021"

[dependencies]
```

Key fields:
- **name**: The project name, doubles as the output binary name
- **version**: Semantic versioning (SemVer)
- **edition**: Which Rust edition to use

### Rust Editions

Every few years, Rust issues a new *edition* — the only time at which substantial syntax changes are permitted. Rust retains compatibility with older editions by specifying the edition in `Cargo.toml`:

- **2015**: The original edition
- **2018**: Improved module system, NLL borrow checker
- **2021**: Current stable edition — disjoint captures, `IntoIterator` for arrays, `Cargo.toml` format updates
- **2024**: Upcoming edition (if applicable)

## Build Modes

Cargo has two primary build profiles:

### Debug (default)

```bash
$ cargo build      # or cargo run
```

- Optimizations disabled
- Debug symbols included
- Extra runtime checks active
- Fast compilation, slow execution

### Release

```bash
$ cargo build --release      # or cargo run --release
```

- Optimizations enabled
- Debug symbols stripped by default
- Slower compilation, fast execution

## Source Files

The `src/` directory contains all source code:

- **`main.rs`**: Binary entry point. Projects with `main.rs` require a `fn main()` and build executables.
- **`lib.rs`**: Library entry point. Projects with `lib.rs` are library crates — they can't be run directly but can be used from other programs.
- **Both**: A project with both `main.rs` and `lib.rs` can be both executed and used as a library.

## Feature Flags

Feature flags let library consumers change a crate's behavior at compile time — you've used this when specifying `features = ["derive"]` with Serde.

### Defining Features

In `Cargo.toml`:

```toml
[features]
default = [ "normal" ]
normal = []
other = []
```

- `default` specifies which features are enabled by default.
- Features are additive — they don't conflict unless you write conditional code to avoid it.

### Using Features in Code

Use `#[cfg(feature = "...")]` for conditional compilation:

```rust
#[cfg(feature = "normal")]
pub const MODE: &str = "NORMAL";

#[cfg(feature = "other")]
pub const MODE: &str = "OTHER";
```

### Selecting Features From a Consumer

```toml
# Uses default features
flags_lib = { path = "../flags_lib" }

# Disables defaults, enables specific features
flags_lib = { path = "../flags_lib", default-features = false, features = [ "other" ] }
```

### Conditional Combinations

Use `all()`, `not()`, and `any()` for complex conditions:

```rust
#[cfg(all(not(feature = "other"), feature = "normal"))]
pub const MODE: &str = "NORMAL";
```

This configuration variable is enabled only when `normal` is active AND `other` is not.

## See Also

- [Rust Hello World](rust-hello-world.md) — first program in detail
- [Rust Library Crates](rust-library-crates.md) — creating and using shared libraries
- [Rust Cargo Workspaces](rust-cargo-workspaces.md) — managing multi-project setups
- [Rust Constants](rust-constants.md) — `#[cfg]` conditional constants
