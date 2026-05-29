# Rust Channels

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-channels.md](../../raw/rust/ardan-channels.md)

## Overview

Channels provide a way to communicate between threads or async tasks by sending messages. Rust offers both standard library channels (`std::sync::mpsc`) and Tokio's async channels (`tokio::sync::mpsc`, `tokio::sync::broadcast`).

## Standard Library Channels (std::sync::mpsc)

`mpsc` = "Multi-producer, single consumer" — many senders, one receiver:

```rust
use std::{sync::mpsc, thread};

let (tx, rx) = mpsc::channel::<i32>();

thread::spawn(move || {
    loop {
        match rx.recv().unwrap() {
            1 => println!("Working..."),
            _ => break,
        }
    }
});

tx.send(1).unwrap();
tx.send(1).unwrap();
tx.send(0).unwrap();  // signal the thread to stop
```

## Tokio Async Channels

### mpsc (Multi-Producer, Single Consumer)

```rust
use tokio::sync::mpsc;

#[tokio::main]
async fn main() {
    let (tx, mut rx) = mpsc::channel(32);  // buffer size of 32

    tokio::spawn(async move {
        while let Some(msg) = rx.recv().await {
            println!("Got: {msg}");
        }
    });

    tx.send(42).await.unwrap();
}
```

### Broadcast (Many Producers, Many Consumers)

```rust
use tokio::sync::broadcast;

#[tokio::main]
async fn main() {
    let (tx, _rx) = broadcast::channel::<u32>(32);

    for _ in 0..10 {
        let rx = tx.subscribe();
        tokio::spawn(consumer(rx));
    }

    tx.send(1).unwrap();  // all 10 consumers receive this
}
```

## Channel Types Summary

| Channel | Crate | Producers | Consumers | Use Case |
|---------|-------|-----------|-----------|----------|
| `std::sync::mpsc` | std | Many | One | Thread communication |
| `tokio::sync::mpsc` | tokio | Many | One | Async task communication |
| `tokio::sync::broadcast` | tokio | Many | Many | Fan-out to subscribers |

## See Also

- [Rust Async and Tokio](rust-async-and-tokio.md) — Tokio runtime basics
- [Rust TCP Server](rust-tcp-server.md) — using channels with async TCP
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — alternative concurrency approach
