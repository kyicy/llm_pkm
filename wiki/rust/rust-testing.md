# Rust Testing

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [hello-world.md](../../raw/rust/hello-world.md); [ardan-hello-library.md](../../raw/rust/ardan-hello-library.md); [ardan-simple-login-test.md](../../raw/rust/ardan-simple-login-test.md); [ardan-documentation.md](../../raw/rust/ardan-documentation.md)

## Overview

Rust has a built-in testing framework. Tests are Rust functions annotated with `#[test]`, typically organized into a `tests` module. Cargo compiles and runs tests with `cargo test`, reporting which tests pass and which fail. Doc tests allow code examples in documentation to be run as tests.

## Test Structure

Tests live in a module annotated with `#[cfg(test)]`:

```rust
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

### `#[cfg(test)]`

This compiler directive tells Cargo to *only* compile the annotated module when compiling in test configuration. Unit tests don't take up any space in deployed builds.

### `mod tests`

Modules serve as namespaces, scopes, and compilation units. Everything inside `mod tests` is namespaced as `tests::name` and cannot pollute other modules.

### `use super::*`

This imports everything from the parent module into the test module's scope. Without this, you'd need to call `super::add(2, 2)`.

### `#[test]`

Annotating a function as `#[test]` registers it with Cargo's unit-test runner.

## Assertion Macros

### `assert_eq!`

Asserts that two values are equal:

```rust
assert_eq!(result, 4);
```

If the assertion fails, the test panics with a message showing both values.

### `assert!` and `assert!` with negation

For boolean conditions:

```rust
#[test]
fn test_case_and_trim() {
    assert!(is_login_allowed("HeRbErT"));   // assert true
    assert!(!is_login_allowed("bob"));       // assert false
}
```

## Running Tests

```bash
$ cargo test
```

Output:
```
running 3 tests
test tests::test_greet_user ... ok
test tests::test_login_fail ... ok
test tests::test_case_and_trim ... ok

test result: ok. 3 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s
```

Run tests for all workspace members:

```bash
$ cargo test --all
```

## Testing Library Functions

When testing a library function, the test module typically imports parent items with `use super::*`:

```rust
pub fn greet_user(name: &str) -> String {
    format!("Hello {name}")
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_greet_user() {
        assert_eq!("Hello Herbert", greet_user("Herbert"));
    }
}
```

## Doc Tests

Code examples in documentation comments are automatically run as tests:

```rust
/// ```
/// use my_lib::hash_password;
/// let hash = hash_password("test");
/// assert_eq!(hash.len(), 64);
/// ```
pub fn hash_password(password: &str) -> String {
    // ...
}
```

Run `cargo test` and the doc examples execute alongside unit tests. This ensures documentation stays synchronized with code.

## Benchmarking with `#[bench]` (Nightly)

Rust has built-in benchmark support on the nightly channel. Add the feature gate and import the test crate:

```rust
#![feature(test)]

extern crate test;

#[cfg(test)]
mod tests {
    use super::*;
    use test::Bencher;

    #[bench]
    fn bench_add(b: &mut Bencher) {
        b.iter(|| add(2, 4));
    }
}
```

Run with:

```bash
$ cargo +nightly bench
```

**Downside:** Requires the nightly toolchain. A common workaround is to comment out or cfg-gate benchmarks when not in use.

## Benchmarking with Criterion

For production-quality benchmarks on stable Rust, use [Criterion](https://github.com/bheisler/criterion.rs).

### Setup

In `Cargo.toml`:

```toml
[dev-dependencies]
criterion = { version = "0.4", features = [ "html_reports" ] }

[[bench]]
name = "my_benchmark"
harness = false
```

Create `benches/my_benchmark.rs`:

```rust
use criterion::{black_box, criterion_group, criterion_main, Criterion};

fn criterion_benchmark(c: &mut Criterion) {
    c.bench_function("fib 20", |b| b.iter(|| fibonacci(black_box(20))));
}

criterion_group!(benches, criterion_benchmark);
criterion_main!(benches);
```

Run with `cargo bench`. HTML reports with statistics are generated in `target/criterion/`.

## See Also

- [Rust Library Crates](rust-library-crates.md) — library crates include default test frameworks
- [Rust Cargo Workspaces](rust-cargo-workspaces.md) — running tests across workspace members
- [Rust Documentation](rust-documentation.md) — doc comments and doc tests
- [Rust Benchmarking](rust-benchmarking.md) — benchmarking approaches in detail
