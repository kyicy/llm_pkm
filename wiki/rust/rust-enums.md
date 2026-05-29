# Rust Enums

> Sources: Rust by Example, Unknown
> Raw: [enums.md](../../raw/rust/2026-05-29-enums.md); [enum-c-like.md](../../raw/rust/2026-05-29-enum-c-like.md); [enum-use.md](../../raw/rust/2026-05-29-enum-use.md)

## Overview

The `enum` keyword creates a type that can be one of several distinct variants. Each variant can carry different kinds and amounts of data: unit-like (no data), tuple-like (positional data), or struct-like (named fields). Enums are typically consumed via `match` expressions that handle every variant.

## Variant Kinds

Any variant form valid for a `struct` is also valid in an `enum`:

```rust
enum WebEvent {
    PageLoad,                       // unit-like
    PageUnload,                     // unit-like
    KeyPress(char),                 // tuple-like
    Paste(String),                  // tuple-like
    Click { x: i64, y: i64 },      // struct-like (named fields)
}

fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        WebEvent::Click { x, y } => println!("clicked at x={}, y={}.", x, y),
    }
}
```

Each variant is its own type — `PageLoad` and `PageUnload` are distinct despite both being unit-like.

## Type Aliases

When enum names are long or generic, type aliases provide shorter names. Variants can then be accessed through the alias:

```rust
enum VeryVerboseEnumOfThingsToDoWithNumbers { Add, Subtract }
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

let x = Operations::Add;
```

Within `impl` blocks, `Self` serves the same role:

```rust
impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

## C-Like Enums

Enums can be used as C-style integer enumerations with implicit or explicit discriminators:

```rust
// Implicit discriminator (starts at 0)
enum Number {
    Zero,   // 0
    One,    // 1
    Two,    // 2
}

// Explicit discriminator
enum Color {
    Red   = 0xff0000,
    Green = 0x00ff00,
    Blue  = 0x0000ff,
}
```

Enum variants can be cast to integers:

```rust
println!("zero is {}", Number::Zero as i32);       // "zero is 0"
println!("roses are #{:06x}", Color::Red as u32);  // "roses are #ff0000"
```

## Bringing Variants into Scope with `use`

The `use` declaration can import enum variants to avoid repeated qualification:

```rust
enum Stage { Beginner, Advanced }
enum Role { Student, Teacher }

use Stage::{Beginner, Advanced};  // selective import
use Role::*;                       // wildcard import

let stage = Beginner;   // instead of Stage::Beginner
let role = Student;     // instead of Role::Student

match stage {
    Beginner => println!("..."),  // no Stage:: prefix needed
    Advanced => println!("..."),
}
```

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust Structs](rust-structs.md) — enum variants mirror the three struct forms
- [Rust Linked List with Enums](rust-linked-list-with-enums.md) — practical enum pattern (Cons/Nil)
- [Rust Primitives](rust-primitives.md) — integers used as enum discriminators
