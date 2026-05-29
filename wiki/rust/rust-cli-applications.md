# Rust CLI Applications

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-cli.md](../../raw/rust/ardan-cli.md)

## Overview

Rust is well-suited for building command-line applications. The standard library provides basic argument parsing via `std::env::args()`, while the `clap` crate provides a more powerful system with automatic help generation, subcommands, and argument validation.

## Basic CLI with Clap

Clap with the `derive` feature uses Rust's derive macros to define the CLI interface declaratively:

```toml
[dependencies]
clap = { version = "4", features = ["derive"] }
```

### Defining Commands

```rust
use clap::{Parser, Subcommand};

#[derive(Parser)]
#[command()]
struct Args {
    #[command(subcommand)]
    command: Option<Commands>,
}

#[derive(Subcommand)]
enum Commands {
    /// List all users.
    List,
    /// Add a user.
    Add {
        /// Username
        #[arg(long)]
        username: String,

        /// Password
        #[arg(long)]
        password: String,

        /// Optional - mark as a limited user
        #[arg(long)]
        limited: Option<bool>,

        /// Optional - mark as an admin
        #[arg(long)]
        admin: Option<bool>,
    },
}
```

Key points:
- `#[derive(Parser)]` generates argument parsing code for a struct
- `#[derive(Subcommand)]` makes an enum define subcommands
- `#[arg(long)]` marks a field as a `--long` option
- `///` doc comments become help text for each command/argument

### Parsing and Dispatching

```rust
fn main() {
    let cli = Args::parse();
    match cli.command {
        Some(Commands::List) => list_users(&users),
        Some(Commands::Add { username, password, limited, admin }) => {
            add_user(&mut users, username, password, limited, admin);
        }
        None => {
            println!("Run with --help to see instructions");
            std::process::exit(0);
        }
    }
}
```

## Building a User Management CLI

### Type Aliases

```rust
type UserMap = HashMap<String, User>;
```

### Listing Users

```rust
fn list_users(users: &UserMap) {
    println!("{:<20}{:<20}", "Username", "Login Action");
    println!("{:-<40}", "");

    users.iter().for_each(|(_, user)| {
        println!("{:<20}{:<20?}", user.username, user.action);
    });
}
```

Format specifiers:
- `{:<20}` — left-align, pad to 20 characters
- `{:-<40}` — fill with `-`, width 40
- `{:<20?}` — left-align, width 20, debug format

### Adding Users

```rust
fn add_user(users: &mut UserMap, username: String, password: String,
            limited: Option<bool>, admin: Option<bool>) {
    if users.contains_key(&username) {
        println!("{username} already exists, aborting.");
        return;
    }
    let action = LoginAction::Accept(
        if limited.is_some() { Role::Limited }
        else if admin.is_some() { Role::Admin }
        else { Role::User }
    );
    let user = User::new(&username, &password, action);
    users.insert(username, user);
    save_users_file(users);
}
```

Note: if expressions can be used anywhere a value is expected — the parameter to `Accept` is itself an `if` expression.

### Deleting Users

```rust
fn delete_user(users: &mut UserMap, username: String) {
    if !users.contains_key(&username) {
        println!("{username} does not exist, aborting");
        return;
    }
    users.remove(&username);
    save_users_file(users);
}
```

### Changing Passwords

```rust
fn change_password(users: &mut UserMap, username: String, new_password: String) {
    if let Some(mut user) = users.get_mut(&username) {
        user.password = hash_password(&new_password);
        save_users_file(users);
    } else {
        println!("{username} does not exist, aborting");
    }
}
```

`get_mut` returns a mutable reference to a `HashMap` entry, allowing in-place updates.

### Running with Arguments

Pass arguments to `cargo run` with `--`:

```bash
$ cargo run -- --help
$ cargo run -- list
$ cargo run -- add --username chester --password tester --limited true
$ cargo run -- delete chester
$ cargo run -- change-password --username bob --new-password newpass
```

## See Also

- [Rust Serde Serialization](rust-serde-serialization.md) — persisting CLI app data
- [Rust Password Hashing](rust-password-hashing.md) — hashing passwords in CLI apps
- [Rust Hashmaps](rust-hashmaps.md) — data structures used in user management
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — format string specifiers for CLI output
- [Rust Rocket Web Framework](rust-rocket-web.md) — building web interfaces to CLI tools and services
