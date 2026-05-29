# Rust Constants

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [constants.md](../../raw/rust/2026-05-29-constants.md); [ardan-constants.md](../../raw/rust/ardan-constants.md); [ardan-globals.md](../../raw/rust/ardan-globals.md)

## Overview

Rust provides two keywords for declaring named constants in any scope, including globally: `const` for immutable values and `static` for variables with a `'static` lifetime. Both require explicit type annotations.

## `const` vs `static`

| Property | `const` | `static` |
|----------|---------|----------|
| Mutability | Always immutable | Can be mutable (requires `mut`) |
| Lifetime | Inlined at use site | Fixed memory address, `'static` lifetime |
| Safety | Always safe | Accessing/mutating a mutable static is `unsafe` |

```rust
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    n > THRESHOLD    // const accessible in any scope
}

fn main() {
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
}
```

## Key Rules

- **Global scope**: Both `const` and `static` can be declared outside functions.
- **Explicit types required**: Unlike `let` bindings, type annotations are mandatory.
- **`const` is immutable**: Attempting to reassign a `const` is a compile error.
- **Mutable `static` is `unsafe`**: Reading or writing a `static mut` requires an `unsafe` block, since data races are possible.

## `const fn`: Compile-Time Functions

Use the `const` keyword on functions to evaluate them at compile time:

```rust
const fn add(a: usize, b: usize) -> usize {
    a + b
}

const A: usize = add(4, 6);  // Evaluated at compile time

fn main() {
    println!("{A}");  // 10
}
```

Constant functions can also be used with dynamic (runtime) inputs — they behave like regular functions when called with non-constant arguments.

### `while` Loops in Const Contexts

Mutable variables and `while` loops are allowed in `const fn`:

```rust
const fn loopy() -> usize {
    let mut n = 1;
    let mut i = 0;
    while i < 20 {
        n += i;
        i += 1;
    }
    n
}
```

`for` loops and iterators are **not** allowed in `const fn` — the `Iterator` trait is inherently not constant.

### `const fn` Limitations

- **No floating point operations**: `const n: f32 = 1.0` is fine as a direct constant, but `const fn` using floats won't work.
- **No iterators**: No `for` loops or iterator methods.
- **No external data sources**: Cannot read files or connect to networks at compile time (except via `include_str!` / `include_bytes!` macros).

## Compile-Dependent Constants with `#[cfg]`

Adjust constants based on the compilation environment:

```rust
#[cfg(debug)]
const A: usize = 3;

#[cfg(release)]
const A: usize = 4;
```

Gate by target OS:

```rust
#[cfg(target_family = "unix")]
const A: usize = 3;
#[cfg(not(target_family = "unix"))]
const A: usize = 4;
```

## Embedding Files at Compile Time

Use `include_str!` and `include_bytes!` to embed file contents into the binary:

```rust
const HELP_TEXT: &str = include_str!("help.txt");
const ICON_DATA: &[u8] = include_bytes!("icon.png");
```

## Global Variables with Interior Mutability

Rust does not support simple `let` globals. For mutable global state, use safe interior mutability patterns.

### Atomic Primitives

Atomic types have constant constructors and can be used as safe static globals:

```rust
use std::sync::atomic::AtomicUsize;
use std::sync::atomic::Ordering;

static SHARED: AtomicUsize = AtomicUsize::new(5);

fn main() {
    println!("{}", SHARED.load(Ordering::Relaxed));
}
```

### Mutex for Global State

`Mutex<T>` has a constant constructor for wrappable types:

```rust
use std::sync::Mutex;

static SHARED: Mutex<usize> = Mutex::new(5);

fn main() {
    println!("{}", *SHARED.lock().unwrap());
}
```

### Lazy Singletons with `once_cell`

When a constructor isn't constant, use `once_cell::sync::Lazy` for lazy initialization:

```rust
use std::sync::Mutex;
use once_cell::sync::Lazy;

struct MyType(usize);

impl MyType {
    fn new(n: usize) -> Self {
        Self(n)
    }
}

static SHARED: Lazy<Mutex<MyType>> = Lazy::new(|| Mutex::new(MyType::new(5)));

fn main() {
    println!("{}", SHARED.lock().unwrap().0);
}
```

`Lazy` initializes the value the first time it is accessed. It wraps the initialization in a closure, so you can use runtime expressions.

> **Drop is not guaranteed for globals**: Destructors (`Drop`) are not guaranteed to run for global/static types.

```rust
impl Drop for MyType {
    fn drop(&mut self) {
        println!("Drop");  // Will NOT print
    }
}
```

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust Primitives](rust-primitives.md) — the scalar types used as constant values
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — Mutex, RwLock, and lock best practices
- [Rust Atomic Operations](rust-atomic-operations.md) — atomics as safe shared globals
- [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md) — `#[cfg(feature = "...")]` conditional compilation via feature flags
