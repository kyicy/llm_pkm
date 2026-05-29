# Rust Atomic Operations

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-atomic.md](../../raw/rust/ardan-atomic.md)

## Overview

Atomic variables provide thread-safe operations on primitive types without locks. They are typically implemented directly by the CPU with very low overhead. Rust provides atomic types in `std::sync::atomic`.

## Atomic Types

| Type | Description |
|------|-------------|
| `AtomicBool` | Boolean atomic |
| `AtomicI8`, `AtomicI16`, `AtomicI32`, `AtomicI64` | Signed integer atomics |
| `AtomicU8`, `AtomicU16`, `AtomicU32`, `AtomicU64` | Unsigned integer atomics |
| `AtomicUsize`, `AtomicIsize` | Pointer-sized integer atomics |
| `AtomicPtr<T>` | Pointer atomic |

## Basic Usage: Atomic Counter

```rust
use std::sync::atomic::{AtomicUsize, Ordering};

static COUNTER: AtomicUsize = AtomicUsize::new(0);

// Thread 1
COUNTER.fetch_add(42, Ordering::Relaxed);

// Thread 2 (after join)
let result = COUNTER.load(Ordering::Relaxed);
```

## Example: Counting Primes with Atomic

```rust
use std::sync::atomic::{AtomicUsize, Ordering};

fn is_prime(n: u32) -> bool {
    (2 ..= n/2).all(|i| n % i != 0 )
}

fn main() {
    const MAX: u32 = 200_000;
    static COUNTER: AtomicUsize = AtomicUsize::new(0);

    let t1 = std::thread::spawn(|| {
        COUNTER.fetch_add(
            (2 .. MAX/2).filter(|n| is_prime(*n)).count(),
            Ordering::Relaxed
        );
    });
    let t2 = std::thread::spawn(|| {
        COUNTER.fetch_add(
            (MAX/2 .. MAX).filter(|n| is_prime(*n)).count(),
            Ordering::Relaxed
        );
    });

    t1.join().unwrap();
    t2.join().unwrap();
    println!("Found {} primes", COUNTER.load(Ordering::Relaxed));
}
```

Each run produces the same correct result: `Found 17984 primes`.

## Memory Ordering

The `Ordering` enum controls the memory ordering guarantees:

| Ordering | Description |
|----------|-------------|
| `Relaxed` | No ordering guarantees, only atomicity |
| `Acquire` | Subsequent reads see writes from the releasing thread |
| `Release` | Ensures prior writes are visible to acquiring threads |
| `AcqRel` | Combines Acquire and Release |
| `SeqCst` | Sequential consistency (strongest guarantee) |

For simple counters, `Relaxed` is sufficient.

## Performance: Multiple Threads

| Configuration | Time (200,000 numbers) |
|--------------|----------------------|
| Single thread | ~1.086s |
| 2 threads (atomics) | ~0.797s |
| 8 threads (atomics) | ~0.272s |

## See Also

- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — spawning threads
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — Mutex for complex shared data
- [Rust Rayon](rust-rayon.md) — higher-level parallel processing
