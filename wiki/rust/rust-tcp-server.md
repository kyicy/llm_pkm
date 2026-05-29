# Rust TCP Server

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-tcp-server.md](../../raw/rust/ardan-tcp-server.md)

## Overview

Tokio provides async TCP networking primitives — `TcpListener` for accepting connections and `TcpStream` for sending/receiving data. Combined with `serde`, you can build RPC-style servers in very few lines of code.

## Basic TCP Echo Server

```rust
use tokio::net::TcpListener;
use tokio::spawn;

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let listener = TcpListener::bind("127.0.0.1:8123").await?;

    loop {
        let (mut socket, _addr) = listener.accept().await?;
        spawn(async move {
            let mut buf = vec![0; 1024];
            loop {
                let n = socket.read(&mut buf).await
                    .expect("failed to read");
                if n == 0 { return; }
                socket.write_all(&buf[0..n]).await
                    .expect("failed to write");
            }
        });
    }
}
```

Key patterns:
- `TcpListener::bind()` binds to an address
- `listener.accept()` waits for connections asynchronously
- Each connection is handled in a spawned green-thread
- `socket.read()` reads data into a buffer
- `socket.write_all()` sends data back

## RPC Server with Serde

```rust
use serde::{Serialize, Deserialize};
use tokio::net::TcpListener;

#[derive(Serialize, Deserialize)]
enum Request { Ping }

#[derive(Serialize, Deserialize)]
enum Response { Error, Ack }

async fn rpc_server() -> anyhow::Result<()> {
    let listener = TcpListener::bind("127.0.0.1:8123").await?;

    loop {
        let (mut socket, _) = listener.accept().await?;
        tokio::spawn(async move {
            let mut buf = vec![0; 1024];
            loop {
                let n = socket.read(&mut buf).await.expect("read");
                if n == 0 { return; }

                let response = match serde_json::from_slice(&buf[0..n]) {
                    Ok(Request::Ping) => Response::Ack,
                    Err(_) => Response::Error,
                };

                let bytes = serde_json::to_vec(&response).unwrap();
                socket.write_all(&bytes).await.expect("write");
            }
        });
    }
}
```

## RPC Client

```rust
use tokio::net::TcpStream;

async fn rpc_client() -> anyhow::Result<()> {
    let mut stream = TcpStream::connect("127.0.0.1:8123").await?;
    let msg = serde_json::to_vec(&Request::Ping)?;
    stream.write_all(&msg).await?;

    let mut buf = vec![0; 1024];
    let n = stream.read(&mut buf).await?;
    let response: Response = serde_json::from_slice(&buf[0..n])?;
    println!("{:?}", response);
    Ok(())
}
```

## Running the Application

Use `std::env::args()` to choose between server and client mode:

```rust
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let args: Vec<String> = std::env::args().collect();
    match args.get(1).map(String::as_str) {
        Some("--server") => rpc_server().await,
        Some("--client") => rpc_client().await,
        _ => println!("Usage: --server or --client"),
    }
}
```

Run in two terminals:
```
$ cargo run -- --server
$ cargo run -- --client
Ack
```

## Login Server with Bincode

Bincode is a binary encoding format that packs data more tightly than JSON. Combined with the RPC pattern, you can build a full login server.

### Dependencies

```toml
[dependencies]
anyhow = "1"
serde = { version = "1", features = ["derive"] }
tokio = { version = "1", features = ["full"] }
bincode = "1"
authentication = { path = "../authentication" }
once_cell = "1"
parking_lot = "0"
```

### Global User Store

Use `Lazy<RwLock<HashMap>>` for a global user database:

```rust
use once_cell::sync::Lazy;
use parking_lot::RwLock;

static USERS: Lazy<RwLock<HashMap<String, User>>> = Lazy::new(|| RwLock::new(get_users()));
```

### Login Request Type

```rust
#[derive(Serialize, Deserialize)]
struct LoginRequest {
    username: String,
    password: String,
}
```

### Server Handler

```rust
let mut response = None;
if let Ok(request) = bincode::deserialize::<LoginRequest>(&buf[0..n]) {
    response = login(&USERS.read(), &request.username, &request.password);
}

let bytes = bincode::serialize(&response).unwrap();
socket.write_all(&bytes).await.expect("failed to write");
```

### Client with Bincode

```rust
async fn rpc_client() -> anyhow::Result<()> {
    let mut stream = TcpStream::connect("127.0.0.1:8123").await?;
    let message = bincode::serialize(&login_attempt)?;
    stream.write_all(&message).await?;

    let mut buf = vec![0; 1024];
    let n = stream.read(&mut buf).await?;
    let response: Option<LoginAction> = bincode::deserialize(&buf[0..n])?;
    // handle response...
    Ok(())
}
```

### LoginClient: Connection Reuse

Creating a TCP connection is expensive. Reuse established connections with a wrapper struct:

```rust
struct LoginClient(TcpStream);

impl LoginClient {
    async fn new() -> Self {
        let stream = TcpStream::connect("127.0.0.1:8123").await.unwrap();
        Self(stream)
    }

    async fn login(&mut self, username: &str, password: &str) -> anyhow::Result<LoginAction> {
        let login_attempt = LoginRequest {
            username: username.to_string(),
            password: password.to_string(),
        };
        let message = bincode::serialize(&login_attempt)?;
        self.0.write_all(&message).await?;

        let mut buf = vec![0; 1024];
        let n = self.0.read(&mut buf).await?;
        let response: Option<LoginAction> = bincode::deserialize(&buf[0..n])?;
        // match response...
    }
}

async fn rpc_client() -> anyhow::Result<()> {
    let mut client = LoginClient::new().await;
    let result = client.login("herbert", "password").await?;
    println!("{result:?}");
    Ok(())
}
```

Connection reuse drops request times from ~400us to ~50us in benchmarks.

## See Also

- [Rust Async and Tokio](rust-async-and-tokio.md) — async/await fundamentals
- [Rust Channels](rust-channels.md) — async communication between tasks
- [Rust Serde Serialization](rust-serde-serialization.md) — serializing messages over TCP
- [Rust Rocket Web Framework](rust-rocket-web.md) — web front-end to TCP services
- [Rust Benchmarking](rust-benchmarking.md) — measuring network service performance
