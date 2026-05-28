# Rust Comments

> Sources: Rust by Example, Unknown
> Raw: [comments.md](../../raw/rust/comments.md)

## Overview

Rust supports two categories of comments: regular comments (ignored by the compiler) and documentation comments (parsed into HTML library documentation). Regular comments include line comments (`//`) and block comments (`/* ... */`), while documentation comments use `///` for item-level docs and `//!` for enclosing-item (module/crate-level) docs.

## Regular Comments

**Line comments** start with `//` and continue to the end of the line:

```rust
// This is a line comment
```

**Block comments** are enclosed between `/*` and `*/` and can span multiple lines:

```rust
/* This is a block comment
   spanning multiple lines */
```

Block comments can be nested (e.g., `/* outer /* inner */ outer */`), and can be used within expressions:

```rust
let x = 5 + /* 90 + */ 5; // evaluates to 10
```

## Documentation Comments

**`///`** — Generates documentation for the item that follows it (function, struct, etc.).

**`//!`** — Generates documentation for the enclosing item, typically used at the top of a file or module for crate/module-level docs.

These are parsed by `rustdoc` into HTML library documentation, supporting Markdown formatting.

## See Also

- [Rust Hello World](rust-hello-world.md)
