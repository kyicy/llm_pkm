# Rust Borrow Checker

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-borrow-checker.md](../../raw/rust/ardan-borrow-checker.md); [ardan-data-race.md](../../raw/rust/ardan-data-race.md)

## Overview

The borrow checker enforces Rust's ownership rules at compile time. It ensures memory safety without a garbage collector by guaranteeing that data races and use-after-free errors cannot occur.

## The Core Rules

1. **Each value has exactly one owner** at any time.
2. **Only one thing at a time may have mutable (write) access** to a variable.
3. **Any number of things may have read-only access** to a variable — but only if nothing can currently write to it.
4. **References must always be valid** — they cannot outlive the data they point to.

These rules apply regardless of whether the code is single-threaded or multi-threaded. Rust assumes all programs may be multi-threaded.

## Data Race Prevention

The borrow checker prevents data races that other languages allow silently.

### C++ (compiles, inconsistent results):

```cpp
uint32_t count = 0;
// Two threads increment count simultaneously — data race!
std::thread t1([&count]() { count++; });
std::thread t2([&count]() { count++; });
```

Each run produces different results because the threads overwrite each other's work.

### Go (compiles, inconsistent results):

```go
var count = 0
go func() { count++ }()  // data race!
go func() { count++ }()  // data race!
fmt.Println(count)
```

### Rust (does not compile):

```rust
let mut counter = 0;
std::thread::spawn(|| { counter += 1; });  // compile error!
std::thread::spawn(|| { counter += 1; });  // compile error!
```

Rust produces multiple errors:
- `cannot borrow counter as mutable more than once at a time`
- `closure may outlive the current function, but it borrows counter`
- `cannot borrow counter as immutable because it is also borrowed as mutable`

**Of the three languages, only Rust prevents the data race at compile time.**

## Best Practices

- Keep it simple. Keep a clear data-path through which data may be modified.
- Don't use Rust as an object-oriented language. Combine simple data types and retain a store associating types with types.
- Move ownership of operations to the level that actually owns all of the parts.
- Break work down into small, testable pieces.

## See Also

- [Rust Lifetimes](rust-lifetimes.md) — ensuring references remain valid
- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — spawning threads safely
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — safe shared mutable data
- [Rust Atomic Operations](rust-atomic-operations.md) — lock-free thread-safe counters
