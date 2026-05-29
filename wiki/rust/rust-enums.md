# Rust Enums

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [enums.md](../../raw/rust/2026-05-29-enums.md); [enum-c-like.md](../../raw/rust/2026-05-29-enum-c-like.md); [enum-use.md](../../raw/rust/2026-05-29-enum-use.md); [ardan-enums.md](../../raw/rust/ardan-enums.md)

## Overview

The `enum` keyword creates a type that can be one of several distinct variants. Each variant can carry different kinds and amounts of data: unit-like (no data), tuple-like (positional data), or struct-like (named fields). Enums are typically consumed via `match` expressions that handle every variant. The compiler exhaustively checks match arms and warns about unhandled variants.

## Variant Kinds

Any variant form valid for a `struct` is also valid in an `enum`:

```rust
enum WebEvent {
    PageLoad,                       // unit-like
    PageUnload,                     // unit-like
    KeyPress(char),                 // tuple-like
    Paste(String),                  // tuple-like
    Click { x: i64, y: i64 },      // struct-like (named fields)
}

fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        WebEvent::Click { x, y } => println!("clicked at x={}, y={}.", x, y),
    }
}
```

Each variant is its own type — `PageLoad` and `PageUnload` are distinct despite both being unit-like.

## C-Like Enums

Enums can be used as C-style integer enumerations with implicit or explicit discriminators. Variants can be cast to integers with `as`:

```rust
// Implicit discriminator (starts at 0)
enum Number { Zero, One, Two }

// Explicit discriminator
enum Color { Red = 0xff0000, Green = 0x00ff00, Blue = 0x0000ff }

println!("zero is {}", Number::Zero as i32);       // "zero is 0"
println!("roses are #{:06x}", Color::Red as u32);  // "roses are #ff0000"
```

## Deriving Traits

Enums don't implement equality or debug printing by default. Use `#[derive]`:

```rust
#[derive(PartialEq, Debug)]
pub enum LoginAction {
    Admin,
    User,
    Denied,
}
```

`PartialEq` is a *trait* — an interface describing the capabilities of a type. `#[derive]` can automatically add many trait implementations.

## Enums with Data (Tuple-Like and Struct-Like)

Enum variants can carry data, making them similar to `union` types in other languages:

```rust
#[derive(PartialEq, Debug)]
pub enum Role { Admin, User, Limited }

#[derive(PartialEq, Debug)]
pub enum DeniedReason {
    PasswordExpired,
    AccountLocked { reason: String },
}

#[derive(PartialEq, Debug)]
pub enum LoginAction {
    Accept(Role),               // tuple-like variant
    Denied(DeniedReason),       // tuple-like variant
}
```

Enums with data are the size of the largest member. A `String` occupies two `usize` values (length + pointer).

## Option Type

`Option<T>` is a built-in enum representing a value that may or may not exist. It is the safe Rust alternative to nullable pointers:

```rust
pub fn login(name: &str) -> Option<LoginAction> {
    match name.to_lowercase().trim() {
        "herbert" => Some(LoginAction::Accept(Role::Admin)),
        "bob" => Some(LoginAction::Accept(Role::User)),
        _ => None,
    }
}
```

Every response must be `Some(...)` or `None`. This forces callers to handle both cases, avoiding null-pointer bugs.

## Match Expressions

`match` is central to Rust's expressive power. Unlike `switch` in other languages, Rust's `match` supports pattern matching, variable capture, and exhaustive checking:

```rust
match login(&input) {
    None => {
        println!("{} is not a known user.", input.trim());
    }
    Some(LoginAction::Accept(role)) => {
        match role {
            Role::Admin => println!("With great power, comes great responsibility."),
            Role::User => println!("You have regular user access"),
            Role::Limited => println!("You have read-only access."),
        }
    }
    Some(LoginAction::Denied(DeniedReason::PasswordExpired)) => {
        println!("Unfortunately, your password has expired.");
    }
    Some(LoginAction::Denied(DeniedReason::AccountLocked { reason })) => {
        println!("Sorry, your login was denied.");
        println!("Reason: {reason}");
    }
}
```

Key points:
- `|` means `or` in match patterns: `"bob" | "fred" => ...`
- `_` means "default" (wildcard)
- Variables can be captured from inside patterns: `reason` captures the string
- `_` ignores a field; `..` ignores all remaining fields
- There is no fall-through between arms
- The compiler warns if a variant is not handled

### `if let`

`if let` is a concise form of `match` for single-pattern matching:

```rust
if let Some(LoginAction::Denied(DeniedReason::AccountLocked { reason: _ })) = login("kevin") {
    // matched
} else {
    panic!("Failed");
}
```

## Enum Methods

Enums can have two types of functions: associated functions (like static methods) and member functions.

### Associated Functions

Associated functions are called on the type itself, not an instance. They don't take `self`:

```rust
impl LoginAction {
    fn standard_user() -> Option<Self> {
        Some(LoginAction::Accept(Role::User))
    }
}

// Usage:
"bob" => LoginAction::standard_user(),
```

`Self` (uppercase) refers to the type itself.

### Member Functions

Member functions take `&self` (or `&mut self`) and operate on an instance:

```rust
impl LoginAction {
    pub fn do_login(&self, on_success: fn(&Role), on_denied: fn(&DeniedReason)) {
        match self {
            Self::Accept(role) => on_success(role),
            Self::Denied(reason) => on_denied(reason),
        }
    }
}
```

### Function Pointers as Callbacks

`fn(&Role)` and `fn(&DeniedReason)` are *function pointers*. You can pass functions as parameters:

```rust
fn user_accepted(role: &Role) {
    println!("You are logged in as a {role:?}");
}

login_action.do_login(user_accepted, |reason| {
    println!("Access denied!");
    println!("{reason:?}");
});
```

### Closures in Match Arms

Closures (anonymous functions) can be passed inline, as shown with `|reason| { ... }` in the example above.

## Type Aliases

When enum names are long or generic, type aliases provide shorter names:

```rust
enum VeryVerboseEnumOfThingsToDoWithNumbers { Add, Subtract }
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;
let x = Operations::Add;
```

Within `impl` blocks, `Self` serves the same role.

## Bringing Variants into Scope with `use`

The `use` declaration can import enum variants to avoid repeated qualification:

```rust
enum Stage { Beginner, Advanced }
use Stage::{Beginner, Advanced};  // selective import
use Role::*;                       // wildcard import

let stage = Beginner;   // instead of Stage::Beginner
```

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust Structs](rust-structs.md) — enum variants mirror the three struct forms
- [Rust Linked List with Enums](rust-linked-list-with-enums.md) — practical enum pattern (Cons/Nil)
- [Rust Primitives](rust-primitives.md) — integers used as enum discriminators
