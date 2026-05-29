# Knowledge Base Index

## ai

AI and LLM capabilities, limitations, and their impact on software development.

| Article | Summary | Updated |
|---------|---------|---------|
| [AI Agents in Software Development](ai/ai-agents-in-software-development.md) | George Hotz's critique: AI coding agents cannot truly program and their adoption will harm software quality, especially in large organizations | 2026-05-29 |

## knowledge-management

Techniques and patterns for organizing personal knowledge using LLMs.

| Article | Summary | Updated |
|---------|---------|---------|
| [LLM-Maintained Knowledge Bases](knowledge-management/llm-maintained-knowledge-bases.md) | Karpathy's pattern: LLMs incrementally build and maintain a compounding wiki, with humans curating sources and asking questions | 2026-05-29 |

## rust

Rust programming language fundamentals: program structure, type system, custom types, memory safety, error handling, concurrency, and async programming.

| Article | Summary | Updated |
|---------|---------|---------|
| [Rust Hello World](rust/rust-hello-world.md) | Basic Rust program structure: main function, println! macro, cargo new, debug vs release, Cargo.toml structure, macros | 2026-05-29 |
| [Rust Comments](rust/rust-comments.md) | Line comments, block comments, and doc comments (///, //!) in Rust | 2026-05-28 |
| [Rust Cargo and Project Setup](rust/rust-cargo-and-project-setup.md) | Cargo commands, --vcs flag, Cargo.toml structure, editions, feature flags, #[cfg(feature)], debug vs release builds | 2026-05-29 |
| [Rust Cargo Workspaces](rust/rust-cargo-workspaces.md) | Workspace configuration, workspace members, shared dependencies, batch commands | 2026-05-29 |
| [Rust Library Crates](rust/rust-library-crates.md) | lib.rs vs main.rs, pub visibility, path dependencies, importing libraries, module organization | 2026-05-29 |
| [Rust Modules and Visibility](rust/rust-modules-and-visibility.md) | Module types (block, file, directory), pub/pub(crate), re-exporting, preludes | 2026-05-29 |
| [Rust Documentation](rust/rust-documentation.md) | Doc comments (///, //!), cargo doc, doc tests, missing_docs warnings | 2026-05-29 |
| [Rust Testing](rust/rust-testing.md) | #[test], #[cfg(test)], mod tests, assert_eq!/assert!, doc tests, nightly #[bench] with Bencher, Criterion setup | 2026-05-29 |
| [Rust Printing and Formatting](rust/rust-printing-and-formatting.md) | Rust's std::fmt system: print macros, format string syntax, Debug and Display traits, combined format specifiers | 2026-05-29 |
| [Rust Primitives](rust/rust-primitives.md) | Scalar types (integers, floats, char, bool, unit) and compound types (arrays, tuples), atomics, Mutex | 2026-05-29 |
| [Rust Literals and Operators](rust/rust-literals-and-operators.md) | Numeric literals in multiple bases, type suffixes, underscores, E-notation, and arithmetic/boolean/bitwise operators | 2026-05-29 |
| [Rust Error Handling](rust/rust-error-handling.md) | Result, ? operator, Box<dyn Error>, anyhow, thiserror, map_err, error types comparison | 2026-05-29 |
| [Rust Arrays and Slices](rust/rust-arrays-and-slices.md) | Fixed-size stack-allocated arrays and dynamically-sized slice views, array-of-structs, parallel iteration | 2026-05-29 |
| [Rust Tuples](rust/rust-tuples.md) | Heterogeneous value collections, destructuring, tuple indexing, nesting, one-element tuples, and tuple structs | 2026-05-29 |
| [Rust Vectors](rust/rust-vectors.md) | Heap-allocated, resizable arrays: Vec, vec! macro, adding/removing elements, capacity vs length, JoinHandles | 2026-05-29 |
| [Rust Hashmaps](rust/rust-hashmaps.md) | HashMap key-value storage, entry API, transforming vectors to maps, performance comparison with Vec | 2026-05-29 |
| [Rust Generic Data Structures](rust/rust-generic-data-structures.md) | Generic types, StableVec&lt;T&gt; with Vec&lt;Option&lt;T&gt;&gt;, Index trait, complex generics with where bounds, custom trait requirements | 2026-05-29 |
| [Rust Custom Types](rust/rust-custom-types.md) | Overview of struct, enum, const/static, traits, NewType pattern, and generic data structures | 2026-05-29 |
| [Rust Structs](rust/rust-structs.md) | C-like structs, tuple structs, unit structs, field init shorthand, constructors, Clone derive, slices, iterators, map/find patterns | 2026-05-29 |
| [Rust Enums](rust/rust-enums.md) | Enum variants (unit-like, tuple-like, struct-like), matching, type aliases, C-like discriminators, use imports, enum methods, function pointers, closures | 2026-05-29 |
| [Rust NewType Pattern](rust/rust-new-type-pattern.md) | Tuple struct wrappers for type safety, From/Into traits, generic functions with trait bounds, operator overloading | 2026-05-29 |
| [Rust Constants](rust/rust-constants.md) | `const` vs `static`, `const fn` compile-time evaluation, `#[cfg]` conditional compilation, lazy singletons with `once_cell`, safe shared statics with `Mutex`/`AtomicUsize` | 2026-05-29 |
| [Rust Linked List with Enums](rust/rust-linked-list-with-enums.md) | Functional-style Cons/Nil linked list using enums, Box indirection, and enum methods | 2026-05-29 |
| [Rust Borrow Checker](rust/rust-borrow-checker.md) | Ownership rules, borrowing rules, data race prevention (C++/Go/Rust comparison) | 2026-05-29 |
| [Rust Lifetimes](rust/rust-lifetimes.md) | Lifetime annotations, elision, struct lifetimes, Rc, RefCell, interior mutability, performance overhead | 2026-05-29 |
| [Rust RAII](rust/rust-raii.md) | Drop trait, RAII pattern, File and resource management, custom RAII wrappers | 2026-05-29 |
| [Rust Traits](rust/rust-traits.md) | Custom traits, default implementations, trait bounds with `+`, `dyn` trait objects, supertraits, `Any` downcasting | 2026-05-29 |
| [Rust Traits and OOP](rust/rust-traits-and-oop.md) | Redesigning OOP patterns for Rust, moving ownership to the owner, error handling with thiserror | 2026-05-29 |
| [Rust Serde Serialization](rust/rust-serde-serialization.md) | Serde framework, derive(Serialize/Deserialize), JSON serialization, pretty-printing, file I/O with RAII | 2026-05-29 |
| [Rust Password Hashing](rust/rust-password-hashing.md) | sha2 crate, SHA-256 hashing, password hashing at construction, hash comparison for login | 2026-05-29 |
| [Rust CLI Applications](rust/rust-cli-applications.md) | Clap derive-based CLI, subcommands, user management (CRUD), formatted output, colored output | 2026-05-29 |
| [Rust Threads and Concurrency](rust/rust-threads-and-concurrency.md) | std::thread::spawn, move closures, data races, CPU-bound workloads, managing multiple threads | 2026-05-29 |
| [Rust Atomic Operations](rust/rust-atomic-operations.md) | AtomicUsize, fetch_add, Ordering, multi-threaded prime counting | 2026-05-29 |
| [Rust Mutex and Shared State](rust/rust-mutex-and-shared-state.md) | Mutex<T>, RwLock, parking_lot, deadlock patterns, lock best practices, per-thread results via JoinHandle<T> | 2026-05-29 |
| [Rust Rayon](rust/rust-rayon.md) | Parallel iterators (par_iter, into_par_iter), work-stealing thread pool, scope-based task spawning | 2026-05-29 |
| [Rust Async and Tokio](rust/rust-async-and-tokio.md) | async/await, Tokio runtime, green threads vs OS threads, join!, spawn, blocking, spawn_blocking, green thread batching, TCP connection reuse, connection limits | 2026-05-29 |
| [Rust Channels](rust/rust-channels.md) | mpsc (std and Tokio), broadcast channels, async and thread communication patterns | 2026-05-29 |
| [Rust TCP Server](rust/rust-tcp-server.md) | TcpListener, TcpStream, async echo server, RPC with serde, bincode binary encoding, LoginClient connection reuse, login server example | 2026-05-29 |
| [Rust Macros](rust/rust-macros.md) | Declarative macros (macro_rules!), $ variables, expr/ident types, repeating $()+, #[macro_export], macro recursion, hygiene | 2026-05-29 |
| [Rust Benchmarking](rust/rust-benchmarking.md) | Instant timing, nightly #[bench] with Bencher, Criterion setup, HTML reports, dev-dependencies | 2026-05-29 |
| [Rust DashMap](rust/rust-dashmap.md) | Lock-free DashMap<K,V>, get_mut/insert, concurrent readers+writers, trade-offs vs Mutex<HashMap>, Lazy singleton pattern | 2026-05-29 |
| [Rust Rocket Web Framework](rust/rust-rocket-web.md) | #[get]/#[post] routes, JSON with rocket::serde, static file serving, Rocket + Tokio TcpStream microservice integration | 2026-05-29 |
| [Rust Safety Guarantees](rust/rust-safety-guarantees.md) | Memory safety vs thread safety vs type safety, unsafe meaning, cargo audit, #![no_std] for embedded/kernel | 2026-05-29 |
| [Ardan Ultimate Rust Foundations — Curriculum](rust/rust-ardan-curriculum.md) | Course curriculum overview with cross-references: 4-day Ardan Labs Rust course covering core Rust, ownership, concurrency, generics, and systems programming | 2026-05-29 |

## security

Software supply chain security, attack prevention, and tooling configurations.

| Article | Summary | Updated |
|---------|---------|---------|
| [Supply Chain Attack Prevention](security/supply-chain-attack-prevention.md) | Cooldown mechanisms for package managers and editor extensions to mitigate supply chain attacks | 2026-05-28 |
