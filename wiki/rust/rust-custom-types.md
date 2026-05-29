# Rust Custom Types

> Sources: Rust by Example, Unknown
> Raw: [custom-types.md](../../raw/rust/2026-05-29-custom-types.md)

## Overview

Rust provides two primary keywords for defining custom data types — `struct` for structures and `enum` for enumerations — plus `const` and `static` for named constants. These form the foundation for modeling domain data beyond the built-in primitives.

## The Three Mechanisms

| Keyword | Purpose |
|---------|---------|
| `struct` | Define a structure — a named collection of fields |
| `enum` | Define an enumeration — a type that is one of several variants |
| `const` / `static` | Define named constants, including at global scope |

## See Also

- [Rust Structs](rust-structs.md) — C-like, tuple, and unit structs
- [Rust Enums](rust-enums.md) — variants, matching, type aliases, C-like enums, `use`
- [Rust Constants](rust-constants.md) — `const` vs `static`, global scope, `unsafe`
- [Rust Primitives](rust-primitives.md) — the built-in types these mechanisms build upon
- [Rust Library Crates](rust-library-crates.md) — sharing custom types across crates
- [Rust Serde Serialization](rust-serde-serialization.md) — making custom types serializable
- [Rust Traits](rust-traits.md) — custom traits, default implementations, trait bounds, `dyn` dispatch
- [Rust Traits and OOP](rust-traits-and-oop.md) — designing data structures for Rust's ownership model
- [Rust NewType Pattern](rust-new-type-pattern.md) — tuple struct wrappers for type safety
- [Rust Generic Data Structures](rust-generic-data-structures.md) — generic types with `impl<T>` and `where` bounds
- [Rust Macros](rust-macros.md) — declarative macros for code generation and syntax extension
