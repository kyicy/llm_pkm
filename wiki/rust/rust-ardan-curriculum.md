# Ardan Ultimate Rust Foundations — Curriculum

> Sources: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025
> Raw: [ardan-curriculum.md](../../raw/rust/ardan-curriculum.md)

## Course Overview

Presented by Ardan Labs, Ultimate Rust: Foundations is a "zero to hero" workshop that covers Rust fundamentals through hands-on, live-coding sessions. The course walks through the borrow checker, lifetime system, concurrency, generics, and systems-level programming.

- **Format:** 4 days, 4 hours per day (live-coding workshop, short break each hour)
- **Instructor:** Ardan Labs team
- **Prerequisites:** Rust installed (via [rustup.rs](https://rustup.rs/)), VS Code with Rust Analyzer (or compatible IDE)

## Day 1: Core Rust

Basics of Rust: project setup, fundamental types, collections, serialization, and CLI applications.

- [x] **Class Introduction & Setup** — [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md)
- [x] **Hello World** — [Rust Hello World](rust-hello-world.md)
- [x] **Cargo Workspaces** — [Rust Cargo Workspaces](rust-cargo-workspaces.md)
- [ ] **Library Crates** — [Rust Library Crates](rust-library-crates.md)
- [ ] **Unit Testing** — [Rust Testing](rust-testing.md)
- [ ] **Enums** — [Rust Enums](rust-enums.md)
- [ ] **Structs** — [Rust Structs](rust-structs.md)
- [ ] **Arrays & Iterators** — [Rust Arrays and Slices](rust-arrays-and-slices.md)
- [ ] **Vectors** — [Rust Vectors](rust-vectors.md)
- [ ] **HashMaps** — [Rust Hashmaps](rust-hashmaps.md)
- [ ] **Serialization (Serde)** — [Rust Serde Serialization](rust-serde-serialization.md)
- [ ] **Password Hashing** — [Rust Password Hashing](rust-password-hashing.md)
- [ ] **CLI Application** — [Rust CLI Applications](rust-cli-applications.md)

## Day 2: Ownership & Concurrency

Modules, documentation, error handling, borrow checker, lifetimes, OOP patterns, RAII, threading, atomics, mutexes, and async concurrency.

- [ ] **Modules & Visibility** — [Rust Modules and Visibility](rust-modules-and-visibility.md)
- [ ] **Documentation** — [Rust Documentation](rust-documentation.md)
- [ ] **Error Handling** — [Rust Error Handling](rust-error-handling.md)
- [ ] **Borrow Checker** — [Rust Borrow Checker](rust-borrow-checker.md)
- [ ] **Lifetimes** — [Rust Lifetimes](rust-lifetimes.md)
- [ ] **OOP Patterns** — [Rust Traits and OOP](rust-traits-and-oop.md)
- [ ] **RAII / Drop Cleanup** — [Rust RAII](rust-raii.md)
- [ ] **CPU Bound Workload (Counting Primes)** — [Rust Threads and Concurrency](rust-threads-and-concurrency.md)
- [ ] **Data Races** — [Rust Threads and Concurrency](rust-threads-and-concurrency.md)
- [ ] **Atomic Operations** — [Rust Atomic Operations](rust-atomic-operations.md)
- [ ] **Shared State (Mutex)** — [Rust Mutex and Shared State](rust-mutex-and-shared-state.md)
- [ ] **Rayon (Easy Concurrency)** — [Rust Rayon](rust-rayon.md)
- [ ] **Async with Tokio** — [Rust Async and Tokio](rust-async-and-tokio.md)
- [ ] **TCP Server with Tokio** — [Rust TCP Server](rust-tcp-server.md)
- [ ] **Channels** — [Rust Channels](rust-channels.md)

## Day 3: Advanced Types & Generics

Global state, synchronization primitives, type-safe wrappers, traits, generic data structures, and compile-time computation.

- [ ] **Global Variables** — [Rust Constants](rust-constants.md)
- [ ] **Synchronization Primitives** — [Rust Mutex and Shared State](rust-mutex-and-shared-state.md)
- [ ] **NewType Pattern** — [Rust NewType Pattern](rust-new-type-pattern.md)
- [ ] **Traits** — [Rust Traits](rust-traits.md)
- [ ] **Generic Data Types** — [Rust Generic Data Structures](rust-generic-data-structures.md)
- [ ] **Complex Generics** — [Rust Generic Data Structures](rust-generic-data-structures.md)
- [ ] **Constants & `const fn`** — [Rust Constants](rust-constants.md)

## Day 4: Applications & Systems

Macros, conditional compilation, lock alternatives, benchmarking, web services, embedded, and safety guarantees.

- [ ] **Declarative Macros** — [Rust Macros](rust-macros.md)
- [ ] **Feature Flags** — [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md)
- [ ] **parking_lot (Simpler Locks)** — [Rust Mutex and Shared State](rust-mutex-and-shared-state.md)
- [ ] **DashMap** — [Rust DashMap](rust-dashmap.md)
- [ ] **Benchmarking** — [Rust Benchmarking](rust-benchmarking.md)
- [ ] **TCP Login Server** — [Rust TCP Server](rust-tcp-server.md)
- [ ] **Rocket Web Framework** — [Rust Rocket Web Framework](rust-rocket-web.md)
- [ ] **Network Benchmarking (Netbench)** — (no wiki article yet)
- [ ] **no_std (Life without std)** — [Rust Safety Guarantees](rust-safety-guarantees.md)
- [ ] **Rust's Safety Guarantees** — [Rust Safety Guarantees](rust-safety-guarantees.md)
- [ ] **Wrap-Up**
