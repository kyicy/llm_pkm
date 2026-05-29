# Rust DashMap

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-dashmap.md](../../raw/rust/ardan-dashmap.md)

## Overview

`DashMap<K, V>` is a lock-free concurrent hash map that provides safe concurrent access from multiple threads without explicit `Mutex` or `RwLock` wrapping. It uses atomics internally to manage concurrent reads and writes.

## Basic Usage

```rust
use dashmap::DashMap;
use once_cell::sync::Lazy;
use std::{thread, time::Duration};

static MAP: Lazy<DashMap<usize, usize>> = Lazy::new(DashMap::new);

fn main() {
    let mut threads = Vec::new();

    // Adder Threads
    for i in 0..10 {
        threads.push(thread::spawn(move || {
            for _ in 0..100 {
                if let Some(mut count) = MAP.get_mut(&i) {
                    *count += 1;
                } else {
                    MAP.insert(i, 1);
                }
                std::thread::sleep(Duration::from_secs_f32(0.1));
            }
        }));
    }

    // Reader Threads
    for i in 0..10 {
        threads.push(thread::spawn(move || {
            for _ in 0..20 {
                if let Some(count) = MAP.get(&i) {
                    println!("Count of {i}: {}", *count);
                }
                std::thread::sleep(Duration::from_secs_f32(0.5));
            }
        }));
    }

    for t in threads {
        let _ = t.join();
    }
}
```

## Key Operations

| Operation | Method | Description |
|-----------|--------|-------------|
| Read | `.get(&key)` | Returns `Option<Ref<K, V>>` |
| Write | `.insert(&key, value)` | Inserts or replaces |
| Mutate | `.get_mut(&key)` | Returns `Option<RefMut<K, V>>` for in-place mutation |
| Remove | `.remove(&key)` | Removes and returns value |

## Concurrent Readers and Writers

DashMap allows simultaneous readers and writers without a single global lock. Writer threads can add/update entries while reader threads iterate the map. This is achieved through sharding — DashMap internally uses multiple shards, each with its own lock, reducing contention.

## Trade-offs

**Going lock-free is not free.** Lock-free structures are generally a little slower than a well-designed `Mutex<HashMap>` for simple workloads. The advantage is in *complexity reduction* — when you have many concurrent readers and writers, DashMap eliminates the orchestration burden of manual locking.

### DashMap vs Mutex<HashMap>

| Aspect | `DashMap` | `Mutex<HashMap>` |
|--------|-----------|------------------|
| Concurrency | Readers and writers can proceed simultaneously | Only one thread at a time |
| API complexity | Simple — no lock management | Must `.lock().unwrap()` each access |
| Raw throughput | Slightly slower per operation | Slightly faster per operation |
| Contention | Reduced via sharding | All-or-nothing lock |

## Lazy Singleton Pattern

Combine `DashMap` with `once_cell::sync::Lazy` to create a global concurrent map:

```rust
use dashmap::DashMap;
use once_cell::sync::Lazy;

static MAP: Lazy<DashMap<KeyType, ValueType>> = Lazy::new(DashMap::new);
```

## When to Use

- Many threads concurrently reading and writing to the same map
- Complexity of manual `Mutex` management outweighs performance concerns
- Need sharded concurrency without manual lock orchestration
- Read-heavy workloads with occasional writes

## See Also

- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — alternative locking-based concurrency
- [Rust Atomic Operations](rust-atomic-operations.md) — lock-free atomics for simpler state
- [Rust Constants](rust-constants.md) — `Lazy` singleton pattern for globals
