# Rust Traits and OOP Patterns

> Sources: Ardan Ultimate Rust Foundations, 2025
> Raw: [ardan-oop-patterns.md](../../raw/rust/ardan-oop-patterns.md)

## Overview

Rust is not an object-oriented language in the traditional sense — it doesn't have inheritance, and deeply nested object graphs often fight the borrow checker. Instead, Rust encourages composition over inheritance and organizing code around data ownership.

## The OOP Problem

Naively translating OOP patterns to Rust often fails:

```rust
struct Organization { pub people: Vec<Person> }
struct Person { pub resources: Vec<Resource> }

impl Person {
    fn give_resource(&mut self, name: &str, org: &mut Organization, recipient: usize) {
        // ERROR: cannot borrow self.resources as mutable and immutable simultaneously
        // ERROR: cannot borrow org as mutable more than once
    }
}
```

This violates the borrow checker's rule: you can't have a mutable borrow on `self` and a mutable borrow on `org` at the same time.

## The Rust Pattern: Move Ownership Up

Move the operation to the level that actually owns all of the parts:

```rust
impl Organization {
    fn move_resource(&mut self, from: usize, to: usize, name: &str) {
        if let Some(resource) = self.people[from].take_resource(name) {
            self.people[to].give_resource(resource);
        }
    }
}

impl Person {
    fn take_resource(&mut self, name: &str) -> Option<Resource> {
        let index = self.resources.iter().position(|r| r.name == name);
        index.map(|i| self.resources.remove(i))
    }

    fn give_resource(&mut self, resource: Resource) {
        self.resources.push(resource);
    }
}
```

What changed:
- `Organization` owns its workers and resources. A single mutable borrow gives full control.
- The operation is broken into two steps: `take_resource` then `give_resource`.
- The `move` semantic matches reality — there's only one of each resource.

## Adding Robust Error Handling

```rust
#[derive(Error, Debug)]
enum OrgError {
    #[error("Person {0} does not exist")]
    PersonDoesNotExist(usize),
    #[error("Resource not found")]
    ResourceNotFound,
}

impl Organization {
    fn move_resource(&mut self, from: usize, to: usize, name: &str) -> Result<(), OrgError> {
        if !self.has_person(from) { return Err(OrgError::PersonDoesNotExist(from)); }
        if !self.has_person(to) { return Err(OrgError::PersonDoesNotExist(to)); }
        let resource = self.people[from]
            .take_resource(name)
            .ok_or(OrgError::ResourceNotFound)?;
        self.people[to].give_resource(resource);
        Ok(())
    }
}
```

## Key Principles for Rust Data Design

1. **Move operations to the owner** — the struct that owns all the data should orchestrate operations on it.
2. **Break operations into small steps** — each step should have a single responsibility.
3. **Use IDs instead of references** — store a central collection and reference items by ID.
4. **Error handling is built-in** — `Result` types make error paths explicit at every step.

## See Also

- [Rust Traits](rust-traits.md) — trait fundamentals, default implementations, trait bounds, `dyn` dispatch
- [Rust Borrow Checker](rust-borrow-checker.md) — why OOP patterns conflict with Rust's rules
- [Rust Error Handling](rust-error-handling.md) — using `thiserror` for robust error types
- [Rust Structs](rust-structs.md) — defining data types
- [Rust Enums](rust-enums.md) — enum patterns for state management
