# Rust Vectors

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-vectors.md](../../raw/rust/ardan-vectors.md)

## Overview

`Vec<T>` is a heap-allocated, resizable array type. It stores elements contiguously in memory and supports adding and removing elements at runtime. Vectors are one of the most commonly used data structures in Rust.

## Creating Vectors

### With `vec!` Macro

```rust
let v = vec![1, 2, 3, 4, 5];
```

### With `Vec::new()`

```rust
let mut v: Vec<i32> = Vec::new();
```

### With Pre-Allocated Capacity

```rust
let mut v = Vec::with_capacity(100);  // reserves space for 100 elements
```

## Adding and Removing Elements

### Push (append to end)

```rust
let mut users = get_users();
users.push(User::new("kent", "password", LoginAction::Accept(Role::Limited)));
```

### Retain (conditional deletion)

Removes all elements for which the closure returns `false`:

```rust
users.retain(|u| u.username == "kent");
```

### Remove (by index)

```rust
users.remove(0);
```

Retain is generally safer than remove unless you know the exact index.

## Iterator Patterns

Vectors work well with Rust's iterator system:

### Collecting from Iterators

```rust
let usernames: Vec<&String> = users
    .iter()
    .map(|u| &u.username)
    .collect();
```

## Slices and Vectors

Vectors automatically coerce to slices, making them drop-in replacements for functions accepting `&[T]`:

```rust
pub fn get_users() -> Vec<User> { ... }  // return Vec
pub fn login(users: &[User], ...) { ... } // accept &[T]

let users = get_users();
login(&users, ...);  // Vec autoconverts to &[User]
```

## Internal Structure

```rust
pub struct Vec<T, A: Allocator = Global> {
    buf: RawVec<T, A>,
    len: usize,
}
```

- **RawVec**: A contiguous block of heap memory with capacity tracking
- **len**: Current number of elements

## Capacity and Growth

Vectors have both a *length* (number of items) and a *capacity* (allocated space). When capacity is exhausted and a new element is pushed, the vector doubles its capacity and reallocates:

```
Size: 1, Capacity: 4
Size: 4, Capacity: 4
Size: 5, Capacity: 8   // doubled
Size: 8, Capacity: 8
Size: 9, Capacity: 16  // doubled
```

This doubling strategy is important:
- Use `Vec::with_capacity(n)` when you know the size in advance to avoid repeated reallocations
- Appending to large vectors can be slow when reallocation occurs
- During reallocation, memory usage temporarily doubles

## Storing JoinHandles

Vectors are commonly used to store thread handles:

```rust
let mut handles: Vec<JoinHandle<Vec<u32>>> = Vec::new();

for i in 0..8 {
    handles.push(std::thread::spawn(move || {
        compute_primes_in_range(i)
    }));
}
```

See [Rust Threads and Concurrency](rust-threads-and-concurrency.md) for details.

## See Also

- [Rust Arrays and Slices](rust-arrays-and-slices.md) — fixed-size arrays vs resizable vectors
- [Rust Hashmaps](rust-hashmaps.md) — key-value storage alternative for lookups
- [Rust Structs](rust-structs.md) — storing structs in vectors with slice parameters
- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — using Vec for JoinHandles
- [Rust Rayon](rust-rayon.md) — parallel iterators on vectors
