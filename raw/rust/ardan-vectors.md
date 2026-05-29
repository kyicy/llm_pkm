# Vectors

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

A *Vec* is just like an array, but:

* Vectors are *resizable*. You can add or remove elements at any time.
* Like arrays, Vectors guarantee that all data will be stored contiguously in memory.
* Arrays store their data on the *stack*. Vectors store all of their data on the *heap*.

Replace your `get_users()` function with:

```rust
pub fn get_users() -> Vec<User> {
    vec![
        User::new("herbert", "password", LoginAction::Accept(Role::Admin)),
        User::new("bob", "password", LoginAction::Accept(Role::User)),
        User::new("fred", "password", LoginAction::Denied(DeniedReason::PasswordExpired)),
    ]
}
```

Notice:
* Instead of an array, we return `Vec<User>`. The angle brackets are *generic type indicators*.
* The `[..]` has been replaced with `vec![..]`.
* The rest of the program still works. Vectors convert to slices *exactly* like arrays.

## How Vectors Work Internally

```rust
pub struct Vec<T, A: Allocator = Global> {
    buf: RawVec<T, A>,
    len: usize,
}
```

* `buf` defines the "raw vector" — a contiguous block of memory.
* `len` lists how many items are in the vector.

```rust
pub(crate) struct RawVec<T, A: Allocator = Global> {
    ptr: Unique<T>,
    cap: usize,
    alloc: A,
}
```

* `ptr` is a *unique pointer* to a block of memory.
* `cap` lists the current *vector capacity*.
* `alloc` is the currently active allocator.

### Capacity vs Length

If a vector doesn't have available capacity for a new entry, it has to request a new block of memory from the Operating System, move its contents into the new block, and add the new member. This is relatively slow, so vectors reserve some extra space ahead of time.

```rust
fn main() {
    let mut my_vector = Vec::new();
    for i in 0..20 {
        my_vector.push(0);
        println!("Size: {}, Capacity: {}", my_vector.len(), my_vector.capacity());
    }
}
```

Output:
```
Size: 1, Capacity: 4
Size: 2, Capacity: 4
...
Size: 5, Capacity: 8
...
Size: 9, Capacity: 16
...
Size: 17, Capacity: 32
```

**Every time the vector runs out of capacity, it doubles the capacity.**

This is important:
* If you know the capacity in advance, use `Vec::with_capacity(n)` to pre-reserve space.
* If you have a really big vector, adding can be slow if it has to reallocate.
* If you are adding to a really big vector, you may use twice as much memory as intended during reallocation.

## Getting Data into Vectors

### Push

```rust
let mut users = get_users();
users.push(User::new("kent", "password", LoginAction::Accept(Role::Limited)));
```

### Deleting with Retain

```rust
users.retain(|u| u.username == "kent");
```

Retain takes a closure that returns true if an entry should be kept.

### Deleting with Remove

```rust
users.remove(0);
```

### Collecting from Iterators

```rust
let usernames: Vec<&String> = users
    .iter()
    .map(|u| &u.username)
    .collect();
println!("{usernames:#?}");
```

`:#?` is "pretty print debug information".
