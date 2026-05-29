# Rust NewType Pattern

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-new-types.md](../../raw/rust/ardan-new-types.md)

## Overview

The NewType pattern uses a tuple struct with a single field to create a distinct type from an existing one. This provides compile-time type safety — preventing accidental mixing of units, representations, or semantically different values that share the same underlying type (e.g., `f32` for both radians and degrees).

## Basic NewType: Distinguishing Units

### The Problem

Raw primitive types don't distinguish between different units of measurement:

```rust
// Function expects radians, but nothing enforces this
fn project_angle(start: (f32, f32), angle: f32, radius: f32) -> (f32, f32) {
    (
        0.0 - (start.0 + radius * f32::sin(angle)),
        start.1 + radius * f32::cos(angle),
    )
}

// 180.0 passed directly — expects radians but gets degrees
let finish = project_angle(start, 180.0, 10.0);
// Result: (8.011526, -5.984601) — wrong!
```

### The Solution: NewType Wrappers

```rust
struct Radians(f32);
struct Degrees(f32);

impl Degrees {
    fn to_radians(&self) -> f32 {
        self.0.to_radians()
    }
}

fn project_angle(start: (f32, f32), angle: Radians, radius: f32) -> (f32, f32) {
    (
        0.0 - (start.0 + radius * f32::sin(angle.0)),
        start.1 + radius * f32::cos(angle.0),
    )
}

// Now you can't accidentally pass raw degrees:
let finish = project_angle(start, Radians(180.0f32.to_radians()), 10.0);
```

## Implementing `From` for Ergonomics

The `From` trait provides automatic conversion between types:

```rust
impl From<Degrees> for Radians {
    fn from(deg: Degrees) -> Radians {
        Radians(deg.0.to_radians())
    }
}

// Now you can use `.into()`:
let finish = project_angle(start, Degrees(180.0).into(), 10.0);
```

`From` automatically provides the reciprocal `Into` trait implementation.

## Generic Functions with Trait Bounds

Combine NewTypes with generic functions that accept any type convertible to your target:

```rust
fn project_angle<A: Into<Radians>>(start: Point, angle: A, radius: f32) -> Point {
    let angle: Radians = angle.into();
    Point::new(
        0.0 - (start.x + radius * f32::sin(angle.0)),
        start.y + radius * f32::cos(angle.0),
    )
}

// Call directly — no .into() needed:
let finish = project_angle(start, Degrees(180.0), 10.0);
```

The `<A: Into<Radians>>` syntax declares that `A` must implement the `Into<Radians>` trait. This means:
- You can pass `Degrees` or `Radians` directly.
- You can't pass a raw `f32` (no `Into<Radians>` for `f32`).
- Rust generates a specialized function for each concrete type used.

> **Note**: Generic functions increase binary size — monomorphization creates a copy for each concrete type.

### `ToString` as a Generic Bound

A useful idiomatic pattern — accept anything that can be stringified:

```rust
fn take_my_text<S: ToString>(text: S) {
    let s = text.to_string();
    // Work with the string
}

fn main() {
    take_my_text("Hello");           // &str
    take_my_text("Hello".to_string()); // String
    take_my_text(String::new());     // empty String
    let n = 5;
    take_my_text(n);                 // integer
}
```

## Operator Overloading

Rust allows operator overloading via the `std::ops` traits. These can be implemented for NewType and custom types.

### `Add`

```rust
impl std::ops::Add<Point> for Point {
    type Output = Point;
    fn add(mut self, rhs: Point) -> Point {
        self.x += rhs.x;
        self.y += rhs.y;
        self
    }
}

// Usage:
let start = start + Point::new(1.0, 1.0);
```

### `AddAssign`

```rust
impl std::ops::AddAssign for Point {
    fn add_assign(&mut self, other: Self) {
        *self = Self {
            x: self.x + other.x,
            y: self.y + other.y,
        };
    }
}

// Usage:
start += Point::new(1.0, 1.0);
```

> Rust allows implementing standard operator traits but does not allow creating new operators or changing their built-in semantics. While the compiler won't stop you from making `+` do subtraction, you shouldn't do it.

## Key Benefits

- **Type safety**: Prevents accidental mixing of different units or representations.
- **Compile-time enforcement**: Errors are caught at compile time, not runtime.
- **Zero runtime cost**: NewTypes are erased at compile time — no runtime overhead.
- **API clarity**: Function signatures express their requirements explicitly.

## See Also

- [Rust Generic Data Structures](rust-generic-data-structures.md) — generic types and `impl<T>` blocks
- [Rust Traits](rust-traits.md) — trait fundamentals and bounds
- [Rust Structs](rust-structs.md) — tuple structs (the structural basis for NewTypes)
- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
