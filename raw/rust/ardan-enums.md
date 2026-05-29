# Enumerations

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Enumerations should be familiar from other languages. Let's create a simple one for logins:

```rust
pub enum LoginAction {
    Admin,
    User,
    Denied,
}
```

> If you're used to C, Java or similar this should look very familiar. Just like C, enumerations like this one are also stored numerically and you can cast a value with `as (number)`.

Now we can create a login function with more options:

```rust
pub fn login(name: &str) -> LoginAction {
    match name.to_lowercase().trim() {
        "herbert" => LoginAction::Admin,
        "bob" | "fred" => LoginAction::User,
        _ => LoginAction::Denied,
    }
}
```

What's new here?
* The function is returning the `enum` type we created.
* We're using `match` instead of `if` statements. Pattern matching is central to a lot of Rust's expressive power.
* Match statements follow the syntax `(pattern) => expression`.
* We use `|` to mean `or` in match statements.
* The `_` means "default".

```rust
#[derive(PartialEq, Debug)]
pub enum LoginAction {
    Admin,
    User,
    Denied,
}
```

`#[derive]` can add a lot of implementations to your code automatically. `PartialEq` is a *trait* — interfaces that describe the capabilities of a type.

## Enumerations with Variables

Let's create a new enumeration for user roles and denied reasons:

```rust
#[derive(PartialEq, Debug)]
pub enum Role {
    Admin,
    User,
    Limited
}

#[derive(PartialEq, Debug)]
pub enum DeniedReason {
    PasswordExpired,
    AccountLocked{reason: String},
}
```

Rust enumerations share a lot in common with `union` types in other languages. You can attach variables to individual entries.

> Enumerations with data are the size of the largest member. A `String` occupies two `usize` variables: the length and a pointer to the string data.

Now let's modify our initial `LoginAction` enum:

```rust
#[derive(PartialEq, Debug)]
pub enum LoginAction {
    Accept(Role),
    Denied(DeniedReason),
}
```

## Optional Users

Let's extend `login` to include an `Option` — a type that either has or doesn't have a value. It's the closest you'll get in safe Rust to a `NULL`, but forces you to check it.

```rust
pub fn login(name: &str) -> Option<LoginAction> {
    match name.to_lowercase().trim() {
        "herbert" => Some(LoginAction::Accept(Role::Admin)),
        "bob" => Some(LoginAction::Accept(Role::User)),
        "fred" => Some(LoginAction::Denied(DeniedReason::PasswordExpired)),
        "kevin" => Some(LoginAction::Denied(DeniedReason::AccountLocked { reason: "Call Human Resources!".to_string() })),
        _ => None,
    }
}
```

Now we've changed the return type to `Option<LoginAction>`. Every response must be `Some(..)` or `None`.

### Using `if let`

```rust
if let Some(LoginAction::Denied(DeniedReason::AccountLocked { reason: _ })) = login("kevin") {
    // All is well
} else {
    panic!("Failed to read kevin");
}
```

`if let` is the same as a `match` statement, with only one pattern to match.

## Pattern Matching Login Client

```rust
match login(&input) {
    None => {
        println!("{} is not a known user.", input.trim());
        println!("This is where we handle new users.");
    }
    Some(LoginAction::Accept(role)) => {
        println!("Welcome: {}", input.trim());
        match role {
            Role::Admin => println!("With great power, comes great responsibility."),
            Role::Limited => println!("You have read-only access."),
            Role::User => println!("You have regular user access"),
        }
    }
    Some(LoginAction::Denied(DeniedReason::PasswordExpired)) => {
        println!("Unfortunately, your password has expired.");
    }
    Some(LoginAction::Denied(DeniedReason::AccountLocked { reason })) => {
        println!("Sorry, {}, your login was denied.", input.trim());
        println!("Reason: {reason}");
    }
}
```

Things to note:
* `match` can handle nested structures.
* You can *capture* variables from inside a statement.
* You can ignore variables with `_` or `..`.
* You can nest `match` statements.
* There's no fall-through: no need to `break`.
* The compiler will warn you if you add an enumeration variant and forget to check it.

## Enumerations can Contain Functions

There are two major types of function that can be implemented inside an `enum`: associated functions and member functions.

```rust
impl LoginAction {
    fn standard_user() -> Self {
        LoginAction::Accept(Role::User)
    }
}
```

* `Self` (uppercase) refers to the type itself.
* `standard_user()` does *not* contain `self` — making it an *associated function* (like a static method).

### Member functions with function pointers

```rust
pub fn do_login(&self, on_success: fn(&Role), on_denied: fn(&DeniedReason)) {
    match self {
        Self::Accept(role) => on_success(role),
        Self::Denied(reason) => on_denied(reason),
    }
}
```

* `&self` means "provide a read-only reference to myself".
* `fn(&Role)` and `fn(&DeniedReason)` are *function pointers*. You can pass in a function as a parameter.

### Using `do_login` with closures

```rust
use auth_enum_fn::*;

fn user_accepted(role: &Role) {
    println!("You are logged in as a {role:?}");
}

fn main() {
    // ...
    match login(&input) {
        None => { /* ... */ }
        Some(login_action) => {
            login_action.do_login(
                user_accepted,
                |reason| {
                    println!("Access denied!");
                    println!("{reason:?}");
                }
            )
        }
    }
}
```

* `user_accepted` is a regular function passed as a function pointer.
* For "denied", we used a *closure* — an inline function.
* `{:?}` is a format macro shorthand for "print the debug representation".
