# Setup Your Rust Development Environment

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

> Hopefully, you've already done some of this.

## Rust Setup with RustUp

If you haven't already, you need to have Rust installed on your computer.
Visit [RustUp](https://rustup.rs/) and install from there. Instructions
will vary by platform.

### Things to Know About RustUp

There are some caveats about RustUp that you need to know:

* RustUp installs Rust *for your user account*. It doesn't perform a shared installation.
* You *can* get a working environment through package managers such as `snap`, `apt`, `homebrew` and similar. It's better to use the native Rust setup, you get much faster access to updates.
* On Windows, if you don't already have it installed you will be prompted to also install the Visual C++ build tools.
* On a Mac, you will be prompted to install the OS X development tools if you haven't already.
* On Linux, make sure you have LLVM installed.

### Verify that you have a working RustUp

Enter the command `rustup --version`. You should see something like this:

```
rustup 1.25.1 (bb60b1e89 2022-07-12)
info: This is the version for the rustup toolchain manager, not the rustc compiler.
info: The currently active `rustc` version is `rustc 1.65.0 (897e37553 2022-11-02)`
```

> *The version numbers will change.*

**If you plan to code along, please take a second to make sure that Rust is installed and working.**

### Update to the Latest Stable Rust

From time to time (I do monthly), it's a good idea to update your Rust setup. Bug fixes and
performance improvements are applied periodically. Rust won't break *stable* unless a
major security vulnerability emerges.

**To update RustUp itself**:

`rustup self update`

**To update Rust to the latest**:

Enter:

```
rustup update
```

> Once you have a stable project, you may want to coordinate updates with your team to ensure that you are all on the same version.

## Adding Toolchains

You may want to target platforms other than the one you are using for development. Rust includes cross-compilation.

For example, you can support WASM by running:

```
rustup target add wasm32-unknown-unknown
```

Once that's present, you can build for WASM with `cargo build --target wasm32-unknown-unknown`.

## Install Clippy!

It should be installed by default, but some older---updated---setups don't always have it. Run the following:

```
rustup component add clippy
```
