# Rust Error Handling

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-errors.md](../../raw/rust/ardan-errors.md)

## Overview

Rust does not have exceptions. Errors are values represented by types implementing the standard `Error` trait. Functions that can fail return `Result<T, E>`, which forces callers to handle both success and failure cases.

## The `?` Operator

The `?` operator propagates errors to the caller, replacing `unwrap` in production code:

```rust
fn get_line_from_keyboard() -> Result<String, std::io::Error> {
    let mut input = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut input)?;  // returns error to caller if one occurs
    Ok(input.trim().to_string())
}
```

## Boxed Errors

When a function calls multiple fallible operations that return different error types, use `Box<dyn Error>`:

```rust
use std::error;
type Result<T> = std::result::Result<T, Box<dyn error::Error>>;

fn get_int_from_keyboard() -> Result<i32> {
    let text = get_line_from_keyboard()?;
    Ok(text.parse()?)  // parse() returns ParseIntError, but ? works with Box<dyn Error>
}
```

## Error Handling with Anyhow (Applications)

The `anyhow` crate simplifies error handling for application code:

```toml
[dependencies]
anyhow = "1"
```

```rust
use anyhow::Result;

fn main() -> Result<()> {
    let number = get_int_from_keyboard()?;
    println!("{number}");
    Ok(())
}
```

Anyhow's `Result` type works like `Box<dyn Error>` but adds:
- `root_cause()` for finding the underlying problem
- `Context` trait for attaching context to errors
- `downcast_ref::<T>()` for checking error types

**Use anyhow in applications when you don't need to handle specific error variants.**

## Custom Errors with thiserror (Libraries)

For libraries, `thiserror` provides ergonomic custom error types:

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

### Map Errors with `map_err`

Convert error types using `map_err`:

```rust
fn get_line_from_keyboard() -> Result<String, InputError> {
    let mut input = String::new();
    std::io::stdin()
        .read_line(&mut input)
        .map_err(|_| InputError::StdIn)?;
    Ok(input.trim().to_string())
}

fn get_int_from_keyboard() -> Result<i32, InputError> {
    let text = get_line_from_keyboard()?;
    text.trim()
        .parse()
        .map_err(|_| InputError::NotAnInteger)
}
```

### Matching Custom Errors

```rust
fn main() {
    loop {
        match get_int_from_keyboard() {
            Ok(n) => { println!("You entered {n}"); break; },
            Err(InputError::StdIn) => panic!("stdin unavailable"),
            Err(InputError::NotAnInteger) => println!("Please try again"),
        }
    }
}
```

## Comparison of Approaches

| Approach | Use Case | Granularity |
|----------|----------|-------------|
| `unwrap()` / `expect()` | Prototyping, infallible operations | No error handling |
| `Box<dyn Error>` | Quick aggregation of multiple error types | Low |
| `anyhow` | Application code, CLI tools | Low-Medium |
| `thiserror` | Library code, specific error variants | High |

## See Also

- [Rust Testing](rust-testing.md) — testing error paths
- [Rust Library Crates](rust-library-crates.md) — returning errors from libraries
