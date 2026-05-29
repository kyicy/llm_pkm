# Channels

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Communicating between async tasks or threads is accomplished with *channels*.

## Tokio mpsc Channels

`mpsc` = "Multi-producer, single consumer". Many senders, one receiver.

```rust
use tokio::sync::mpsc;

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let (tx, mut rx) = mpsc::channel(32); // 32 = buffer size

    spawn(rpc_server());
    spawn(rpc_client(rx));

    for _ in 0..10 {
        sleep(Duration::from_secs(1)).await;
        let _ = tx.send(1).await;
    }
    let _ = tx.send(2).await;

    Ok(())
}
```

Receiving in the client:

```rust
async fn rpc_client(mut rx: Receiver<u32>) -> anyhow::Result<()> {
    let mut stream = TcpStream::connect("127.0.0.1:8123").await?;

    while let Some(n) = rx.recv().await {
        let message = serde_json::to_vec(&Request::Ping)?;
        stream.write_all(&message).await?;

        let mut buf = vec![0; 1024];
        let n = stream.read(&mut buf).await?;
        let response: Response = serde_json::from_slice(&buf[0..n])?;
        match response {
            Response::Error => println!("Error!"),
            Response::Ack => println!("Ack"),
        }
    }
    Ok(())
}
```

## Tokio Broadcast Channels

Broadcast sends to all subscribers:

```rust
let (tx, _rx) = tokio::sync::broadcast::channel::<u32>(32);
spawn(rpc_server());
for _ in 0..10 {
    spawn(rpc_client(tx.subscribe()));
}

for _ in 0..10 {
    sleep(Duration::from_secs(1)).await;
    let _ = tx.send(1);
}
```

## Standard Library Channels (std::sync::mpsc)

You don't need Tokio for channels — the standard library provides them too:

```rust
use std::{sync::mpsc, thread};

fn main() {
    let (tx, rx) = mpsc::channel::<i32>();

    let handle = thread::spawn(move || {
        loop {
            let n = rx.recv().unwrap();
            match n {
                1 => println!("Hi from worker thread"),
                _ => break,
            }
        }
        println!("Thread closing cleanly");
    });

    for _ in 0..10 {
        tx.send(1).unwrap();
    }
    tx.send(0).unwrap();

    handle.join().unwrap();
}
```

There is no `broadcast` type in the standard library. The `crossbeam` crate provides high-quality channels.
