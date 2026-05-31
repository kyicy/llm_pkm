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
- [x] **Library Crates** — [Rust Library Crates](rust-library-crates.md)
- [x] **Unit Testing** — [Rust Testing](rust-testing.md)
- [x] **Enums** — [Rust Enums](rust-enums.md)
- [x] **Structs** — [Rust Structs](rust-structs.md)
- [x] **Arrays & Iterators** — [Rust Arrays and Slices](rust-arrays-and-slices.md)
- [x] **Vectors** — [Rust Vectors](rust-vectors.md)
- [x] **HashMaps** — [Rust Hashmaps](rust-hashmaps.md)
- [x] **Serialization (Serde)** — [Rust Serde Serialization](rust-serde-serialization.md)
- [x] **Password Hashing** — [Rust Password Hashing](rust-password-hashing.md)
- [x] **CLI Application** — [Rust CLI Applications](rust-cli-applications.md)
<!-- Day 1 Exam: 100/100 PASSED -->

## Day 2: Ownership & Concurrency

Modules, documentation, error handling, borrow checker, lifetimes, OOP patterns, RAII, threading, atomics, mutexes, and async concurrency.

- [x] **Modules & Visibility** — [Rust Modules and Visibility](rust-modules-and-visibility.md)
- [x] **Documentation** — [Rust Documentation](rust-documentation.md)
- [x] **Error Handling** — [Rust Error Handling](rust-error-handling.md)
- [x] **Borrow Checker** — [Rust Borrow Checker](rust-borrow-checker.md)
- [x] **Lifetimes** — [Rust Lifetimes](rust-lifetimes.md)
- [x] **OOP Patterns** — [Rust Traits and OOP](rust-traits-and-oop.md)
- [x] **RAII / Drop Cleanup** — [Rust RAII](rust-raii.md)
- [x] **CPU Bound Workload (Counting Primes)** — [Rust Threads and Concurrency](rust-threads-and-concurrency.md)
- [x] **Data Races** — [Rust Threads and Concurrency](rust-threads-and-concurrency.md)
- [x] **Atomic Operations** — [Rust Atomic Operations](rust-atomic-operations.md)
- [x] **Shared State (Mutex)** — [Rust Mutex and Shared State](rust-mutex-and-shared-state.md)
- [x] **Rayon (Easy Concurrency)** — [Rust Rayon](rust-rayon.md)
- [x] **Async with Tokio** — [Rust Async and Tokio](rust-async-and-tokio.md)
- [x] **TCP Server with Tokio** — [Rust TCP Server](rust-tcp-server.md)
- [x] **Channels** — [Rust Channels](rust-channels.md)
<!-- Day 2 Exam: 100/100 PASSED -->

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


## See Also

- [Hello World](rust-hello-world.md)
- [Printing and Formatting](rust-printing-and-formatting.md)
- [Primitives](rust-primitives.md)
- [Literals and Operators](rust-literals-and-operators.md)
- [Tuples](rust-tuples.md)
- [Arrays and Slices](rust-arrays-and-slices.md)
- [Custom Types](rust-custom-types.md)
- [Structs](rust-structs.md)
- [Enums](rust-enums.md)
- [Constants](rust-constants.md)
- [Comments](rust-comments.md)
- [Linked List with Enums](rust-linked-list-with-enums.md)
- [RAII](rust-raii.md)
- [Borrow Checker](rust-borrow-checker.md)
- [Lifetimes](rust-lifetimes.md)
- [Macros](rust-macros.md)
- [Error Handling](rust-error-handling.md)
- [Modules and Visibility](rust-modules-and-visibility.md)
- [Vectors](rust-vectors.md)
- [Hashmaps](rust-hashmaps.md)
- [Generic Data Structures](rust-generic-data-structures.md)
- [Traits](rust-traits.md)
- [Traits and OOP](rust-traits-and-oop.md)
- [Library Crates](rust-library-crates.md)
- [Cargo and Project Setup](rust-cargo-and-project-setup.md)
- [Cargo Workspaces](rust-cargo-workspaces.md)
- [Documentation](rust-documentation.md)
- [Testing](rust-testing.md)
- [Benchmarking](rust-benchmarking.md)
- [CLI Applications](rust-cli-applications.md)
- [Serde Serialization](rust-serde-serialization.md)
- [Safety Guarantees](rust-safety-guarantees.md)
- [Threads and Concurrency](rust-threads-and-concurrency.md)
- [Channels](rust-channels.md)
- [Mutex and Shared State](rust-mutex-and-shared-state.md)
- [Atomic Operations](rust-atomic-operations.md)
- [DashMap](rust-dashmap.md)
- [Rayon](rust-rayon.md)
- [Async and Tokio](rust-async-and-tokio.md)
- [Rocket Web](rust-rocket-web.md)
- [TCP Server](rust-tcp-server.md)
- [Password Hashing](rust-password-hashing.md)
- [New Type Pattern](rust-new-type-pattern.md)
