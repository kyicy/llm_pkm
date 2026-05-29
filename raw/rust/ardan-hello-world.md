# First Program: Hello World

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

## Create a new Rust Project

1. Open VSCode.
2. Select "Open Folder" and load wherever you cloned this GitHub repo.
3. Select `File` -> `New Window`.
4. Open the integrated terminal with `View` -> `Terminal` or `Ctrl` + `backtick`

Let's make a new Rust program with `cargo new`:

1. Change to a new directory. Type: `cd rust/live` `<enter>`
2. Create a new project with `cargo new login_system`.
    * `login_system` is the name of the program to create.

> You can also use `cargo init`. They do the same thing.

You should see:

```
     Created binary (application) `login_system` package
```

Let's take a quick tour of everything that has been done.

```
cd login_system
tree /f
    (on Windows), du -h will give a similar display on *NIX.
```

There's more here than you might expect:

```
C:.
│   .gitignore
│   Cargo.toml
│
└───src
        main.rs
```

## Surprise: Git Integration!

* `.gitignore`. Rust has created a Git file to automatically exclude your `target` directory.
* If you `dir -h .`, you discover a `.git` folder — a whole new Git repository!

You can NOT use Git by modifying the `cargo new` command:

```
cargo new --vcs none login_system_nogit
```

Other `--vcs` options:
* `git` - the default
* `hg` - Mercurial
* `pijul`
* `fossil`
* `none` - don't do any automatic SCM integration.

> **Tip**: If you are already inside a Git workspace, creating a new project won't make another one.

## Cargo.toml

Every new project will have a `Cargo.toml` file created:

```toml
[package]               # Every Cargo project needs a package section
name = "login_system"   # The project name, which will double as the target filename
version = "0.1.0"       # Version in semantic versioning.
edition = "2021"        # Which edition of Rust.

[# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
# Defaults to an empty list.
```

Why 2021? Every few years, Rust issues a new *edition*. This is the only time at which substantial syntax changes are permitted. Rust retains compatibility with older editions.

## The `src` folder

Your source code largely lives in the `src` folder. Rust has created a `main.rs` file.

* If a project has a `main.rs`, it expects to have a function named `main()` — and builds an executable.
* If a project has a `lib.rs` file, it's a library.
* If a project has *both*, then it can be included in other projects as a library — or executed.

Let's take a quick look at `main.rs`:

```rust
fn main() {
    println!("Hello, world!");
}
```

Things to note:

* Rust is *terse* — `fn` for `function`.
* `fn main()` creates a new *function* called `main`, with no parameters.
* `println!` has a mysterious `!`. That denotes it as a *macro*.
* You can expand macros in Rust Analyzer via the Command Palette.

## Run "Hello World"

You can run the newly created program with `cargo run`.

You'll see the output:

```
   Compiling hello_login_system v0.1.0
    Finished dev [unoptimized + debuginfo] target(s) in 1.57s
     Running `target/debug/hello_login_system.exe`
Hello, world!
```

This runs everything in *debug* mode. Optimizations are disabled, extra debug information is generated, and extra run-time error checks are running.

You can always run in optimized mode with:

```
cargo run --release
```
