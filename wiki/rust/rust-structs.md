# Rust Structs

> Sources: Rust by Example, Unknown; Ardan Ultimate Rust Foundations, 2025
> Raw: [structs.md](../../raw/rust/2026-05-29-structs.md); [ardan-structs.md](../../raw/rust/ardan-structs.md)

## Overview

Rust supports three kinds of structs via the `struct` keyword: classic C-like structs with named fields, tuple structs (essentially named tuples), and unit structs with no fields (useful for generics and marker types). Structs support field init shorthand, struct update syntax, destructuring, and can be nested as fields of other structs.

## Three Struct Variants

### Classic C Structs

Named fields accessed with dot notation:

```rust
struct Point {
    x: f32,
    y: f32,
}

let point = Point { x: 5.2, y: 0.4 };
println!("({}, {})", point.x, point.y);
```

### Tuple Structs

Positional fields accessed by index, like named tuples:

```rust
struct Pair(i32, f32);
let pair = Pair(1, 0.1);
println!("{} and {}", pair.0, pair.1);
```

### Unit Structs

No fields at all — useful as marker types or for trait implementations on types that carry no data:

```rust
struct Unit;
let _unit = Unit;
```

## Construction Patterns

### Field Init Shorthand

When variable names match field names, omit the colon:

```rust
let name = String::from("Peter");
let age = 27;
let peter = Person { name, age };  // equivalent to name: name, age: age
```

### Struct Update Syntax

Copy remaining fields from another instance of the same type:

```rust
let bottom_right = Point { x: 10.3, ..another_point };
```

## User Struct Example (with Methods)

A practical example modeling a user with a constructor:

```rust
pub struct User {
    username: String,
    password: String,
    action: LoginAction,
}

impl User {
    pub fn new(username: &str, password: &str, action: LoginAction) -> Self {
        Self {
            username: username.to_string(),
            password: password.to_string(),
            action,  // field init shorthand — same as `action: action`
        }
    }
}
```

The constructor uses `Self` to refer to the struct type, `to_string()` to convert `&str` to `String`, and field init shorthand to avoid repeating `action: action`.

## Working with Arrays of Structs and Slices

Store multiple users in an array:

```rust
pub fn get_users() -> [User; 3] {
    [
        User::new("herbert", "password", LoginAction::Accept(Role::Admin)),
        User::new("bob", "password", LoginAction::Accept(Role::User)),
        User::new("fred", "password", LoginAction::Denied(DeniedReason::PasswordExpired)),
    ]
}
```

A function accepting a slice (`&[User]`) can work with arrays, vectors, or any contiguous collection:

```rust
pub fn login(users: &[User], username: &str, password: &str) -> Option<LoginAction> {
    users
        .iter()
        .find(|u| u.username == username && u.password == password)
        .map(|user| user.action.clone())
}
```

This pattern demonstrates:
- **Slices (`&[T]`)**: accept any contiguous collection without knowing the container type
- **Iterators (`.iter()`)**: create an iterator over elements
- **`.find()`**: locate the first matching element using a closure
- **`.map()`**: transform `Some(user)` into `Some(user.action.clone())`
- **Clone**: required because `LoginAction` contains `String` fields — add `#[derive(Clone)]`

Arrays autoconvert to slices when borrowed: `login(&users, &username, &password)` works because `&[User; 3]` coerces to `&[User]`.

## Destructuring

Structs can be destructured in `let` bindings:

```rust
let Point { x: left_edge, y: top_edge } = point;
let Pair(integer, decimal) = pair;
```

## Nested Structs

Structs can be composed as fields of other structs:

```rust
struct Rectangle {
    top_left: Point,
    bottom_right: Point,
}
```

Derive `Debug` (`#[derive(Debug)]`) to enable debug printing with `{:?}`. Derive `Clone` (`#[derive(Clone)]`) to enable deep copying.

## See Also

- [Rust Custom Types](rust-custom-types.md) — overview of all custom type mechanisms
- [Rust NewType Pattern](rust-new-type-pattern.md) — tuple struct wrappers for type safety
- [Rust Enums](rust-enums.md) — enum variants can be unit-like, tuple-like, or struct-like
- [Rust Tuples](rust-tuples.md) — tuple structs build on the same concepts
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — `Debug` and `Display` for structs
- [Rust Generic Data Structures](rust-generic-data-structures.md) — generic types with `impl<T>` blocks
- [Rust Arrays and Slices](rust-arrays-and-slices.md) — arrays and slices for storing structs
- [Rust Vectors](rust-vectors.md) — the heap-allocated, resizable alternative to arrays
