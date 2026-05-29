# The Dreaded Borrow Checker

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

To understand the borrow checker, you need to internalize some rules:

* Rust assumes that all programs may be multi-threaded.
* Only one thing at a time may *ever* have mutable (write) access to a variable.
* Any number of things may have *read only* access to a variable — but only if nothing can currently write to it.

This is generally good advice:
* Keep it simple.
* Keep a really obvious data-path through which data may be modified.
* Don't use Rust as an object-oriented language. It isn't one. You won't have much trouble if you combine simple data types and retain a store associating types with types.
* You *will* have a miserable time if you implement a bunch of functionality-specific traits, mix and match them, and store them in a giant, C++ style common object store.
