# Counting Prime Numbers - Badly

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

An inefficient prime number checker for CPU-bound workload demonstration:

```rust
fn is_prime(n: u32) -> bool {
   (2 ..= n/2).all(|i| n % i != 0 )
}
```

Unit test:

```rust
#[cfg(test)]
mod test {
    use super::*;

    #[test]
    fn test_first_hundred_primes() {
        let primes: Vec<u32> = (2..100).filter(|n| is_prime(*n)).collect();
        assert_eq!(
          primes,
           [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
        );
     }
}
```

Single-threaded loop:

```rust
fn main() {
    let mut count = 0;
    let now = std::time::Instant::now();
    for i in 2 .. MAX {
        if is_prime(i) {
            count += 1;
        }
    }
    let time = now.elapsed();
    println!("Found {count} primes in {} seconds", time.as_secs_f32());
}
```

In release mode, counting primes up to 200,000 takes approximately 1.08 seconds.
