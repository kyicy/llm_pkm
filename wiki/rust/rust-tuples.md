# Rust Tuples

> Sources: Rust by Example, Unknown
> Raw: [tuples.md](../../raw/rust/2026-05-29-tuples.md)

## Overview

Tuples are compound types that collect values of different types into a single value. They are constructed with parentheses `()` and have type signatures of the form `(T1, T2, ...)`. Functions commonly use tuples to return multiple values.

## Construction and Type Signature

```rust
let long_tuple = (1u8, 2u16, 3u32, 4u64,
                  -1i8, -2i16, -3i32, -4i64,
                  0.1f32, 0.2f64,
                  'a', true);
```

Each element can be of a different type. The type signature reflects each element's type: `(u8, u16, u32, u64, i8, i16, i32, i64, f32, f64, char, bool)`.

## Accessing Tuple Elements

### Indexing

Elements are accessed by position using dot notation (0-indexed):

```rust
println!("First: {}", long_tuple.0);
println!("Second: {}", long_tuple.1);
```

### Destructuring

Tuples can be destructured to bind elements to named variables:

```rust
let tuple = (1, "hello", 4.5, true);
let (a, b, c, d) = tuple;
```

This also works in function parameters:

```rust
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    let (int_param, bool_param) = pair;
    (bool_param, int_param)
}
```

## Key Characteristics

- **Nesting**: Tuples can contain other tuples: `let nested = ((1u8, 2u16), (4u64, -1i8));`
- **Printing**: Tuples implement `Debug` and can be printed with `{:?}`. Tuples with more than 12 elements cannot be printed.
- **One-element tuples**: Require a trailing comma to distinguish from parenthesized expressions: `(5u32,)` is a tuple; `(5u32)` is just an integer.
- **Function returns**: Tuples enable returning multiple values from functions without defining a struct.

## Tuple Structs

Rust also supports tuple structs — named structs with positional fields:

```rust
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
```

These combine the naming benefits of structs with the positional access of tuples.

## See Also

- [Rust Primitives](rust-primitives.md) — overview of compound types including tuples
- [Rust Arrays and Slices](rust-arrays-and-slices.md) — the other compound type
- [Rust Structs](rust-structs.md) — tuple structs are named tuples with the `struct` keyword
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — implementing `Display` for custom types like tuple structs
