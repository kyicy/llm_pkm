# Rust Generic Data Structures

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-generic-data.md](../../raw/rust/ardan-generic-data.md); [ardan-generic-complex.md](../../raw/rust/ardan-generic-complex.md)

## Overview

Rust supports generic data structures — types parameterized by one or more type variables. This enables reusable, type-safe containers like `Vec<T>`, `HashMap<K, V>`, and custom collections. Generics in structs mirror generics in functions: type parameters are declared with `<T>` and can be constrained with trait bounds.

## StableVec: A Generic Stable-ID Container

A `StableVec<T>` stores values while keeping index positions stable — removing an entry leaves a `None` placeholder so other indices remain valid.

### Struct Definition

```rust
#[derive(Debug)]
struct StableVec<T> {
    data: Vec<Option<T>>
}
```

The `<T>` declares a type parameter. Inside the struct, `T` is used as a placeholder for the element type.

### Constructor with `impl<T>`

The `impl` block must also declare the generic parameter:

```rust
impl <T> StableVec<T> {
    fn new() -> Self {
        Self { data: Vec::new() }
    }

    fn push(&mut self, item: T) -> usize {
        let id = self.data.len();
        self.data.push(Some(item));
        id
    }

    fn remove(&mut self, id: usize) {
        self.data[id] = None;
    }

    fn get(&self, id: usize) -> &Option<T> {
        &self.data[id]
    }
}
```

### Implementing the `Index` Trait

The `Index` trait enables bracket-access syntax (`store[3]`):

```rust
impl<T> Index<usize> for StableVec<T> {
    type Output = Option<T>;
    fn index(&self, index: usize) -> &Self::Output {
        &self.data[index]
    }
}
```

### Usage

```rust
fn main() {
    let mut store = StableVec::<String>::new();
    let a = store.push("A".to_string());
    let b = store.push("B".to_string());
    let c = store.push("C".to_string());
    store.remove(b);
    println!("{:?}", store.get(a));   // Some("A")
    println!("{:?}", store.get(b));   // None (removed)
    println!("{:?}", store[c]);       // Some("C") via Index
}
```

## HashSetData: Complex Multi-Generic Container

A key-value store where each key maps to a vector of values — demonstrating multiple type parameters and trait bounds with `where`.

### Basic Definition (No Constraints)

```rust
use std::collections::HashMap;

struct HashSetData<KEY, VALUE> {
    data: HashMap<KEY, Vec<VALUE>>
}

impl <KEY, VALUE> HashSetData<KEY, VALUE> {
    fn new() -> Self {
        Self { data: HashMap::new() }
    }
}
```

This compiles for the constructor, but adding a method that uses `HashMap` operations reveals missing trait bounds.

### Adding Trait Bounds with `where`

Methods like `get_mut` and `insert` require `KEY: Eq + Hash`:

```rust
struct HashSetData<KEY, VALUE>
where KEY: Eq + Hash
{
    data: HashMap<KEY, Vec<VALUE>>
}

impl <KEY, VALUE> HashSetData<KEY, VALUE>
where KEY: Eq + Hash
{
    // methods here...
}
```

The `where` clause must appear on *both* the struct definition and each `impl` block.

### Adding Data

```rust
fn add_reading(&mut self, key: KEY, reading: VALUE) {
    if let Some(entry) = self.data.get_mut(&key) {
        entry.push(reading);
    } else {
        self.data.insert(key, vec![reading]);
    }
}
```

### Combining Multiple Trait Bounds

You can require multiple traits for different type parameters:

```rust
where KEY: Eq + Hash, VALUE: Debug
```

### Custom Trait Requirements

Define a custom trait and require it as a bound:

```rust
trait Sensor {
    fn reading(&self) -> i32;
}

struct Data(i32);

impl Sensor for Data {
    fn reading(&self) -> i32 {
        self.0
    }
}
```

Then add the bound:

```rust
where KEY: Eq + Hash + std::fmt::Display, VALUE: Debug + Sensor
```

### Complete Example

```rust
use std::collections::HashMap;
use std::fmt::Debug;

trait Sensor {
    fn reading(&self) -> i32;
}

#[derive(Debug)]
struct Data(i32);

impl Sensor for Data {
    fn reading(&self) -> i32 { self.0 }
}

#[derive(Debug)]
struct HashSetData<KEY, VALUE>
where KEY: Eq + Hash + std::fmt::Display, VALUE: Debug + Sensor
{
    data: HashMap<KEY, Vec<VALUE>>
}

impl <KEY, VALUE> HashSetData<KEY, VALUE>
where KEY: Eq + Hash + std::fmt::Display, VALUE: Debug + Sensor
{
    fn new() -> Self {
        Self { data: HashMap::new() }
    }

    fn add_reading(&mut self, key: KEY, reading: VALUE) {
        if let Some(entry) = self.data.get_mut(&key) {
            entry.push(reading);
        } else {
            self.data.insert(key, vec![reading]);
        }
    }

    fn print_results(&self) {
        for (key, value) in self.data.iter() {
            let sum: i32 = value.iter().map(|r| r.reading()).sum();
            let avg = sum / value.len() as i32;
            println!("{key} : {avg}");
        }
    }
}

fn main() {
    let mut readings = HashSetData::<usize, Data>::new();
    readings.add_reading(1, Data(-2));
    readings.add_reading(1, Data(3));
    readings.add_reading(1, Data(5));
    readings.add_reading(2, Data(1));
    readings.print_results();
    // Output:
    // 2 : 1
    // 1 : 2
}
```

## Key Rules

- **`impl<T>`**: The type parameter must be declared on both the struct and the `impl` block.
- **`where` bounds**: Required on both struct definition and `impl` block whenever trait constraints are needed.
- **Trait bound propagation**: Calling methods on generic fields (e.g., `HashMap` operations) requires the generic parameters to satisfy that type's trait bounds.
- **Bound accumulation**: Trait bounds accumulate as you add functionality — adding a method that requires `Display` means adding `Display` to the existing bounds.
- **Compile-time monomorphization**: Rust generates a separate copy of the generic code for each concrete type used. All type checking happens at compile time.

## See Also

- [Rust NewType Pattern](rust-new-type-pattern.md) — generics with `From`/`Into` and trait bounds
- [Rust Traits](rust-traits.md) — trait fundamentals, bounds, and `dyn` dispatch
- [Rust Vectors](rust-vectors.md) — the element storage used in generic containers
- [Rust Hashmaps](rust-hashmaps.md) — key-value storage used in `HashSetData`
- [Rust Structs](rust-structs.md) — struct definitions with generic parameters
