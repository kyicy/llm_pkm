# Cargo Workspaces

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

If you're working with more than one related project, `workspaces` can help you:

* Workspaces combine all of your builds into a single `target` folder.
* Workspaces share downloads — if you have a bunch of projects with shared dependencies, workspaces build them once and share the result. Faster compilation, less disk space usage.
* A lot of cargo commands can be run in the "workspace root" with `--all` as a command-line flag, and will operate on all of them. Run all of your tests with `cargo test --all`, or build everything with `cargo build --all`.

> While working on Hands-on Rust, I had so many examples outside of a workspace that I ran out of disk space. Moving into a workspace meant I only had a single copy of each library.

## Our Current Setup

Go back to your source folder. Open `Cargo.toml` and add a `workspace` section:

```toml
[workspace]
members = []
```

The workspace automatically includes the top-level `src` directory. This is the *parent* workspace.

It's often confusing if you open a workspace with several projects and `cargo run` just happens to run the first project you created! Edit `src/main.rs` to change the message:

```rust
fn main() {
    println!("You probably wanted to run one of the nested workspaces.");
}
```

Now, if someone accidentally runs the parent project they are notified.

Let's create a `login` project *inside* the workspace:

```
cargo new login
```

You will see a warning:

```
warning: compiling this new package may not work due to invalid workspace configuration
...
error: failed to load manifest for workspace member
```

This is a long-winded way of saying: *Don't forget to add the new project to your workspace members*.

Add the newly created project by re-opening the parent's `Cargo.toml` and adding it to your workspace:

```toml
members = [
    "login",
]
```

## Try It Out

1. Change directory to your workspace root.
2. Type `cargo run`. You'll see the message that you probably didn't mean to run this one.
3. Change directory to your `login` program.
4. Type `cargo run` and see "Hello World".
5. Notice that there's only one `target` folder for the whole workspace.
