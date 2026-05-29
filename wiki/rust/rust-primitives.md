# Rust Primitives

> Sources: Rust by Example, Unknown
> Raw: [primitives.md](../../raw/rust/2026-05-29-primitives.md)

## Overview

Rust provides a rich set of primitive types divided into scalar types (single values) and compound types (collections of values). Variables can be type-annotated explicitly, annotated via numeric suffixes, or have their types inferred from context. Numeric types default to `i32` for integers and `f64` for floats when no annotation is present.

## Scalar Types

### Integers

Signed: `i8`, `i16`, `i32`, `i64`, `i128`, `isize` (pointer-sized).
Unsigned: `u8`, `u16`, `u32`, `u64`, `u128`, `usize` (pointer-sized).

The default integer type is `i32`.

### Floating Point

`f32` and `f64`, with `f64` as the default.

### Character and Boolean

`char` represents a Unicode scalar value (4 bytes each), e.g., `'a'`, `'α'`, `'∞'`.
`bool` is either `true` or `false`.

### Unit Type

The unit type `()` has exactly one value: an empty tuple `()`. Despite its tuple-like value, it is considered a scalar type because it contains no multiple values.

## Compound Types

- **Arrays**: Fixed-size collections of same-type elements, e.g., `[1, 2, 3]` with type signature `[T; length]`.
- **Tuples**: Collections of values of different types, e.g., `(1, true)` with type signature `(T1, T2, ...)`.

### Beyond Primitives

Rust also provides standard library types that build on these primitives:

- **Vectors** (`Vec<T>`): Heap-allocated, resizable arrays
- **Hashmaps** (`HashMap<K, V>`): Key-value dictionary with O(1) lookup
- **Options** (`Option<T>`): Safe nullable values
- **Strings** (`String`): Heap-allocated, growable UTF-8 string
- **Atomics** (`AtomicUsize`, etc.): Thread-safe primitive counters
- **Mutex** (`Mutex<T>`): Mutual exclusion for shared data

## Type Annotations and Inference

Variables can be type-annotated in three ways:

1. **Explicit annotation**: `let a_float: f64 = 1.0;`
2. **Suffix annotation**: `let an_integer = 5i32;`
3. **Default**: `let default_integer = 7;` (defaults to `i32`)

Rust also infers types from how a variable is used elsewhere:

```rust
let mut inferred_type = 12;       // initially i32
inferred_type = 4294967296i64;    // now inferred as i64
```

## Mutability and Shadowing

Variables are immutable by default. Use `mut` to make them mutable:

```rust
let mut mutable = 12;  // Mutable i32
mutable = 21;          // OK
```

A mutable variable's type cannot change. However, shadowing creates a new variable with the same name:

```rust
let mutable = true;    // shadows previous `mutable`, new type allowed
```

## See Also

- [Rust Literals and Operators](rust-literals-and-operators.md) — expressing primitive values
- [Rust Arrays and Slices](rust-arrays-and-slices.md) — fixed-size arrays and dynamic slices
- [Rust Tuples](rust-tuples.md) — heterogeneous value collections
- [Rust Custom Types](rust-custom-types.md) — structs, enums, and constants built on primitives
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — formatting types for output
- [Rust Vectors](rust-vectors.md) — heap-allocated, resizable array type
- [Rust Hashmaps](rust-hashmaps.md) — key-value dictionary type
- [Rust Atomic Operations](rust-atomic-operations.md) — thread-safe integer operations
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — shared mutable data
