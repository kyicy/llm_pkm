# Atomically Counting Primes

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Atomic variables guarantee no concurrency issues. They are typically implemented by the CPU with very low overhead.

## Basic Atomic Counter

```rust
use std::sync::atomic::AtomicUsize;

fn is_prime(n: u32) -> bool {
    (2 ..= n/2).all(|i| n % i != 0 )
}

fn main() {
    const MAX: u32 = 200_000;
    static COUNTER: AtomicUsize = AtomicUsize::new(0);
    let t1 = std::thread::spawn(|| {
        COUNTER.fetch_add(
            (2 .. MAX/2).filter(|n| is_prime(*n)).count(),
            std::sync::atomic::Ordering::Relaxed
        );
    });
    let t2 = std::thread::spawn(|| {
        COUNTER.fetch_add(
            (MAX/2 .. MAX).filter(|n| is_prime(*n)).count(),
            std::sync::atomic::Ordering::Relaxed
        );
    });
    t1.join();
    t2.join();
    println!("Found {} prime numbers", COUNTER.load(std::sync::atomic::Ordering::Relaxed));
}
```

Each run produces the same result: `Found 17984 prime numbers`.

With timing (2 threads): ~0.797 seconds compared to ~1.086 seconds single-threaded.

## Using Many Threads

```rust
const N_THREADS: u32 = 8;
static COUNTER: AtomicUsize = AtomicUsize::new(0);
let mut threads = Vec::with_capacity(N_THREADS as usize);
let group = MAX / N_THREADS;

for i in 0 .. N_THREADS {
    threads.push(std::thread::spawn(move || {
        let range = u32::max(2, i*group) .. (i+1)*group;
        COUNTER.fetch_add(
            range.filter(|n| is_prime(*n)).count(),
            std::sync::atomic::Ordering::Relaxed
        );
    }));
}

for thread in threads {
    let _ = thread.join();
}
```

With 8 threads: ~0.272 seconds — a significant speedup.
