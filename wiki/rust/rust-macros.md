# Rust Macros

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-macros.md](../../raw/rust/ardan-macros.md)

## Overview

Macros are Rust's way of letting you change the syntax of the language. There are two types: **declarative macros** (`macro_rules!`) and **procedural macros**. Declarative macros are pattern-based — they match input syntax and produce output code. Unlike C, Rust macros are *hygienic*: using a macro is always marked with `!`, and macros don't leak outside their scope.

## Basic Macro Syntax

Start with `macro_rules!`:

```rust
macro_rules! push {
    ($target: expr, $val: expr) => {
        $target.push($val);
    };
}
```

Key elements:
- **`$`**: Decorates macro variables (e.g., `$target`, `$val`)
- **`expr`**: The most common fragment specifier — matches any expression
- Other fragment types: `ident` (identifiers), `ty` (types), `pat` (patterns), `stmt` (statements), etc.

## Multiple Parameters and Repeating Patterns

For variable-length arguments, use the repeating construct `$()`:

```rust
macro_rules! push {
    ($target: expr, $($val: expr),+) => {
        $(
            $target.push($val);
        )+
    };
}
```

- `$()` wraps the pattern that repeats
- `+` means "one or more" (use `*` for "zero or more")
- The comma before `+` indicates the separator between elements

Usage:

```rust
fn main() {
    let mut vec = Vec::new();
    push!(vec, 1, 2, 3, 4);
    println!("{:?}", vec);  // [1, 2, 3, 4]
}
```

Expanding the macro (via Rust Analyzer's "Expand Macro") shows:

```rust
vec.push(1);
vec.push(2);
vec.push(3);
vec.push(4);
```

## Exporting Macros

To make a macro available to other crates, annotate with `#[macro_export]`:

```rust
#[macro_export]
macro_rules! push {
    ($target: expr, $($val: expr),+) => {
        $(
            $target.push($val);
        )+
    };
}
```

The macro will *always* end up at the root of your crate, regardless of where it's defined.

> Macros can take longer to compile than regular functions.

## Macro Recursion

Macros can call other macros:

```rust
macro_rules! really_push {
    ($target: expr, $val: expr) => {
        $target.push($val);
    };
}

#[macro_export]
macro_rules! push {
    ($target: expr, $($val: expr),+) => {
        $(
            really_push!($target, $val);
        )+
    };
}
```

Macros are expanded as a pre-processing step before compilation, so recursion works naturally — as long as you avoid infinite recursion.

## Macro Hygiene

Rust macros are *hygienic*: they cannot introduce or leak names into the calling scope. This prevents the class of bugs common in C where a macro can redefine variables or create unexpected side effects. The `!` syntax also makes macro calls visually distinct from regular function calls.

## See Also

- [Rust Custom Types](rust-custom-types.md) — defining types with structs and enums that macros can manipulate
- [Rust Testing](rust-testing.md) — `#[test]` attribute is itself a macro
