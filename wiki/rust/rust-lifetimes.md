# Rust Lifetimes

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-lifetimes.md](../../raw/rust/ardan-lifetimes.md)

## Overview

Lifetimes ensure that references are always valid — they prevent using a pointer after the data it points to has been freed or moved. The Rust compiler can infer lifetimes in simple cases (lifetime elision) but requires explicit annotations when the relationship between references is ambiguous.

## Lifetime Elision

Simple functions don't need explicit lifetime annotations — the compiler infers them:

```rust
// This is automatically annotated by the compiler:
fn do_something(x: &i32) {
    println!("{x}");
}

// The compiler treats it as:
fn do_something<'a>(x: &'a i32) {
    println!("{x}");
}
```

## When Annotations Are Required

Functions that return a reference and receive multiple references need explicit annotations:

```rust
// ERROR: which reference does the return borrow from?
fn get_x(x: &i32, _y: &i32) -> &i32 {
    x
}

// FIX: annotate lifetimes
fn get_x<'a, 'b>(x: &'a i32, _y: &'b i32) -> &'a i32 {
    x
}
```

## Lifetimes on Structs

Structures that hold references need lifetime annotations:

```rust
struct CatFeeder<'a> {
    cat: &'a Cat
}
```

With mutable references and implementation blocks:

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

When data goes out of scope, the borrow checker prevents use-after-free:

```rust
let mut feeders = Vec::new();
{
    let mut cats = vec![...];
    for cat in cats.iter_mut() {
        feeders.push(CatFeeder{ cat })
    }
}
// ERROR: `cats` does not live long enough
feeders.iter_mut().for_each(|f| f.feed());
```

## Reference Counting with Rc

For shared ownership, use `Rc<T>` (single-threaded):

```rust
use std::rc::Rc;

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
        owners.push(CatOwner{ cat: cat.clone() });  // clones Rc, not Cat
    }
}
```

`Rc::clone()` just increments a reference counter — it is very fast.

## Interior Mutability with RefCell

When you need to mutate data through an immutable reference:

```rust
use std::cell::RefCell;

struct Cat {
    name: RefCell<String>
}

impl Owner {
    fn feed(&self) {  // takes &self, not &mut self
        let mut name_borrow = self.cat.name.borrow_mut();
        *name_borrow += " (purring)";
    }
}
```

## Performance of Reference Counting

Release mode benchmark (10M iterations):
| Method | Per Operation |
|--------|---------------|
| Direct vector access | 25 ns |
| `Rc<T>` | 34 ns |
| `Arc<T>` (thread-safe) | 33 ns |
| Central store (HashMap by ID) | 268 ns |

## See Also

- [Rust Borrow Checker](rust-borrow-checker.md) — ownership and borrowing rules
- [Rust RAII](rust-raii.md) — `Drop` trait for resource cleanup
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — thread-safe shared state with `Arc<Mutex<T>>`
