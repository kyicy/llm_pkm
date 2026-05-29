# Rust Rayon

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-rayon.md](../../raw/rust/ardan-rayon.md)

## Overview

Rayon is a data-parallelism library for Rust that makes it easy to convert sequential iterator chains into parallel computations. It uses a work-stealing thread pool and provides `par_iter` and `into_par_iter` methods on iterable types.

## Setup

```toml
[dependencies]
rayon = "1"
```

## Basic Parallel Iterator

Adding `.into_par_iter()` to an iterator chain enables parallelism:

```rust
use rayon::prelude::{IntoParallelIterator, ParallelIterator};

fn is_prime(n: u32) -> bool {
    (2 ..= n/2).all(|i| n % i != 0 )
}

fn main() {
    let count = (2..200_000u32)
        .into_par_iter()   // single change: parallel iterator
        .filter(|n| is_prime(*n))
        .count();

    println!("Found {count} primes");
}
```

### Performance

| Configuration | Time | Speedup |
|--------------|------|---------|
| Single-threaded | ~1.08s | 1x |
| Rayon (auto-parallel) | ~0.106s | ~10x |

A 10x speedup by adding one line of code.

## Required Imports

```rust
use rayon::prelude::*;  // brings IntoParallelRefIterator, ParallelIterator, etc.
```

## Managing Tasks with Scope

Rayon's `scope` function manages groups of tasks. The scope waits until all child tasks complete:

```rust
fn hello(n: u64) {
    println!("Hello from thread {n}");
    std::thread::sleep(std::time::Duration::from_secs(n));
    println!("Bye from thread {n}");
}

fn main() {
    rayon::scope(|s| {
        for i in 0..8 {
            s.spawn(move |_| hello(i));
        }
    });
    // All tasks complete before this line runs
}
```

## Key Methods

| Method | On | Description |
|--------|-----|-------------|
| `.into_par_iter()` | `Vec<T>`, ranges, etc. | Consumes the collection, parallel iteration |
| `.par_iter()` | `&[T]`, `&Vec<T>` | Borrows for parallel iteration |
| `.par_iter_mut()` | `&mut [T]` | Mutable parallel iteration |
| `rayon::scope()` | Function | Scoped task spawning with automatic join |

## See Also

- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — manual thread management
- [Rust Atomic Operations](rust-atomic-operations.md) — thread-safe counters
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — shared state between Rayon tasks
