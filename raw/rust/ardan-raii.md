# RAII: Resource Acquisition is Initialization

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

RAII means that resources are acquired during initialization and released automatically when the object goes out of scope. In Rust, this is implemented with the `Drop` trait.

Basic example:

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
// "Destructing" is printed when x goes out of scope
```

Rust uses RAII for file descriptors, locks, network connections — they all close automatically when they leave scope.

## File Lock Example

```rust
use std::fs::remove_file;
use std::time::Duration;
use std::{path::Path, fs::File};
use std::io::Write;

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
        let path = Path::new("file.lock");
        remove_file(path).unwrap();
    }
}

fn main() {
    let _lock = FileLock::new();
    // Pretend to do something important
    std::thread::sleep(Duration::from_secs(30));
}
```

When `FileLock` is created, it acquires a lock file. When it is destroyed (goes out of scope), the lock is deleted.
