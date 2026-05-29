# Rust RAII (Resource Acquisition Is Initialization)

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-raii.md](../../raw/rust/ardan-raii.md)

## Overview

RAII is a pattern where resources are acquired during initialization and released automatically when the object goes out of scope. In Rust, this is implemented with the `Drop` trait. Unlike destructors in garbage-collected languages, Rust's `Drop` is guaranteed to run (except during panics).

## The Drop Trait

```rust
struct Droppable;

impl Drop for Droppable {
    fn drop(&mut self) {
        println!("Destructing")
    }
}

fn main() {
    let x = Droppable;
}
// "Destructing" printed when x goes out of scope
```

## Standard Library RAII

Rust's standard library uses RAII extensively:

- **File handles**: Automatically close when `File` leaves scope
- **Mutex locks**: Automatically released when the `MutexGuard` leaves scope
- **Network connections**: Automatically closed when `TcpStream` leaves scope
- **Memory**: Automatically freed when `Box`, `Vec`, `String`, etc. leave scope

## Custom RAII Example: File Lock

```rust
use std::fs::{remove_file, File};
use std::io::Write;
use std::path::Path;

struct FileLock;

impl FileLock {
    fn new() -> Self {
        let path = Path::new("file.lock");
        if path.exists() {
            panic!("You can't run this program more than once");
        }
        let mut output = File::create(path).unwrap();
        write!(output, "locked").unwrap();
        Self
    }
}

impl Drop for FileLock {
    fn drop(&mut self) {
        let _ = remove_file("file.lock");
    }
}

fn main() {
    let _lock = FileLock::new();  // creates file.lock
    std::thread::sleep(Duration::from_secs(30));
}  // file.lock is automatically removed when _lock drops
```

## Best Practices

- Whenever you acquire a finite resource, implement `Drop` to guarantee release.
- Combine reference counting with `Drop` for shared resource management.
- Files, network connections, mutex guards — all should use RAII.

## See Also

- [Rust Lifetimes](rust-lifetimes.md) — lifetime guarantees for references
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — Mutex uses RAII for lock management
