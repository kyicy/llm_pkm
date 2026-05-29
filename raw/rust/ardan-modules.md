# Modules and Visibility

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

A module is a way of grouping code together. It acts as a namespace. Modules also enforce privacy. You have very tight control over what can be accessed inside a module from the rest of your program.

## Terminology

* A `module` is a sub-group of code within a `crate`.
* A `crate` is a combined unit of code, combining modules together. It's either executable or a library.

## Module Method 1: Using `mod` blocks

Wrap code in a `mod` block:

```rust
mod user {
    #[derive(Clone, Debug, Serialize, Deserialize)]
    pub struct User {
        pub username: String,
        pub password: String,
        pub action: LoginAction,
    }

    impl User {
        pub fn new(username: &str, password: &str, action: LoginAction) -> Self {
            Self {
                username: username.to_string(),
                password: hash_password(password),
                action
            }
        }
    }
}
```

Key rules:
* **Modules don't inherit `use` statements from their parent super-module.** You must import everything you need inside each module: `use crate::{LoginAction, hash_password};`
* **Modules don't automatically expose anything in child modules.** Access child types with `use user::User;` at the parent level.
* **Modules themselves are private by default.** Mark with `pub mod user {` to expose the module externally. Alternatively, re-export with `pub use user::User;`

### Struct Member Visibility

```rust
pub password: String;         // Accessible anywhere
pub(crate) password: String;  // Accessible within the crate only
password: String;             // Private to the module
```

### Access from Outside the Crate

Use `pub use` to re-export items from modules as top-level API:

```rust
pub use user::User;
```

This lets consumers do `use authentication::User` instead of `use authentication::user::User`.

## Module Method 2: A Separate File

Create a file such as `user.rs` in `src/`, and add it to the project:

```rust
// In lib.rs:
mod user;
pub use user::User;
```

Adding a file to `src/` does not automatically make it part of the program. You must declare it with `mod <name>;`.

## Module Method 3: Multi-File Modules (Directory)

Create a directory with `mod.rs`:

```
src/
├── lib.rs
├── user.rs
└── login_action/
    ├── mod.rs
    ├── role.rs
    ├── denied_reason.rs
    └── login_action.rs
```

In `lib.rs`:
```rust
mod login_action;
pub use login_action::*;
```

In `login_action/mod.rs`:
```rust
mod denied_reason;
mod login_action;
mod role;

pub use denied_reason::DeniedReason;
pub use login_action::LoginAction;
pub use role::Role;
```

Child files need imports from the crate root:
```rust
use crate::{Role, DeniedReason};
use serde::{Serialize, Deserialize};
```

## Re-Exporting

You can re-export dependencies so consumers don't need to add their own:

```rust
pub mod serde {
    pub use serde::*;
}
```

This lets consumers use `use authentication::serde::Serialize;`.

## Preludes

It's common to create a module named `prelude` and `pub use` the important types there. This convention makes it easy for users to find important types.
