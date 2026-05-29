# Extending the Library

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

## Initial Yes/No Authentication

Let's go back to our `auth` project, and add a new function:

```rust
pub fn is_login_allowed(name: &str) -> bool {
    name.to_lowercase().trim() == "herbert"
}
```

Things to note:
* We're applying `to_lowercase()` to ensure that even "HeRbErT" is in lower case.
* We're calling `trim()` to remove any extraneous characters.
* We use short-form return.

Let's add unit tests:

```rust
#[test]
fn test_case_and_trim() {
    assert!(is_login_allowed("HeRbErT"));
    assert!(is_login_allowed("  herbert\r\n"));
}

#[test]
fn test_login_fail() {
    assert!(!is_login_allowed("bob"));
}
```

Test with `cargo test`.

## Implement Yes/No Login

Now update your `login` program `main.rs`:

```rust
use auth_if::is_login_allowed;

fn main() {
    println!("Welcome to the (Not Very) Secure Server");
    println!("Enter your username:");
    let mut input = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut input).unwrap();
    if is_login_allowed(&input) {
        println!("Welcome, {input}");
    } else {
        println!("Sorry, {input} is now allowed");
    }
}
```

What's new:

* `let mut input = String::new()` creates a new mutable string. Rust defaults to immutable variables.
* Obtaining `stdin` gets a link the operating system's `stdin` system.
* `read_line` reads a string. `unwrap` means "crash if an error occurs here".
* We're using an `if` statement to vary what happens for each possible branch.

Note: Reading from `stdin` includes `\r\n` (or `\n` on non-Windows) in your string. Use `trim()` to remove this.
