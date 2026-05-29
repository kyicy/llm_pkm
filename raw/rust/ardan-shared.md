# Shared Data

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

## Using Mutex for Shared State

Use a `Mutex`-wrapped vector for shared mutable data:

```rust
static PRIMES: Mutex<Vec<u32>> = Mutex::new(Vec::new());

threads.push(std::thread::spawn(move || {
    let range = u32::max(2, counter*group) .. (i+1)*group;
    let my_primes: Vec<u32> = range.filter(|n| is_prime(*n)).collect();
    PRIMES.lock().unwrap().extend(my_primes);
}));

println!("Found {} prime numbers", PRIMES.lock().unwrap().len());
```

`Mutex` is fast — lock contention overhead is minimal.

## Per-Thread Results (No Mutex)

Use `JoinHandle<T>` to return results from threads:

```rust
let mut threads: Vec<JoinHandle<Vec<u32>>> = Vec::with_capacity(N_THREADS as usize);

for i in 0 .. N_THREADS {
    threads.push(std::thread::spawn(move || {
        let range = u32::max(2, i*group) .. (i+1)*group;
        range.filter(|n| is_prime(*n)).collect()
    }));
}

let mut primes = Vec::new();
for thread in threads {
    if let Ok(new_primes) = thread.join() {
        primes.extend(new_primes);
    }
}

println!("Found {} prime numbers", primes.len());
```

Comparing Mutex version (~0.283s) with lock-free version (~0.263s): lock-free is faster but not dramatically so. Mutex is really, really fast.
