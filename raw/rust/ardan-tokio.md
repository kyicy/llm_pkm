# Async and Tokio

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

For CPU-bound problems, Rayon is great. For I/O-bound problems (waiting on files, network, external services), Rust supports async/await — "green threading."

## Green Threads vs OS Threads

| Thread | Green-Thread |
|--------|-------------|
| Managed by the OS scheduler | Managed by your async runtime |
| Expensive to create | Cheap to create |
| Keep running while others are busy | Depend on the runtime to remain active |
| Always separated | May or may not be in a thread |

## Setup

```
cargo add tokio -F full
cargo add anyhow
```

## Hello Tokio

```rust
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    println!("Hello, world!");
    Ok(())
}
```

* `#[tokio::main]` is a macro that wraps main to initialize the Tokio async system.
* `async fn` returns a `Future`. It hasn't run yet — it's given you a handle to potentially run later.
* Use `.await` to run a future: `hello(1).await;`

## Joining Multiple Futures

```rust
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    join!(
        hello(1), hello(2), hello(3), hello(4)
    );
    Ok(())
}
```

## Spawning Tasks

Fire off a task without waiting:

```rust
async fn hello(n: u32) {
    println!("Hello {n}");
    if n < 10 {
        spawn(hello_child(n*10));
    }
}
```

## Blocking

Tokio is cooperatively managed. Using `std::thread::sleep` blocks the entire runtime:

```rust
// DON'T: blocks the Tokio runtime
async fn hello_child(n: u32) {
    std::thread::sleep(Duration::from_secs(1));
}

// DO: use Tokio's async sleep
async fn hello_child(n: u32) {
    tokio::time::sleep(Duration::from_secs(1)).await;
}
```

For true blocking operations, use `spawn_blocking`:

```rust
let _ = spawn_blocking(|| std::thread::sleep(Duration::from_secs(1))).await;
```

## Key Rules

* You **can't** call an `async` function directly from a normal function.
* You **can** call a regular function from an `async` function.
* Futures aren't threads. If you have to block, let the runtime know — or you pause the world.
* Recursion in green-thread land is hard.
