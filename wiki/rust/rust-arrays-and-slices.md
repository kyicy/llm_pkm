# Rust Arrays and Slices

> Sources: Rust by Example, Unknown
> Raw: [arrays-and-slices.md](../../raw/rust/2026-05-29-arrays-and-slices.md)

## Overview

Arrays are fixed-size collections of same-type elements stored contiguously on the stack. Their length is known at compile time and is part of the type signature `[T; length]`. Slices are dynamically-sized views into arrays (or other contiguous sequences) represented as a two-word fat pointer (data pointer + length), with type signature `&[T]`.

## Arrays

### Declaration and Initialization

Arrays can be initialized with explicit elements or with a repeat expression:

```rust
let xs: [i32; 5] = [1, 2, 3, 4, 5];       // explicit elements
let ys: [i32; 500] = [0; 500];              // 500 zeros
```

### Properties

- Stack-allocated — size is known at compile time.
- Zero-based indexing: `xs[0]` for the first element.
- `.len()` returns the element count.
- `std::mem::size_of_val` reports the byte size.

### Safe Access with `.get()`

The `.get()` method returns an `Option<&T>`, enabling safe out-of-bounds handling:

```rust
for i in 0..xs.len() + 1 {
    match xs.get(i) {
        Some(xval) => println!("{}: {}", i, xval),
        None => println!("Slow down! {} is too far!", i),
    }
}
```

Out-of-bounds indexing with a constant index causes a **compile-time error**. Out-of-bounds indexing on a slice causes a **runtime panic**.

## Slices

A slice is a reference to a contiguous segment of an array (or other sequence). It is a two-word fat pointer:

- First word: pointer to the data
- Second word: length of the slice

The word size matches `usize` (e.g., 64 bits on x86-64).

### Borrowing Arrays as Slices

Arrays can be automatically borrowed as slices:

```rust
fn analyze_slice(slice: &[i32]) {
    println!("First element: {}", slice[0]);
    println!("Slice length: {}", slice.len());
}

analyze_slice(&xs);          // borrow entire array
analyze_slice(&ys[1..4]);    // borrow a section
```

### Range Syntax

Slices use the range syntax `[starting_index..ending_index]`, where `starting_index` is inclusive and `ending_index` is exclusive.

### Empty Slices

```rust
let empty_array: [u32; 0] = [];
assert_eq!(&empty_array, &[]);
assert_eq!(&empty_array, &[][..]); // equivalent
```

## See Also

- [Rust Primitives](rust-primitives.md) — overview of scalar and compound types
- [Rust Tuples](rust-tuples.md) — the other compound type
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — Debug formatting for arrays
