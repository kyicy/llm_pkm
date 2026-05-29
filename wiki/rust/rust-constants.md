# Rust Constants

> Sources: Rust by Example, Unknown
> Raw: [constants.md](../../raw/rust/2026-05-29-constants.md)

## Overview

Rust provides two keywords for declaring named constants in any scope, including globally: `const` for immutable values and `static` for variables with a `'static` lifetime. Both require explicit type annotations.

## `const` vs `static`

| Property | `const` | `static` |
|----------|---------|----------|
| Mutability | Always immutable | Can be mutable (requires `mut`) |
| Lifetime | Inlined at use site | Fixed memory address, `'static` lifetime |
| Safety | Always safe | Accessing/mutating a mutable static is `unsafe` |

```rust
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    n > THRESHOLD    // const accessible in any scope
}

fn main() {
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
}
```

## Key Rules

- **Global scope**: Both `const` and `static` can be declared outside functions.
- **Explicit types required**: Unlike `let` bindings, type annotations are mandatory.
- **`const` is immutable**: Attempting to reassign a `const` is a compile error.
- **Mutable `static` is `unsafe`**: Reading or writing a `static mut` requires an `unsafe` block, since data races are possible.

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust Primitives](rust-primitives.md) — the scalar types used as constant values
