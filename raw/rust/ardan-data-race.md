# Racing Data

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

A *data race* or *race condition* occurs whenever multiple objects can try to write to the same thing at once with no synchronization.

## The Same Problem in C++

```c++
uint32_t count = 0;
std::thread t1([&count, max]() {
    for (auto i = 2; i < max / 2; i++) {
        if (is_prime(i)) ++count;  // race condition!
    }
});
std::thread t2([&count, max]() {
    for (auto i = max / 2; i < max; i++) {
        if (is_prime(i)) ++count;  // race condition!
    }
});
```

C++ compiles without error but produces inconsistent results:
```
Found 17982 prime numbers.
Found 17983 prime numbers.
Found 17984 prime numbers.
```

## The Same Problem in Go

```go
var count = 0

func first_half() {
    for i := 2; i < max/2; i++ {
        if is_prime(i) { count++ }  // race condition!
    }
}

func second_half() {
    for i := max / 2; i < max; i++ {
        if is_prime(i) { count++ }  // race condition!
    }
}
```

Go also produces inconsistent results: `1229`, `1228`, `1227`, `1229`.

## Rust Prevents It at Compile Time

```rust
fn main() {
    const MAX: u32 = 200_000;
    let mut counter = 0;
    let t1 = std::thread::spawn(|| {
       counter += (2 .. MAX/2).filter(|n| is_prime(*n)).count();
    });
    let t2 = std::thread::spawn(|| {
       counter += (MAX/2 .. MAX).filter(|n| is_prime(*n)).count();
    });
    t1.join();
    t2.join();
    println!("Found {counter} prime numbers in the range 2..{MAX}");
}
```

**Rust won't compile.** Multiple errors including:
- `closure may outlive the current function, but it borrows counter`
- `cannot borrow counter as mutable more than once at a time`
- `cannot borrow counter as immutable because it is also borrowed as mutable`

The error boils down to: **Rust detected your race condition, and won't let you corrupt your data.** Of the three languages, only Rust saves the day.
