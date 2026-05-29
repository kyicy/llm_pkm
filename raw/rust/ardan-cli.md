# Build a Command-Line User Management App

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

## Create a new project

1. Go to your workspace root.
2. Create a new project: `cargo new userman`.
3. Edit `Cargo.toml` to include `userman` in your workspace `[members]`.

## Setup Dependencies

We're using `clap`, the standard way of reading command-line options in Rust:

```toml
[dependencies]
authentication = { path = "../authentication" }
clap = { version = "4", features = ["derive"] }
```

## A Minimal Clap Example

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
}

fn main() {
    let cli = Args::parse();
    match cli.command {
        Some(Commands::List) => {
            println!("All Users Goes Here\n");
        }
        None => {
            println!("Run with --help to see instructions");
            std::process::exit(0);
        }
    }
}
```

Working through this program:
* `#[derive(Parser)]` adds Clap parser code to a structure.
* `#[command()]` indicates that this is the default command.
* `#[command(subcommand)]` tells Clap we're defining additional command-line options.
* `#[derive(Subcommand)]` tells Clap that an enumeration contains sub-commands.
* Each enumeration entry represents one possible command.
* `///` is a *documentation comment* — used if you use `cargo doc`.
* `let cli = Args::parse()` tells Clap to start parsing command-line arguments.

Passing arguments to `cargo run`:

```
cargo run -- --help
```

## Displaying a List of Users

Let's use a type alias to reduce typing:

```rust
type UserMap = HashMap<String, User>;
```

Building a user list function with formatted output:

```rust
fn list_users(users: &UserMap) {
    println!("{:<20}{:<20}", "Username", "Login Action");
    println!("{:-<40}", "");

    users
        .iter()
        .for_each(|(_, user)| {
            println!("{:<20}{:<20?}", user.username, user.action);
        });
}
```

New format string features:
* `{:<20}` — left align and pad to 20 characters wide.
* `{:-<40}` — use `-` to pad left 40 characters wide.
* `iter()` on a `HashMap` returns `(key, value)` tuples.
* `_` marks the key as a placeholder.
* `{:<20?}` combines left-align with debug formatting.

### Adding color with the `colored` crate

```toml
colored = "2.0.0"
```

```rust
fn list_users(users: &UserMap) {
    use colored::Colorize;
    println!("{:<20}{:<20}", "Username", "Login Action");
    println!("{:-<40}", "");

    users
        .iter()
        .for_each(|(_, user)| {
            let action = format!("{:?}", user.action);
            let action = match user.action {
                LoginAction::Accept(..) => action.green(),
                LoginAction::Denied(..) => action.red(),
            };
            println!("{:<20}{:<20}", user.username, action);
        });
}
```

## Adding Users

Add a save function to the authentication library:

```rust
pub fn save_users_file(users: &HashMap<String, User>) {
    use std::io::Write;
    let json = serde_json::to_string_pretty(&users).unwrap();
    let mut f = std::fs::File::create("users.json").unwrap();
    f.write_all(json.as_bytes()).unwrap();
}
```

Add a subcommand for adding a user:

```rust
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
  }
}
```

Handle it:

```rust
fn main() {
    let mut users = get_users();
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

The `add_user` function:

```rust
fn add_user(users: &mut UserMap, username: String, password: String, limited: Option<bool>, admin: Option<bool>) {
    let action = LoginAction::Accept(
        if limited.is_some() {
            Role::Limited
        } else if admin.is_some() {
            Role::Admin
        } else {
            Role::User
        }
    );
    let user = User::new(&username, &password, action);
    users.insert(username, user);
    save_users_file(users);
}
```

### Duplicate Users Check

```rust
if users.contains_key(&username) {
    println!("{username} already exists, aborting.");
    return;
}
```

## Deleting Users

```rust
/// Delete a user
Delete {
    /// Username
    username: String,
}

fn delete_user(users: &mut UserMap, username: String) {
    if !users.contains_key(&username) {
        println!("{username} does not exist, aborting");
        return;
    }
    users.remove(&username);
    save_users_file(users);
}
```

## Updating Users

### Changing passwords

```rust
/// Change a password
ChangePassword {
    /// Username
    username: String,
    /// New Password
    new_password: String,
}

fn change_password(users: &mut UserMap, username: String, new_password: String) {
    if let Some(mut user) = users.get_mut(&username) {
        user.password = hash_password(&new_password);
        save_users_file(users);
    } else {
        println!("{username} does not exist, aborting");
    }
}
```

`get_mut` returns a *mutable* reference to a record in the `HashMap`.
