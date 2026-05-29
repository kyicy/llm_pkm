# Structures

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Now we want to create a `struct` to represent the important pieces of user information:

```rust
pub struct User {
    username: String,
    password: String,
    action: LoginAction,
}
```

Let's add a constructor:

```rust
impl User {
    pub fn new(username: &str, password: &str, action: LoginAction) -> Self {
        Self {
            username: username.to_string(),
            password: password.to_string(),
            action
        }
    }
}
```

Two things to note:
* We're using `.to_string()` to convert `&str` into a `String`.
* `action` is the same as the parameter, so you can omit `action: action` (field init shorthand).

## Arrays and Slices

Let's make a function that returns a list of users:

```rust
pub fn get_users() -> [User; 3] {
    [
        User::new("herbert", "password", LoginAction::Accept(Role::Admin)),
        User::new("bob", "password", LoginAction::Accept(Role::User)),
        User::new("fred", "password", LoginAction::Denied(DeniedReason::PasswordExpired)),
    ]
}
```

Now a function to test a login using slices and iterators:

```rust
pub fn login(users: &[User], username: &str, password: &str) -> Option<LoginAction> {
    let username = username.trim().to_lowercase();
    let password = password.trim();
    if let Some(user) = users
        .iter()
        .find(|u| u.username == username && u.password == password) {
        Some(user.action.clone())
    } else {
        None
    }
}
```

This doesn't compile initially because `LoginAction` doesn't support being cloned. We need to add `Clone`:

```rust
#[derive(PartialEq, Debug, Clone)]
```

Clippy suggests simplifying to:

```rust
pub fn login(users: &[User], username: &str, password: &str) -> Option<LoginAction> {
    let username = username.trim().to_lowercase();
    let password = password.trim();
    users
        .iter()
        .find(|u| u.username == username && u.password == password)
        .map(|user| user.action.clone())
}
```

Things to notice:
* Take a *slice* of `User` types (`&[User]`). A slice is any set of array, vector or other contiguous structures.
* Create an *iterator* with `.iter()`.
* Call `find` which reads each entry and runs the provided comparison closure function.
* `.map()` transforms `Some(user)` into `Some(user.action.clone())`.

## Integration in the login program

```rust
use auth_struct::*;

fn user_accepted(role: &Role) {
    println!("You are logged in as a {role:?}");
}

fn main() {
    let users = get_users();

    println!("Welcome to the (Not Very) Secure Server");
    println!("Enter your username:");
    let mut username = String::new();
    let mut password = String::new();
    let stdin = std::io::stdin();
    stdin.read_line(&mut username).unwrap();
    println!("Enter your password:");
    stdin.read_line(&mut password).unwrap();

    match login(&users, &username, &password) {
        None => {
            println!("{} is not a known user.", username.trim());
        }
        Some(login_action) => {
            login_action.do_login(
                user_accepted,
                |reason| {
                    println!("Access denied");
                    println!("{reason:?}");
                }
            )
        }
    }
}
```

To note:
* We fetch the user list with `get_users()`.
* We retrieve both a username and a password.
* When we call `login`, we can automatically convert the users array into a slice by borrowing it.
