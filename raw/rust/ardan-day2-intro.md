# Day 2

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Yesterday, we learned a lot of the basics of Rust: workspaces, applications and libraries, importing dependencies, enumerations, structures, arrays, vectors, HashMaps, serialization, hashing passwords, and a full CLI application using `clap`.

Today, we're going to start putting our knowledge of the basic language to work:

* Modules, Visibility and Organizing Your Code.
* Error Handling
* The Borrow Checker
* Lifetimes
* Resource Acquisition is Initialization

Then, we're going to dive into Rust's promises of *Fearless Concurrency*:

* Build a CPU-bound workload.
* Take a look at a couple of other languages that have race condition problems.
* Build the same program in Rust, and see how Rust saves our bacon.
* Use *atomics* for thread-safe primitive variables.
* Use `Rayon` to introduce really easy parallel programming for CPU-bound workloads.
* Use `async` and `Tokio` to build a TCP networking server.
