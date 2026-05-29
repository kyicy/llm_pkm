# Rust Cargo Workspaces

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-workspaces.md](../../raw/rust/ardan-workspaces.md)

## Overview

Cargo workspaces allow you to manage multiple related packages under a single project root. All member packages share a single `target/` directory and a unified `Cargo.lock` file, reducing build times and disk usage.

## Workspace Configuration

A workspace is defined in the root-level `Cargo.toml` by adding a `[workspace]` section:

```toml
[workspace]
members = [
    "login",
    "authentication",
]
```

The workspace automatically includes the top-level `src/` directory as a member (the "parent" workspace).

## Creating Workspace Members

Create new projects inside the workspace directory:

```bash
$ cargo new login
$ cargo new --lib authentication
```

Each new project will emit a warning about invalid workspace configuration until you add it to the `members` list in the root `Cargo.toml`:

```toml
members = [
    "login",
    "authentication",
]
```

> **Tip**: It's helpful to include inline comments about what each member does.

## Benefits

### Shared Build Artifacts

All workspace members compile into a single `target/` directory. This means:
- One `target/` folder to clean up (not one per project)
- Shared dependency downloads and compilation
- Faster builds overall

### Batch Commands

Run commands across all workspace members:

```bash
$ cargo test --all       # Run all tests in all members
$ cargo build --all      # Build all members
$ cargo check --all      # Check all members for errors
```

> **Caution**: `cargo run --all` will try to run every executable in the workspace, which may not be what you want.

### Handling the Parent Crate

When a workspace has a parent project with `src/main.rs`, running `cargo run` at the workspace root runs the parent project. It's good practice to change the parent's main function to indicate this:

```rust
fn main() {
    println!("You probably wanted to run one of the nested workspaces.");
}
```

## See Also

- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — project creation and Cargo.toml
- [Rust Library Crates](rust-library-crates.md) — creating shared libraries within workspaces
