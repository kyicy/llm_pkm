# Rust Modules and Visibility

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-modules.md](../../raw/rust/ardan-modules.md)

## Overview

Modules group code into namespaces and enforce privacy boundaries. They are the primary mechanism for organizing Rust code into manageable units. A module can be a block within a file, a separate file, or a directory of files.

## Terminology

- **Module**: A sub-group of code within a crate
- **Crate**: A combined unit of code (executable or library), combining modules

## Three Ways to Define Modules

### 1. Inline `mod` Blocks

```rust
mod user {
    use serde::{Serialize, Deserialize};
    use crate::{LoginAction, hash_password};

    #[derive(Clone, Debug, Serialize, Deserialize)]
    pub struct User {
        pub username: String,
        pub password: String,
        pub action: LoginAction,
    }
}
```

### 2. Separate File

Create `user.rs` in `src/`:

```rust
// In lib.rs:
mod user;          // declares the module
pub use user::User;  // re-exports for external consumers
```

A file in `src/` does not automatically become part of the program — you must declare it with `mod <name>;`.

### 3. Directory with `mod.rs`

```
src/
├── lib.rs
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
mod role;
mod denied_reason;
mod login_action;

pub use role::Role;
pub use denied_reason::DeniedReason;
pub use login_action::LoginAction;
```

## Visibility Modifiers

| Modifier | Visibility |
|----------|------------|
| `pub` | Accessible anywhere |
| `pub(crate)` | Accessible within the crate only |
| `pub(super)` | Accessible in parent module only |
| (default) | Private to the module |

```rust
pub fn public_function() {}      // accessible anywhere
pub(crate) fn crate_only() {}    // within the crate only
fn private_function() {}         // within this module only
```

## Accessing Items Across Modules

- `use crate::module::Item` — absolute path from crate root
- `use super::Item` — relative path from parent module
- `use self::Item` — relative path from current module

## Re-Exporting Dependencies

Libraries can re-export dependencies so consumers don't need to add them:

```rust
pub mod serde {
    pub use serde::*;
}
```

## Preludes

A common convention is to create a `prelude` module that re-exports the most important types. Users can then `use library::prelude::*` to get everything they need.

## See Also

- [Rust Library Crates](rust-library-crates.md) — crate types and public visibility
- [Rust Documentation](rust-documentation.md) — documenting modules for consumers
