# Rust Safety Guarantees

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-safety.md](../../raw/rust/ardan-safety.md); [ardan-nostd.md](../../raw/rust/ardan-nostd.md)

## Overview

Rust provides strong safety guarantees, but they have specific bounds. Understanding what Rust *does* and *does not* guarantee — and when to use `unsafe` — is essential for writing robust Rust code.

## Memory Safety

Rust's memory safety guarantees ensure **no**:
- Use-after-free
- Buffer overruns
- Dangling pointers
- Iterator invalidation

These account for a large percentage of security vulnerabilities in C and C++ programs.

Rust specifically does **NOT** guarantee against memory leaks. `std::mem::forget` allows explicit leaking. However, Rust's defaults make leaks difficult — RAII and Drop handling largely eliminate the problem in normal usage.

## Thread Safety

Rust prevents **data races** — concurrent read/write or write/write to the same memory without synchronization. This is enforced at compile time through the type system (the `Send` and `Sync` traits).

Rust does **NOT** prevent deadlocks. Misusing locks (e.g., double-locking a Mutex) causes deadlocks at runtime. RAII scope-bound locks help but don't eliminate the need for careful design.

## Type Safety

Rust enforces type safety, but you must opt into stronger guarantees through patterns like **NewTypes** — tuple struct wrappers that prevent mixing semantically distinct values of the same underlying type.

## The `unsafe` Keyword

Marking a block `unsafe` does not mean the code will explode. It means the code **cannot be proved safe** by Rust's static analyzer. Common `unsafe` scenarios:
- Dereferencing raw pointers
- Calling functions through FFI (foreign code can't offer Rust guarantees)
- Direct hardware access

`unsafe` isolates these operations so the rest of your crate remains provably safe.

## Auditing with `cargo audit`

```bash
$ cargo install cargo-audit
$ cargo audit
```

`cargo audit` scans your dependency tree against CVE reports. It's recommended for any production Rust project, and GitHub Actions can run it automatically.

## `#![no_std]`: Life Without the Standard Library

Rust can operate without the standard library for embedded systems, kernel modules, and other constrained environments:

```rust
#![no_std]
```

This creates very small binaries but loses access to collections, heap allocation, and other conveniences. Rust remains a true systems language — you can build an operating system with it.

## Summary

| Safety Domain | Guaranteed | Not Guaranteed |
|--------------|------------|----------------|
| Memory | Use-after-free, buffer overrun, dangling pointers | Memory leaks |
| Thread | Data races (compile-time) | Deadlocks |
| Type | Type safety (with opt-in via NewTypes) | Automatic semantic separation |
| Unsafe | Isolates unprovable code | No runtime safety checks in `unsafe` blocks |

## See Also

- [Rust Borrow Checker](rust-borrow-checker.md) — compile-time memory safety enforcement
- [Rust Mutex and Shared State](rust-mutex-and-shared-state.md) — avoiding deadlocks
- [Rust NewType Pattern](rust-new-type-pattern.md) — opt-in type safety
- [Rust RAII](rust-raii.md) — automatic resource management preventing leaks
