# Rust Mutex and Shared State

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-shared.md](../../raw/rust/ardan-shared.md); [ardan-sync.md](../../raw/rust/ardan-sync.md)

## Overview

`Mutex<T>` provides mutual exclusion for shared mutable data — ensuring that only one thread at a time can access the protected value. In Rust, the Mutex owns the data it protects, enforcing safe access patterns through its API.

## Basic Mutex Usage

Use `Mutex` to protect shared mutable data with a static lifetime:

```rust
use std::sync::Mutex;

static PRIMES: Mutex<Vec<u32>> = Mutex::new(Vec::new());

fn main() {
    let mut handles = vec![];
    for i in 0..8 {
        handles.push(std::thread::spawn(move || {
            let my_data = compute_primes(i);
            PRIMES.lock().unwrap().extend(my_data);
        }));
    }
    for h in handles { h.join().unwrap(); }
    println!("Found {} primes", PRIMES.lock().unwrap().len());
}
```

The `lock()` call returns a `MutexGuard` that automatically releases the lock when it drops (RAII).

## Per-Thread Results with JoinHandle

For many workloads, collecting per-thread results via `JoinHandle<T>` avoids the need for a Mutex entirely:

```rust
use std::thread::JoinHandle;

let mut threads: Vec<JoinHandle<Vec<u32>>> = Vec::new();

for i in 0..8 {
    threads.push(std::thread::spawn(move || {
        compute_primes_in_range(i)  // returns Vec<u32>
    }));
}

let mut all_primes = Vec::new();
for thread in threads {
    if let Ok(result) = thread.join() {
        all_primes.extend(result);
    }
}
```

### Mutex vs Per-Thread Performance

| Approach | Time (200,000 primes) |
|----------|----------------------|
| Mutex shared vector | ~0.283s |
| Per-thread results (JoinHandle) | ~0.263s |

The Mutex overhead is minimal — it's really, really fast.

## Understanding Locking

Locking is a two-stage process:

```rust
fn main() {
    let mut lock = SHARED.lock().unwrap();
    lock.0 += 1;
    println!("{}", lock.0);
}
```

- `lock()` obtains exclusive access to the interior variable. You can mutate it.
- `unwrap()` catches any errors (e.g., poisoned mutex from a panicked thread).

### `const fn` Constructors

To use a static `Mutex<T>` with custom types, the constructor must be const:

```rust
static SHARED: Mutex<MyType> = Mutex::new(MyType::new(5));
// MyType::new must be `const fn`
```

## Deadlocks

**Rust provides no protection against deadlocks.** Deadlocks happen at runtime, and most of Rust's safety is compile-time.

Accidental double-lock:

```rust
let mut lock = SHARED.lock().unwrap();
lock.0 += 1;
println!("{}", SHARED.lock().unwrap().0);  // DEADLOCK: same mutex locked twice
```

### Deadlock Prevention

1. **Scoped locking**: Use interior braces to limit the lock's scope:

```rust
fn main() {
    {
        let mut lock = SHARED.lock().unwrap();
        lock.0 += 1;
    }  // lock is dropped here
    println!("{}", SHARED.lock().unwrap().0);  // OK
}
```

2. **Manual drop**: Use `std::mem::drop` to release early:

```rust
fn main() {
    let mut lock = SHARED.lock().unwrap();
    lock.0 += 1;
    std::mem::drop(lock);  // Release explicitly
    println!("{}", SHARED.lock().unwrap().0);  // OK
}
```

## RwLock: Read/Write Lock

`RwLock` is an alternative to `Mutex` with two access modes — multiple concurrent readers or a single writer.

```rust
use std::sync::RwLock;

static SHARED: RwLock<MyType> = RwLock::new(MyType::new(5));

fn main() {
    for _ in 0..10 {
        std::thread::spawn(|| {
            let read_lock = SHARED.read().unwrap();
            println!("The value of SHARED is {}", read_lock.0)
        });
    }
    std::thread::spawn(|| {
        let mut write_lock = SHARED.write().unwrap();
        write_lock.0 += 1;
    });

    std::thread::sleep(std::time::Duration::from_secs(5));
}
```

### RwLock Semantics

| Lock Type | Method | Behavior |
|-----------|--------|----------|
| Read | `.read()` | Unlimited concurrent readers |
| Write | `.write()` | Single writer, blocks all readers |

- **Multiple readers**: Any number of threads can hold a read lock simultaneously.
- **Single writer**: Only one thread can hold a write lock, and no read locks can be active.
- **Writer starvation**: If readers never drop their locks (e.g., sleeping while holding a read lock), writers will block indefinitely.

### Avoiding Writer Starvation

Drop read locks before doing expensive work:

```rust
for _ in 0..10 {
    std::thread::spawn(|| {
        let read_lock = SHARED.read().unwrap();
        println!("The value of SHARED is {}", read_lock.0);
        std::mem::drop(read_lock);  // Release before sleeping
        std::thread::sleep(std::time::Duration::from_secs(5));
    });
}
```

## Lock Best Practices

1. **Keep locks as short as possible** — minimize the time any lock is held.
2. **Build outside the lock** — if you need to perform a large computation, build the result first, then acquire the lock to move it in.
3. **Prefer scoped locking** — use interior braces to limit lock scope naturally.
4. **Use `RwLock` for read-heavy workloads** — multiple readers don't block each other.
5. **Use `Mutex` for write-heavy or mixed workloads** — simpler semantics, no writer starvation risk.

## When to Use Each

- **Mutex**: Multiple threads need to write to a shared collection concurrently
- **Per-thread results (JoinHandle)**: Each thread produces independent results that can be merged after joining
- **Atomic**: Simple counters or flags (see Atomic Operations article)
- **RwLock**: Read-heavy workloads where reads significantly outnumber writes

## parking_lot: A Lighter Alternative

The `parking_lot` crate provides drop-in replacements for `Mutex` and `RwLock` that eliminate the `.unwrap()` boilerplate:

```rust
use parking_lot::{Mutex, RwLock};

static SHARED: Mutex<usize> = Mutex::new(5);

fn main() {
    // No .unwrap() needed — parking_lot locks can't be poisoned
    let mut lock = SHARED.lock();
    println!("{}", *lock);
}
```

Key differences:
- **No `.unwrap()`**: `parking_lot` locks don't return `Result` and can't be poisoned, eliminating error handling boilerplate.
- **Performance**: On some platforms (Windows), `parking_lot` is faster than the standard library.
- **Otherwise drop-in**: The API is functionally similar to `std::sync::Mutex` / `RwLock`.

## See Also

- [Rust Atomic Operations](rust-atomic-operations.md) — lock-free counters
- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — thread spawning basics
- [Rust RAII](rust-raii.md) — how MutexGuard uses Drop for automatic unlock
- [Rust Channels](rust-channels.md) — alternative concurrency model
- [Rust Constants](rust-constants.md) — static variables with Mutex/RwLock for global state
