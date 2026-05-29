# Rust Structs

> Sources: Rust by Example, Unknown
> Raw: [structs.md](../../raw/rust/2026-05-29-structs.md)

## Overview

Rust supports three kinds of structs via the `struct` keyword: classic C-like structs with named fields, tuple structs (essentially named tuples), and unit structs with no fields (useful for generics and marker types). Structs support field init shorthand, struct update syntax, destructuring, and can be nested as fields of other structs.

## Three Struct Variants

### Classic C Structs

Named fields accessed with dot notation:

```rust
struct Point {
    x: f32,
    y: f32,
}

let point = Point { x: 5.2, y: 0.4 };
println!("({}, {})", point.x, point.y);
```

### Tuple Structs

Positional fields accessed by index, like named tuples:

```rust
struct Pair(i32, f32);

let pair = Pair(1, 0.1);
println!("{} and {}", pair.0, pair.1);
```

### Unit Structs

No fields at all — useful as marker types or for trait implementations on types that carry no data:

```rust
struct Unit;
let _unit = Unit;
```

## Construction Patterns

### Field Init Shorthand

When variable names match field names, omit the colon:

```rust
let name = String::from("Peter");
let age = 27;
let peter = Person { name, age };  // equivalent to name: name, age: age
```

### Struct Update Syntax

Copy remaining fields from another instance of the same type:

```rust
let bottom_right = Point { x: 10.3, ..another_point };
// bottom_right.y is taken from another_point.y
```

## Destructuring

Structs can be destructured in `let` bindings:

```rust
let Point { x: left_edge, y: top_edge } = point;

// Tuple structs
let Pair(integer, decimal) = pair;
```

## Nested Structs

Structs can be composed as fields of other structs:

```rust
struct Rectangle {
    top_left: Point,
    bottom_right: Point,
}
```

Derive `Debug` (`#[derive(Debug)]`) to enable debug printing with `{:?}`.

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust Enums](rust-enums.md) — enum variants can be unit-like, tuple-like, or struct-like
- [Rust Tuples](rust-tuples.md) — tuple structs build on the same concepts
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — `Debug` and `Display` for structs
