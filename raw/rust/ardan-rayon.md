# Using Rayon

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Rayon is a popular Rust crate for CPU-bound parallel processing. It uses a work-stealing thread pool and offers `par_iter` to transform regular iterator tasks into parallel tasks.

## Setup

```
cargo add rayon
```

## Basic Parallel Iterator

```rust
use rayon::prelude::{IntoParallelIterator, ParallelIterator};

fn is_prime(n: u32) -> bool {
    (2 ..= n/2).all(|i| n % i != 0 )
}

fn main() {
    const MAX: u32 = 200000;
    let now = std::time::Instant::now();

    let count = (2..MAX)
        .into_par_iter()  // <<< This one line adds parallelism
        .filter(|n| is_prime(*n))
        .count();

    let duration = now.elapsed();
    println!("Found {count} primes in {} seconds", duration.as_secs_f32());
}
```

Single-threaded: ~1.08s. With Rayon: ~0.106s. A 10x speedup by adding one line.

## Managing Tasks with Scope

Rayon uses `scope` to manage groups of tasks:

```rust
use std::{thread::sleep, time::Duration};

fn hello(n: u64) {
    println!("Hello from thread {n}");
    sleep(Duration::from_secs(n));
    println!("Bye from thread {n}");
}

fn main() {
    rayon::scope(|s| {
        for i in 0..8 {
            s.spawn(move |_| hello(i));
        }
    });
}
```

A scope waits until all child jobs have finished before returning.
