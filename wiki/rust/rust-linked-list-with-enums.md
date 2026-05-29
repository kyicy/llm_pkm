# Rust Linked List with Enums

> Sources: Rust by Example, Unknown
> Raw: [linked-list.md](../../raw/rust/2026-05-29-linked-list.md)

## Overview

Enums can model recursive data structures. A classic functional linked list uses an enum with two variants: `Cons` (a node containing an element and a pointer to the next node) and `Nil` (the end of the list). Methods are attached via `impl` blocks, using `match` to handle each variant.

## The Cons/Nil Pattern

```rust
enum List {
    Cons(u32, Box<List>),  // element + heap-allocated next node
    Nil,                    // end of list
}
```

`Box<List>` is required because `List` is recursive — without indirection, the compiler cannot determine the size of `List` at compile time. `Box` provides a fixed-size pointer stored on the stack, pointing to heap-allocated data.

## Methods on Enums

Methods use `match` to branch on the current variant:

```rust
impl List {
    fn new() -> List {
        Nil
    }

    fn prepend(self, elem: u32) -> List {
        Cons(elem, Box::new(self))
    }

    fn len(&self) -> u32 {
        match *self {
            Cons(_, ref tail) => 1 + tail.len(),
            Nil => 0,
        }
    }

    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => format!("{}, {}", head, tail.stringify()),
            Nil => format!("Nil"),
        }
    }
}
```

Key details:
- `*self` dereferences `&self` to match on the concrete type rather than a reference (preferred in Rust).
- `ref tail` takes a reference to the tail inside the `Cons` variant without taking ownership — required because `self` is borrowed.
- Recursive methods like `len()` and `stringify()` are non-tail-recursive and may overflow the stack for very long lists.

## Usage

```rust
let mut list = List::new();
list = list.prepend(1);
list = list.prepend(2);
list = list.prepend(3);

// linked list has length: 3
// 3, 2, 1, Nil
```

## See Also

- [Rust Enums](rust-enums.md) — enum variants, matching, and type aliases
- [Rust Structs](rust-structs.md) — alternative way to model list nodes
