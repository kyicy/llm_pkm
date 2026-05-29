# Hello Library

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Now that we have a workspace, let's add a second project to it. This time, we're going to create a *library*.

**Terminology Time**

* A `library` is a generic term for shared code.
* A `crate` is a Cargo-managed bundle of code, often a library.
* A `module` is a section inside a crate.

## Create a new library

Go to your workspace root and run:

```
cargo new --lib authentication
```

Once again, you'll get a warning that really means *don't forget to update your workspace members*.

```toml
members = [
    "login", # Test login program
    "authentication", # Authenticator library
]
```

Cargo has created a `lib.rs` file instead of a `main.rs` file. This makes the package a *library* — you can't run it, it's designed to be used from other applications:

```rust
pub fn add(left: usize, right: usize) -> usize {
    left + right
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        let result = add(2, 2);
        assert_eq!(result, 4);
    }
}
```

## Understanding Rust Function Syntax

```rust
//     ⬇️ The function name
//          ⬇️ Function parameters
//                                    ⬇️ The function return type
//⬇️ `pub` means "public" - the function is available from outside the library/module.
pub fn add(left: usize, right: usize) -> usize {
    left + right // No "return" statement is necessary. Rust functions return the last
                 // expression result from a function.
}
```

If you prefer `return`, this is also valid:

```rust
pub fn add(left: usize, right: usize) -> usize {
    return left + right;
}
```

Clippy complains when you use `return` unnecessarily. Canonical Rust uses the short form.

## Understanding the Tests

```rust
#[cfg(test)]
```

This is a *compiler directive*. It tells Cargo to *only* compile the next section if you are compiling in the "test" configuration.

```rust
mod tests {
    use super::*;
    ..
}
```

`mod tests` declares a *module*. Modules serve as a namespace, a scope, and often a compilation unit. You draw elements from other modules into the current one with `use`. `use super::*` means "use everything from the parent module."

```rust
#[test]
fn it_works() {
    let result = add(2, 2);
    assert_eq!(result, 4);
}
```

Annotating a function as a `test` adds it to Cargo's unit-test runner. `assert_eq!` is an assertion macro that panics if the two arguments are not equal.

## Run the Tests

Run unit tests with:

```
cargo test
```

You can also test your whole workspace at once:

```
cargo test --all
```

## The Hello World Service

### Step 1: Cleanup the Default Code

Delete the `add` function, and the unit test (keeping the framework).

### Step 2: Add a function

```rust
pub fn greet_user(name: &str) -> String {
    format!("Hello {name}")
}
```

Things to notice:

* We made the function *public* with `pub`.
* Rust has TWO types of string:
    * `&str` is an immutable buffer of characters in memory.
    * `String` is a buffered string designed for modification.
* `format!` is another macro, used under the hood by `println!` and other formatters.

### Step 3: Test the New Function

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_greet_user() {
        assert_eq!("Hello Herbert", greet_user("Herbert"));
    }
}
```

Run with `cargo test`.

### Step 4: Integration

Return to the `login` project. Open `Cargo.toml`, and add our project as a dependency:

```toml
[dependencies]
authentication = { path = "../authentication" }
```

> You can specify version numbers (e.g. `library = "1"`). Provide as many significant numbers as you need. You can also use `{ git = "git path" }` and load directly from a shared Git repository.

Update `main.rs`:

```rust
use authentication::greet_user;

fn main() {
    println!("{}", greet_user("Herbert"));
}
```

Run it with `cargo run`.
