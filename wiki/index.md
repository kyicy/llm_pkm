# Knowledge Base Index

## learning

Study techniques, learning methods, and skill acquisition.

| Article | Summary | Updated |
|---------|---------|---------|
| [Feynman Technique](learning/feynman-technique.md) | Four-step learning method: explain concepts simply to reveal true understanding | 2026-05-29 |

## mathematics

Single and multivariable calculus, linear algebra, and related mathematical topics.

| Article | Summary | Updated |
|---------|---------|---------|
| [MIT 18.01 Unit 1: Derivatives](mathematics/mit-18.01-unit1-derivatives.md) | Definition and computation of derivatives, limits, differentiation rules, implicit differentiation, exponentials, logs, and hyperbolic functions | 2026-05-29 |
| [MIT 18.01 Unit 2: Applications of Differentiation](mathematics/mit-18.01-unit2-applications-of-differentiation.md) | Linear and quadratic approximations, curve sketching, optimization, related rates, Newton's method, MVT, antiderivatives, and separation of variables | 2026-05-29 |
| [MIT 18.01 Unit 3: The Definite Integral](mathematics/mit-18.01-unit3-definite-integrals.md) | Riemann sums, FTC 1 & 2, areas between curves, volumes of revolution, average value, Gaussian integral, and numerical integration | 2026-05-29 |
| [MIT 18.01 Unit 4: Techniques of Integration and Series](mathematics/mit-18.01-unit4-integration-and-series.md) | Trig integrals and substitution, partial fractions, integration by parts, arc length, polar coordinates, L'Hôpital's rule, improper integrals, and Taylor series | 2026-05-29 |
| [MIT 18.01 — Curriculum](mathematics/mit-18.01-curriculum.md) | Full 38-lecture curriculum map for MIT Single Variable Calculus, organized by unit with linked lectures, key skills, and highlights | 2026-05-29 |

## ai

Artificial intelligence, agents, and related topics.

| Article | Summary | Updated |
|---------|---------|---------|
| [AI Agents in Software Development](ai/ai-agents-in-software-development.md) | George Hotz argues that AI coding agents cannot truly program and that their widespread adoption in software development... | Unknown |

## knowledge-management

Personal knowledge management systems and methodologies.

| Article | Summary | Updated |
|---------|---------|---------|
| [LLM-Maintained Knowledge Bases](knowledge-management/llm-maintained-knowledge-bases.md) | Instead of RAG-style retrieval where an LLM re-discovers knowledge from raw documents on every query, the LLM Wiki patte... | Unknown |

## rust

Rust programming language topics from the Ardan Ultimate Rust Foundations curriculum.

| Article | Summary | Updated |
|---------|---------|---------|
| [Ardan Ultimate Rust Foundations — Curriculum](rust/rust-ardan-curriculum.md) | Presented by Ardan Labs, Ultimate Rust: Foundations is a "zero to hero" workshop that covers Rust fundamentals through h... | Unknown |
| [Rust Arrays and Slices](rust/rust-arrays-and-slices.md) | Arrays are fixed-size collections of same-type elements stored contiguously on the stack. Their length is known at compi... | Unknown |
| [Rust Async and Tokio](rust/rust-async-and-tokio.md) | Rust's async/await model enables *cooperative multitasking* for I/O-bound workloads. Unlike OS threads, async tasks ("gr... | Unknown |
| [Rust Atomic Operations](rust/rust-atomic-operations.md) | Atomic variables provide thread-safe operations on primitive types without locks. They are typically implemented directl... | Unknown |
| [Rust Benchmarking](rust/rust-benchmarking.md) | Rust offers several approaches to benchmarking, from quick timing with `std::time::Instant` to full-featured benchmark s... | Unknown |
| [Rust Borrow Checker](rust/rust-borrow-checker.md) | The borrow checker enforces Rust's ownership rules at compile time. It ensures memory safety without a garbage collector... | Unknown |
| [Rust Cargo and Project Setup](rust/rust-cargo-and-project-setup.md) | Cargo is Rust's build system and package manager. It handles compilation, dependency management, testing, documentation ... | Unknown |
| [Rust Cargo Workspaces](rust/rust-cargo-workspaces.md) | Cargo workspaces allow you to manage multiple related packages under a single project root. All member packages share a ... | Unknown |
| [Rust Channels](rust/rust-channels.md) | Channels provide a way to communicate between threads or async tasks by sending messages. Rust offers both standard libr... | Unknown |
| [Rust CLI Applications](rust/rust-cli-applications.md) | Rust is well-suited for building command-line applications. The standard library provides basic argument parsing via `st... | Unknown |
| [Rust Comments](rust/rust-comments.md) | Rust supports two categories of comments: regular comments (ignored by the compiler) and documentation comments (parsed ... | Unknown |
| [Rust Constants](rust/rust-constants.md) | Rust provides two keywords for declaring named constants in any scope, including globally: `const` for immutable values ... | Unknown |
| [Rust Crate Root](rust/rust-crate-root.md) | Every crate has a root file (`lib.rs` or `main.rs`) — the entry point that defines the module tree. `crate` is a keyword referring to this root | 2026-05-30 |
| [Rust Custom Types](rust/rust-custom-types.md) | Rust provides two primary keywords for defining custom data types — `struct` for structures and `enum` for enumerations ... | Unknown |
| [Rust DashMap](rust/rust-dashmap.md) | `DashMap<K, V>` is a lock-free concurrent hash map that provides safe concurrent access from multiple threads without ex... | Unknown |
| [Rust Documentation](rust/rust-documentation.md) | Rust has built-in documentation tooling. Documentation comments use Markdown and can include code examples that are auto... | Unknown |
| [Rust Enums](rust/rust-enums.md) | The `enum` keyword creates a type that can be one of several distinct variants. Each variant can carry different kinds a... | Unknown |
| [Rust Error Handling](rust/rust-error-handling.md) | Rust does not have exceptions. Errors are values represented by types implementing the standard `Error` trait. Functions... | Unknown |
| [Rust Generic Data Structures](rust/rust-generic-data-structures.md) | Rust supports generic data structures — types parameterized by one or more type variables. This enables reusable, type-s... | Unknown |
| [Rust Hashmaps](rust/rust-hashmaps.md) | `HashMap<K, V>` stores key-value pairs and provides O(1) average-case lookup. It is the Rust equivalent of dictionaries ... | Unknown |
| [Rust Hello World](rust/rust-hello-world.md) | The traditional Hello World program in Rust demonstrates the basic structure of a Rust program: a `main()` function that... | Unknown |
| [Rust Library Crates](rust/rust-library-crates.md) | A library crate is a package designed to be shared and used by other programs, rather than executed directly. Library cr... | Unknown |
| [Rust Lifetimes](rust/rust-lifetimes.md) | Lifetimes ensure that references are always valid — they prevent using a pointer after the data it points to has been fr... | Unknown |
| [Rust Linked List with Enums](rust/rust-linked-list-with-enums.md) | Enums can model recursive data structures. A classic functional linked list uses an enum with two variants: `Cons` (a no... | Unknown |
| [Rust Literals and Operators](rust/rust-literals-and-operators.md) | Rust supports literals for all primitive types and a set of operators with C-like precedence. Integers can be expressed ... | Unknown |
| [Rust Macros](rust/rust-macros.md) | Macros are Rust's way of letting you change the syntax of the language. There are two types: **declarative macros** (`ma... | Unknown |
| [Rust Modules and Visibility](rust/rust-modules-and-visibility.md) | Modules group code into namespaces and enforce privacy boundaries. They are the primary mechanism for organizing Rust co... | Unknown |
| [Rust Mutex and Shared State](rust/rust-mutex-and-shared-state.md) | `Mutex<T>` provides mutual exclusion for shared mutable data — ensuring that only one thread at a time can access the pr... | Unknown |
| [Rust NewType Pattern](rust/rust-new-type-pattern.md) | The NewType pattern uses a tuple struct with a single field to create a distinct type from an existing one. This provide... | Unknown |
| [Rust Password Hashing](rust/rust-password-hashing.md) | Storing passwords in plain text is a security risk. Rust provides the `sha2` crate (among others) for hashing passwords ... | Unknown |
| [Rust Primitives](rust/rust-primitives.md) | Rust provides a rich set of primitive types divided into scalar types (single values) and compound types (collections of... | Unknown |
| [Rust Printing and Formatting](rust/rust-printing-and-formatting.md) | Rust's printing and formatting system is built on the `std::fmt` module, which provides a set of macros and traits for t... | Unknown |
| [Rust RAII (Resource Acquisition Is Initialization)](rust/rust-raii.md) | RAII is a pattern where resources are acquired during initialization and released automatically when the object goes out... | Unknown |
| [Rust Rayon](rust/rust-rayon.md) | Rayon is a data-parallelism library for Rust that makes it easy to convert sequential iterator chains into parallel comp... | Unknown |
| [Rust Rocket Web Framework](rust/rust-rocket-web.md) | Rocket is a simple, fast web framework for Rust. It uses attribute macros for routing and has built-in support for JSON,... | Unknown |
| [Rust Safety Guarantees](rust/rust-safety-guarantees.md) | Rust provides strong safety guarantees, but they have specific bounds. Understanding what Rust *does* and *does not* gua... | Unknown |
| [Rust Serde Serialization](rust/rust-serde-serialization.md) | Serde is Rust's framework for serialization and deserialization. It is format-agnostic — you pair it with a format crate... | Unknown |
| [Rust Structs](rust/rust-structs.md) | Rust supports three kinds of structs via the `struct` keyword: classic C-like structs with named fields, tuple structs (... | Unknown |
| [Rust TCP Server](rust/rust-tcp-server.md) | Tokio provides async TCP networking primitives — `TcpListener` for accepting connections and `TcpStream` for sending/rec... | Unknown |
| [Rust Testing](rust/rust-testing.md) | Rust has a built-in testing framework. Tests are Rust functions annotated with `#[test]`, typically organized into a `te... | Unknown |
| [Rust Threads and Concurrency](rust/rust-threads-and-concurrency.md) | Rust provides OS threads through the standard library's `std::thread` module. The borrow checker enforces thread safety ... | Unknown |
| [Rust Traits and OOP Patterns](rust/rust-traits-and-oop.md) | Rust is not an object-oriented language in the traditional sense — it doesn't have inheritance, and deeply nested object... | Unknown |
| [Rust Traits](rust/rust-traits.md) | Traits are Rust's mechanism for defining shared behavior — similar to interfaces in other languages. They describe a set... | Unknown |
| [Rust Tuples](rust/rust-tuples.md) | Tuples are compound types that collect values of different types into a single value. They are constructed with parenthe... | Unknown |
| [Rust Vectors](rust/rust-vectors.md) | `Vec<T>` is a heap-allocated, resizable array type. It stores elements contiguously in memory and supports adding and re... | Unknown |

## security

Software security, supply chain attacks, and defensive practices.

| Article | Summary | Updated |
|---------|---------|---------|
| [Supply Chain Attack Prevention](security/supply-chain-attack-prevention.md) | Supply chain attacks via package managers and editor extensions have become increasingly common in 2026. The core defens... | Unknown |

