# Rust Hello World

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [hello-world.md](../../raw/rust/hello-world.md); [ardan-hello-world.md](../../raw/rust/ardan-hello-world.md)

## Overview

The traditional Hello World program in Rust demonstrates the basic structure of a Rust program: a `main()` function that serves as the entry point, and the `println!` macro for console output. Rust programs are compiled using `cargo`, the build system and package manager, or directly with `rustc`, the Rust compiler.

## Program Structure

Every Rust executable requires a `main()` function where execution begins:

```rust
fn main() {
    println!("Hello World!");
}
```

The `println!` macro prints text to the console, appending a newline. It is part of the `std::fmt` module and supports formatted text output with compile-time format string checking.

## Macros

The `!` in `println!` denotes a macro. Macros use Rust's built-in macro system to support syntax that doesn't fit inside regular Rust syntax. You can expand macros in Rust Analyzer via the Command Palette ("Expand Macro Recursively"):

```rust
// Expanded println!("Hello, world!")
{
    $crate::io::_print($crate::fmt::Arguments::new_v1(&[], &[]));
}
```

## Project Creation with Cargo

Use `cargo new` to create a new Rust project:

```bash
$ cargo new login_system
     Created binary (application) `login_system` package
```

This creates:
- `Cargo.toml` — package manifest with name, version, edition, and dependencies
- `src/main.rs` — source file with a `main()` function
- `.gitignore` — excludes the `target/` directory
- A `.git` repository (unless `--vcs` is specified)

The `cargo init` command does the same thing as `cargo new`.

### Cargo.toml Structure

```toml
[package]               # Every Cargo project needs a package section
name = "login_system"   # The project name, doubles as the target filename
version = "0.1.0"       # Semantic versioning
edition = "2021"        # Which edition of Rust

[dependencies]
# Defaults to an empty list
```

### Git Integration and `--vcs`

By default, `cargo new` creates a Git repository. You can disable this with `--vcs none`:

```bash
$ cargo new --vcs none login_system
```

Other supported VCS backends: `git` (default), `hg` (Mercurial), `pijul`, `fossil`. If you are already inside a Git workspace, creating a new project won't create another repository.

## Compilation and Execution

Compile with `cargo build` or compile and run with `cargo run`:

```bash
$ cargo run
   Compiling hello_login_system v0.1.0
    Finished dev [unoptimized + debuginfo] target(s) in 1.57s
     Running `target/debug/hello_login_system.exe`
Hello, world!
```

### Debug vs Release Mode

Running without flags uses *debug* mode: optimizations are disabled, extra debug information is generated, and extra run-time error checks are active.

To run in optimized mode:

```bash
$ cargo run --release
```

The `--release` flag produces a slower compilation but faster execution.

## Direct Compilation with rustc

Rust source files (`.rs` extension) can also be compiled directly with `rustc`:

```bash
$ rustc hello.rs
$ ./hello
Hello World!
```

## See Also

- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — detailed Cargo.new flags, editions, profiles
- [Rust Comments](rust-comments.md)
- [Rust Printing and Formatting](rust-printing-and-formatting.md)
- [Rust Primitives](rust-primitives.md) — type system used in program structure
