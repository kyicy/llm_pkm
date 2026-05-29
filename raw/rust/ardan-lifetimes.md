# Lifetimes

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Lifetimes prevent using a pointer after the item being pointed to is no longer available (it moved, was freed, etc.).

## Lifetimes with Functions

Simple references have lifetimes inferred (lifetime elision):

```rust
fn do_something(x: &i32) {
    println!("{x}");
}
```

When Rust was new, you'd have had to write:

```rust
fn do_something<'a>(x: &'a i32) {
    println!("{x}");
}
```

### Functions with Multiple References

When a function returns a reference and takes more than one reference, lifetime annotations are required:

```rust
// This won't compile: which reference does the return borrow from?
fn get_x(x: &i32, _y: &i32) -> &i32 {
    x
}
```

Fix with explicit lifetimes:

```rust
fn get_x<'a, 'b>(x: &'a i32, _y: &'b i32) -> &'a i32 {
    x
}
```

## Lifetimes for Structures

Structures that hold references need lifetime annotations:

```rust
struct Cat(String);

struct CatFeeder<'a> {
    cat: &'a Cat
}

fn main() {
    let cats = vec![
        Cat("Frodo".to_string()),
        Cat("Bilbo".to_string()),
        Cat("Pippin".to_string()),
    ];

    let mut feeders = Vec::new();
    for cat in cats.iter() {
        feeders.push(CatFeeder{ cat })
    }
}
```

### Mutable References in Structures

```rust
struct CatFeeder<'a> {
    cat: &'a mut Cat
}

impl Cat {
    fn feed(&mut self) {
        self.0 = format!("{} (purring)", self.0);
    }
}

impl<'a> CatFeeder<'a> {
    fn feed(&mut self) {
        self.cat.feed();
    }
}
```

### Lifetime Protection in Action

When `cats` goes out of scope before feeders are used, Rust catches it:

```rust
fn main() {
    let mut feeders = Vec::new();
    {
        let mut cats = vec![...];
        for cat in cats.iter_mut() {
            feeders.push(CatFeeder{ cat })
        }
    }
    // Error: `cats` does not live long enough
    feeders.iter_mut().for_each(|f| f.feed());
}
```

## Reference Counting with Rc

When you need shared ownership, use `Rc` (single-threaded reference counting):

```rust
use std::rc::Rc;

struct Cat(String);

struct CatOwner {
    cat: Rc<Cat>
}

fn main() {
    let cats = vec![
        Rc::new(Cat("Frodo".to_string())),
        Rc::new(Cat("Bilbo".to_string())),
    ];

    let mut owners = Vec::new();
    for cat in cats {
        owners.push(CatOwner{ cat: cat.clone() });  // clones the Rc, not the Cat
    }
}
```

`Rc` is designed to be cloned — it just increments the reference counter.

### Drop with Rc

```rust
impl Drop for Cat {
    fn drop(&mut self) {
        println!("{} was dropped", self.0);
    }
}
```

Note: `for cat in owners` moves each owner. Use `for cat in owners.iter()` to avoid moving.

## Interior Mutability with RefCell

When you need mutable access through an immutable reference:

```rust
use std::rc::Rc;
use std::cell::RefCell;

struct Cat {
    name: RefCell<String>
}

struct Owner {
    cat: Rc<Cat>
}

impl Owner {
    fn feed(&self) {
        let mut name_borrow = self.cat.name.borrow_mut();
        *name_borrow += " (purring)";
    }
}
```

This pattern is called *interior mutability*. `RefCell` implements runtime locking to ensure `borrow_mut` and `borrow` won't break memory safety.

## Performance of Reference Counting

Benchmark results (10 million iterations, release mode):
- Vector of Cats: 25 nanos per cat
- RC Cats: 34 nanos per cat (+9ns)
- ARC Cats (thread-safe): 33 nanos per cat (+8ns)
- Central Cat Store (HashMap by ID): 268 nanos per cat

The overhead of reference counting is minimal.
