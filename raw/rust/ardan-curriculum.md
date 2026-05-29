# Ultimate Rust 1: Foundations

> Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
> Collected: 2026-05-29
> Published: 2025

Presented by [Ardan Labs](https://www.ardanlabs.com/), Ultima Rust: Foundations gives you a "zero to hero" class to get you started with Rust. You'll learn the basics of Rust, before diving into hands-on learning that can help you build a Rust foundation into your architecture. Take advantage of the speed and safety of Rust, tame the borrow and lifetime checkers, and pick up some tricks to help you become productive in Rust.

This is a four day class. Each day is 4 hours, with a short break at the end of each hour.

Classes are presented in a live-coding workshop environment. You are encouraged to code along, and keep this guide as a road map into Rust.

## Pre-Requisites

You need:

* Rust installed (via RustUp.rs)
* An IDE configured to use Rust Analyzer.
    * The instructor will use Visual Studio Code, so if you want to match the examples exactly with what you see, this is the recommended platform. It is [available free](https://code.visualstudio.com/download) for Mac, Windows and Linux.

You should also clone a copy of these notes for yourself:

```
git clone https://github.com/thebracket/ArdanUltimateRustFoundations.git
```

## Class Overview

**Day 1**

- Introduction
- Setup & Update Rust
- Visual Studio Code
- cargo init and "Hello World"
- Cargo Workspaces
- Hello Library
- Text Input & Better Unit Testing
- Enumerations/Unions
- Structures
- Arrays & Iterators
- Vectors
- HashMaps
- Serialization
- Hashing Passwords
- A CLI Application

**Day 2**

- Modules & Visibility
- Documentation
- Error Handling
- The Borrow Checker
- Lifetimes
- OOP Patterns
- RAII - Drop Cleanup
- CPU Bound Workload
- Racing Data
- Atomically Counting Primes
- Shared Data

**Day 3**

- Easy Concurrency with Rayon
- Async with Tokio
- TCP Server with Tokio
- Sending Receiving data - Channels
- Global Variables
- Synchronization Primitives
- Type Safety with NewTypes
- Basic Traits
- Generic Data Types
- More Complex Generic Data
- Constants & Constant Functions
- Macros
- Feature Flags

**Day 4**

- Simpler Locks: Parking Lot
- Avoiding Locks with DashMap
- Simple Benchmarks
- Complex Benchmarks - A Quick Visit
- Putting it together: a TCP login server
- A Simple Web Application
- How fast are our network services?
- Life without the Standard Library
- Rust's Safety Guarantees
- Wrap-Up
