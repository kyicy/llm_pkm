# Rust Rocket Web Framework

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-rocket.md](../../raw/rust/ardan-rocket.md)

## Overview

Rocket is a simple, fast web framework for Rust. It uses attribute macros for routing and has built-in support for JSON, static files, and async operations via Tokio.

## Hello Web

```toml
[dependencies]
rocket = "0.5.0-rc.2"
```

Minimal Rocket app:

```rust
#[macro_use] extern crate rocket;

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

#[launch]
fn rocket() -> _ {
    rocket::build().mount("/", routes![index])
}
```

Run with `cargo run` and visit `http://127.0.0.1:8000`.

Key points:
- `#[get("/")]` — attribute macro that registers an HTTP GET handler
- `routes![...]` — macro that collects route handlers into a list
- `#[launch]` — macro that creates the `main` function entry point
- `rocket::build().mount(...)` — mounts routes at a given base path

## Static File Serving

Use `NamedFile` to serve files:

```rust
#[macro_use] extern crate rocket;
use rocket::fs::NamedFile;

#[get("/")]
pub async fn login_page() -> NamedFile {
    NamedFile::open("login.html").await.unwrap()
}

#[launch]
fn rocket() -> _ {
    rocket::build().mount("/", routes![login_page])
}
```

## JSON Endpoints

Rocket includes its own Serde integration for JSON handling:

```rust
use rocket::serde::{json::Json, Deserialize, Serialize};

#[derive(Serialize, Deserialize, Clone, Debug)]
#[serde(crate = "rocket::serde")]
struct Login {
    username: String,
    password: String,
}

#[post("/api/login", data = "<user>")]
pub fn login(user: Json<Login>) {
    println!("{user:?}");
}
```

The `#[serde(crate = "rocket::serde")]` attribute tells Serde to use Rocket's bundled Serde rather than the standalone version.

## Microservice Integration

Rocket can act as a front-end to TCP-based services. Since Rocket includes Tokio, you can use it for TCP connections:

```toml
bincode = "1"
authentication = { path = "../authentication" }
```

```rust
#[post("/api/login", data = "<user>")]
pub async fn login(user: Json<Login>) {
    use rocket::tokio::io::{AsyncWriteExt, AsyncReadExt};
    use rocket::tokio::net::TcpStream;

    let login_attempt = user.0;

    let mut stream = TcpStream::connect("127.0.0.1:8123").await.unwrap();
    let message = bincode::serialize(&login_attempt).unwrap();
    stream.write_all(&message).await.unwrap();

    let mut buf = vec![0; 1024];
    let n = stream.read(&mut buf).await.unwrap();
    let response: Option<LoginAction> = bincode::deserialize(&buf[0..n]).unwrap();

    println!("{response:?}");
}
```

This pattern implements a miniature micro-service architecture:
1. User-facing Rocket web server receives JSON from the browser
2. Encodes it with bincode binary serialization
3. Sends it to a TCP backend service
4. Receives and processes the response

## See Also

- [Rust Macros](rust-macros.md) — `#[get]`, `#[post]`, and `routes!` are declarative macros
- [Rust TCP Server](rust-tcp-server.md) — building the TCP backend service
- [Rust Async and Tokio](rust-async-and-tokio.md) — Rocket's async runtime
- [Rust Serde Serialization](rust-serde-serialization.md) — JSON and bincode serialization
