# Rust Traits

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-traits.md](../../raw/rust/ardan-traits.md)

## Overview

Traits are Rust's mechanism for defining shared behavior — similar to interfaces in other languages. They describe a set of function signatures that implementing types must provide. Unlike classes in OOP languages, traits contain only function declarations, not data fields. Rust uses static dispatch by default (concrete types resolved at compile time), with `dyn` for dynamic dispatch.

## Defining and Implementing Traits

### Basic Trait

```rust
trait Animal {
    fn make_noise(&self);
}

struct Cat;
struct Tortoise;

impl Animal for Cat {
    fn make_noise(&self) {
        println!("Meow")
    }
}

impl Animal for Tortoise {
    fn make_noise(&self) {
        println!("Hiss")
    }
}

fn main() {
    let cat = Cat{};
    cat.make_noise();  // Meow
}
```

You cannot directly instantiate a trait — `let cat = Animal{};` fails because traits are not concrete types.

### Default Implementations

Traits can provide default function bodies. Types that implement the trait can override them:

```rust
trait Animal {
    fn make_noise(&self) {
        println!("Who knows what noise I make?")
    }
}

struct Tortoise;
impl Animal for Tortoise {}  // Uses default

struct Cat;
impl Animal for Cat {
    fn make_noise(&self) {    // Override
        println!("Meow")
    }
}
```

### Traits Cannot Contain Data

Traits define behavior, not structure. This does not compile:

```rust
trait Animal {
    name: String,             // ERROR: traits can't have fields
    fn make_noise(&self) { ... }
}
```

A trait implementation *can* access the implementing type's own fields (it knows the concrete type via `&self`):

```rust
struct Cat { noise: String }

impl Animal for Cat {
    fn make_noise(&self) {
        println!("{}", self.noise);  // Accesses Cat's field
    }
}
```

## Trait Bounds on Generic Functions

Use traits to constrain generic type parameters:

```rust
fn pet<A: Animal>(animal: A) {
    animal.make_noise()
}
```

### Multiple Trait Bounds

Combine trait requirements with `+`:

```rust
trait Tame {}

impl Tame for Cat {}

fn pet<A: Animal + Tame>(animal: A) {
    animal.make_noise()
}
```

Now `pet()` only accepts types that implement *both* `Animal` and `Tame`.

## Dynamic Dispatch with `dyn` Trait Objects

Storing different types that implement the same trait in a collection requires dynamic dispatch:

```rust
// ERROR: Vec infers type from first element (Box<Cat>)
let mut animals: Vec<Box<Animal>> = Vec::new(); // Error: missing `dyn`

// CORRECT: explicitly use dyn for dynamic dispatch
let mut animals: Vec<Box<dyn Animal>> = Vec::new();
animals.push(Box::new(cat));
animals.push(Box::new(tortoise));

for animal in animals.iter() {
    animal.make_noise();
}
```

The `dyn` keyword enables a **vtable** (virtual dispatch table) — at runtime, Rust looks up the correct function implementation for each element. This has a small performance cost compared to static dispatch, though LLVM can often optimize it away.

## Trait Dependencies (Supertraits)

A trait can require that implementors also implement other traits:

```rust
trait Animal: std::fmt::Debug {
    fn make_noise(&self);
}

// Now any type implementing Animal must also implement Debug:
#[derive(Debug)]
struct Cat;
impl Animal for Cat { ... }
```

Multiple supertraits can be combined with `+`:

```rust
trait Animal: std::fmt::Debug + std::fmt::Display { ... }
```

## Downcasting with `Any`

Rust provides runtime type inspection through the `Any` trait. This is deliberately verbose — prefer compile-time polymorphism when possible.

### Setup

```rust
use std::any::Any;

trait Animal: std::fmt::Debug + std::fmt::Display + Any {
    fn make_noise(&self) {
        println!("Who knows what noise I make?")
    }
    fn as_any(&self) -> &dyn Any;  // Required for downcasting
}
```

Each implementing type must provide `as_any`:

```rust
impl Animal for Cat {
    fn make_noise(&self) { println!("Meow") }
    fn as_any(&self) -> &dyn Any { self }
}
```

### Downcasting

```rust
for animal in animals.iter() {
    if let Some(cat) = animal.as_any().downcast_ref::<Cat>() {
        println!("We have access to the cat");
    }
    animal.make_noise();
}
```

`downcast_ref::<Cat>()` attempts a runtime type check — returning `Some(&Cat)` if the type matches, `None` otherwise.

## Key Points

- Traits are interfaces, not classes — no data fields, no inheritance trees.
- **Static dispatch** (monomorphization) is the default — fast but generates separate code per type.
- **Dynamic dispatch** (`dyn Trait`) uses vtables — flexible but has small runtime overhead.
- **Supertraits** (`Trait: OtherTrait`) enforce that implementors also satisfy other trait bounds.
- **`Any` downcasting** is available but should be a last resort — prefer trait-based polymorphism.
- Rust uses traits extensively in the standard library — `Debug`, `Display`, `Clone`, `From`, `Into`, `Iterator`, etc.

## See Also

- [Rust Traits and OOP](rust-traits-and-oop.md) — designing data structures with traits for ownership patterns
- [Rust Generic Data Structures](rust-generic-data-structures.md) — trait bounds on generic types with `where`
- [Rust NewType Pattern](rust-new-type-pattern.md) — `From`/`Into` traits for type conversion
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — `Debug` and `Display` traits
