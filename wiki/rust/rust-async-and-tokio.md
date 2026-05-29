# Rust Async and Tokio

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-tokio.md](../../raw/rust/ardan-tokio.md)

## Overview

Rust's async/await model enables *cooperative multitasking* for I/O-bound workloads. Unlike OS threads, async tasks ("green threads") are lightweight and managed by a runtime. Tokio is the most popular async runtime in the Rust ecosystem.

## Green Threads vs OS Threads

| OS Thread | Green Thread (async) |
|-----------|---------------------|
| Managed by the OS scheduler | Managed by your async runtime |
| Expensive to create | Cheap to create |
| Keep running while others are busy | Yield cooperatively at `.await` points |
| Always separated | May share an OS thread |

## Setup

```toml
[dependencies]
tokio = { version = "1", features = ["full"] }
anyhow = "1"
```

## Hello Tokio

```rust
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    println!("Hello, world!");
    Ok(())
}
```

- `#[tokio::main]` initializes the Tokio runtime
- `async fn` returns a `Future` — it represents work to be done later
- `.await` runs a future to completion

## Working with Futures

### Awaiting a Single Future

```rust
async fn hello(n: u32) {
    println!("Hello {n}");
}

#[tokio::main]
async fn main() {
    hello(1).await;  // runs the future and waits for it
}
```

### Joining Multiple Futures

```rust
use tokio::join;

#[tokio::main]
async fn main() {
    join!(
        hello(1), hello(2), hello(3), hello(4)
    );
}
```

### Spawning Tasks (Fire-and-Forget)

```rust
use tokio::spawn;

async fn hello(n: u32) {
    println!("Hello {n}");
    if n < 10 {
        spawn(hello_child(n * 10));
    }
}
```

## Blocking

Tokio's default scheduler is cooperative. Using `std::thread::sleep` blocks the **entire runtime**:

```rust
// DON'T: blocks the Tokio runtime, pausing all tasks
async fn bad() {
    std::thread::sleep(Duration::from_secs(1));
}

// DO: Tokio's async sleep yields to other tasks
async fn good() {
    tokio::time::sleep(Duration::from_secs(1)).await;
}
```

For truly blocking operations:

```rust
let result = tokio::task::spawn_blocking(|| {
    std::thread::sleep(Duration::from_secs(1));
    compute_something_heavy()
}).await.unwrap();
```

## Key Rules

1. You **cannot** call an `async` function directly from a regular function — you need a runtime.
2. You **can** call a regular function from an `async` function.
3. Futures aren't threads — if you block, you may pause the entire runtime.
4. Recursion in async is complex — avoid deeply recursive async functions.

## Green Thread Batching

Tokio green threads (spawned tasks) have overhead. Benchmarking a TCP login service reveals a consistent pattern:

1. **First request per green-thread is slow** (~3000-4000 usecs)
2. **Subsequent requests in the same green-thread are fast** (~300-400 usecs)

This is because spawning a green thread involves setup overhead — Tokio's runtime needs to create task state, allocate space, and schedule the work.

**Lesson: batch your operations within green threads.** Instead of spawning a separate task per request, spawn fewer tasks that handle multiple requests each.

## TCP Connection Reuse

Creating a new TCP connection for each request is far more expensive than reusing an existing one:

```rust
struct LoginClient(TcpStream);

impl LoginClient {
    async fn login(&mut self, username: &str, password: &str) -> anyhow::Result<LoginAction> {
        // reuse self.0 for all requests
    }
}
```

| Pattern | Per-request latency |
|---------|-------------------|
| New connection per request | ~400 usecs |
| Reused connection (`LoginClient`) | ~50 usecs |

The connection establishment handshake dominates network latency for short-lived requests.

## Concurrent Connection Limits

TCP is not unlimited. In benchmarks:
- **1,000 concurrent connections**: Manageable, with some variance (worst case ~20ms)
- **100,000 concurrent connections**: Fails — the server can't keep up (`ConnectionRefused`)
- TCP port limit (65,535) creates a hard ceiling for outbound connections

For high-throughput microservice architectures, prefer **connection pooling** and **connection reuse** over creating new connections per request.

## See Also

- [Rust Channels](rust-channels.md) — async channel communication
- [Rust TCP Server](rust-tcp-server.md) — building async network services
- [Rust Rayon](rust-rayon.md) — alternative for CPU-bound parallelism
- [Rust Threads and Concurrency](rust-threads-and-concurrency.md) — OS threads vs async
- [Rust Benchmarking](rust-benchmarking.md) — measuring async network latency
