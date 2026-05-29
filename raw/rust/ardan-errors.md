# Error Handling

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

So far, we've largely ignored errors. Whenever something might return an error, we've called `unwrap` or the slightly better `expect`. Both are the nuclear option: crash the whole program.

* `unwrap` crashes with only a stack trace.
* `expect("message")` crashes with the error message and a stack trace.

## Returning Results

Change functions to return `Result` types:

```rust
fn get_line_from_keyboard() -> Result<String, std::io::Error> {
    let mut input = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut input)?;  // ? propagates the error
    let trimmed = input.trim();
    Ok(trimmed.to_string())
}
```

The `?` operator replaces `unwrap` — it returns the error to the caller if one occurs.

## Boxed Errors for Multiple Error Types

When calling functions that return different error types, use a boxed error:

```rust
use std::error;
type Result<T> = std::result::Result<T, Box<dyn error::Error>>;

fn get_line_from_keyboard() -> Result<String> {
    let mut input = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut input)?;
    let trimmed = input.trim();
    Ok(trimmed.to_string())
}

fn get_int_from_keyboard() -> Result<i32> {
    let text = get_line_from_keyboard()?;
    Ok(text.parse()?)  // parse() returns a different error type, but ? works with Box<dyn Error>
}
```

### Matching on Boxed Errors

```rust
match number {
    Ok(n) => { println!("You entered {n}"); break; },
    Err(e) => println!("Error: {e:?}"),
}
```

## Consuming Errors with Anyhow

The `anyhow` crate simplifies error handling for applications:

```toml
[dependencies]
anyhow = "1"
```

```rust
use anyhow::Result;

fn get_line_from_keyboard() -> Result<String> { ... }

fn get_int_from_keyboard() -> Result<i32> { ... }

fn main() {
    loop {
        println!("Enter an integer:");
        let number = get_int_from_keyboard();
        match number {
            Ok(n) => { println!("You entered {n}"); break; },
            Err(e) => {
                if let Some(std::io::Error { .. }) = e.downcast_ref::<std::io::Error>() {
                    panic!("stdin is unavailable");
                } else {
                    println!("Try again - that wasn't an integer");
                }
            }
        }
    }
}
```

**Use anyhow in client programs when you aren't too worried about exactly what went wrong.**

## Creating Better Errors with thiserror

For libraries, use `thiserror` to define specific error types:

```toml
[dependencies]
thiserror = "1"
```

```rust
use thiserror::Error;

#[derive(Error, Debug)]
enum InputError {
    #[error("Standard input is unavailable")]
    StdIn,

    #[error("Cannot parse integer from text")]
    NotAnInteger,
}
```

### Using Custom Errors

```rust
fn get_line_from_keyboard() -> Result<String, InputError> {
    let mut input = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut input).map_err(|_| InputError::StdIn)?;
    let trimmed = input.trim();
    Ok(trimmed.to_string())
}

fn get_int_from_keyboard() -> Result<i32, InputError> {
    let text = get_line_from_keyboard()?;
    text.trim().parse().map_err(|_| InputError::NotAnInteger)
}
```

### Matching Custom Errors

```rust
fn main() {
    loop {
        println!("Enter an integer:");
        let number = get_int_from_keyboard();
        match number {
            Ok(n) => { println!("You entered {n}"); break; },
            Err(InputError::StdIn) => panic!("Input doesn't work"),
            Err(InputError::NotAnInteger) => println!("Please try again"),
        }
    }
}
```

**Errors are not exceptions.** They are values to handle explicitly.
