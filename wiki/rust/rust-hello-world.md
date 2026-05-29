# Rust Hello World

> Sources: Rust by Example, Unknown
> Raw: [hello-world.md](../../raw/rust/hello-world.md)

## Overview

The traditional Hello World program in Rust demonstrates the basic structure of a Rust program: a `main()` function that serves as the entry point, and the `println!` macro for console output. Rust programs are compiled using `rustc`, the Rust compiler.

## Program Structure

Every Rust executable requires a `main()` function where execution begins:

```rust
fn main() {
    println!("Hello World!");
}
```

The `println!` macro prints text to the console, appending a newline. It is part of the `std::fmt` module and supports formatted text output with compile-time format string checking.

## Compilation

Rust source files (`.rs` extension) are compiled with `rustc`:

```bash
$ rustc hello.rs
```

This produces a binary that can be executed directly:

```bash
$ ./hello
Hello World!
```

## See Also

- [Rust Comments](rust-comments.md)
- [Rust Printing and Formatting](rust-printing-and-formatting.md)
- [Rust Primitives](rust-primitives.md) — type system used in program structure
