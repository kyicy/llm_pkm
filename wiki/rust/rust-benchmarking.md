# Rust Benchmarking

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-benchmarks.md](../../raw/rust/ardan-benchmarks.md); [ardan-benchmarks2.md](../../raw/rust/ardan-benchmarks2.md)

## Overview

Rust offers several approaches to benchmarking, from quick timing with `std::time::Instant` to full-featured benchmark suites like Criterion. The choice depends on how rigorous you need the results to be.

## Quick & Dirty: `std::time::Instant`

For a fast estimate of how long something takes:

```rust
use std::time::Instant;

fn main() {
    let now = Instant::now();
    let mut i = 0;
    for j in 0 .. 1_000 {
        i += j * j;
    }
    let elapsed = now.elapsed();
    println!("Time elapsed: {} nanos", elapsed.as_nanos());
    println!("{i}");
}
```

This is handy for ad-hoc measurements but not 100% accurate — reading the clock isn't instantaneous.

## Nightly `#[bench]` with `test::Bencher`

Rust has built-in benchmark support on the nightly channel. Add `#![feature(test)]` to enable it:

```rust
#![feature(test)]

extern crate test;

pub fn add(left: usize, right: usize) -> usize {
    left + right
}

#[cfg(test)]
mod tests {
    use super::*;
    use test::Bencher;

    #[bench]
    fn bench_add(b: &mut Bencher) {
        b.iter(|| add(2, 4));
    }
}
```

Run with:

```bash
$ cargo +nightly bench
```

**Downside:** This requires the nightly toolchain. A common workaround is to comment out the benchmarks when not using them.

### Setup

```bash
$ rustup install nightly
$ cargo init bench --lib
```

## Criterion

[Criterion](https://github.com/bheisler/criterion.rs) is the recommended production benchmark framework. It works on stable Rust and generates HTML reports with statistics.

### Setup

In `Cargo.toml`:

```toml
[dev-dependencies]
criterion = { version = "0.4", features = [ "html_reports" ] }

[[bench]]
name = "my_benchmark"
harness = false
```

> `[dev-dependencies]` loads dependencies only for development — they aren't included in the final binary.

Create `benches/my_benchmark.rs`:

```rust
use criterion::{black_box, criterion_group, criterion_main, Criterion};

fn fibonacci(n: u64) -> u64 {
    match n {
        0 => 1,
        1 => 1,
        n => fibonacci(n-1) + fibonacci(n-2),
    }
}

fn criterion_benchmark(c: &mut Criterion) {
    c.bench_function("fib 20", |b| b.iter(|| fibonacci(black_box(20))));
}

criterion_group!(benches, criterion_benchmark);
criterion_main!(benches);
```

Run with:

```bash
$ cargo bench
```

HTML reports are generated in `target/criterion/` with full statistics.

### `black_box`

`black_box` prevents the compiler from optimizing away the benchmarked code by making it appear as a black-box function call to the optimizer.

## Approach Comparison

| Approach | Rust Version | Output | Precision |
|----------|-------------|--------|-----------|
| `Instant::now()` | Stable | Console print | Low |
| `#[bench]` | Nightly only | Cargo test output | Medium |
| Criterion | Stable | Console + HTML reports | High |

## See Also

- [Rust Testing](rust-testing.md) — unit testing, doc tests, and `#[bench]` integration
- [Rust Async and Tokio](rust-async-and-tokio.md) — understanding green-thread overhead in benchmarks
