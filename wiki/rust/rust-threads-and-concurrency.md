# Rust Threads and Concurrency

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-data-race.md](../../raw/rust/ardan-data-race.md); [ardan-count-primes.md](../../raw/rust/ardan-count-primes.md)

## Overview

Rust provides OS threads through the standard library's `std::thread` module. The borrow checker enforces thread safety at compile time — data races that compile silently in C++ and Go are caught as compiler errors in Rust.

## Spawning Threads

```rust
use std::thread;

let handle = thread::spawn(|| {
    // work to do in the new thread
    println!("Hello from a thread!");
});

handle.join().unwrap();  // wait for the thread to finish
```

## Move Closures

Threads may outlive the function that spawned them. Use `move` to transfer ownership of data into a closure:

```rust
let data = vec![1, 2, 3];
let handle = thread::spawn(move || {
    println!("{data:?}");  // data is moved into the closure
});
handle.join().unwrap();
```

## Data Race Prevention

Rust prevents data races that other languages allow silently. The following code will **not compile** in Rust:

```rust
let mut counter = 0;
let t1 = thread::spawn(|| {
    counter += 1;  // ERROR: closure may outlive the function
});
let t2 = thread::spawn(|| {
    counter += 1;  // ERROR: cannot borrow counter as mutable more than once
});
```

Compare with C++ and Go where equivalent code compiles but produces inconsistent results due to data races.

## CPU-Bound Workload Example

An inefficient prime number checker used to demonstrate concurrency:

```rust
fn is_prime(n: u32) -> bool {
    (2 ..= n/2).all(|i| n % i != 0 )
}

// Single-threaded: ~1.08s for 200,000 numbers
fn main() {
    const MAX: u32 = 200_000;
    let count = (2..MAX).filter(|n| is_prime(*n)).count();
    println!("Found {count} primes");
}
```

## Managing Multiple Threads

Store thread handles in a `Vec` and join them all:

```rust
let mut handles = Vec::new();
for i in 0..8 {
    handles.push(thread::spawn(move || {
        // do work with i
    }));
}

for handle in handles {
    handle.join().unwrap();
}
```

## See Also

- [Rust Borrow Checker](rust-borrow-checker.md) — how Rust prevents data races
- [Rust Atomic Operations](rust-atomic-operations.md) — thread-safe counters
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — shared mutable data
- [Rust Rayon](rust-rayon.md) — easy parallel iterators
- [Rust Async and Tokio](rust-async-and-tokio.md) — async concurrency model
