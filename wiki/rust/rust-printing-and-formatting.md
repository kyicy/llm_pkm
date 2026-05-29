# Rust Printing and Formatting

> Sources: Rust by Example, Unknown
> Raw: [formatted-print.md](../../raw/rust/formatted-print.md); [formatting.md](../../raw/rust/formatting.md); [debug.md](../../raw/rust/debug.md); [display.md](../../raw/rust/display.md); [testcase-list.md](../../raw/rust/testcase-list.md)

## Overview

Rust's printing and formatting system is built on the `std::fmt` module, which provides a set of macros and traits for text output. The system performs compile-time format string validation — incorrect argument counts or types produce compiler errors. Key formatting traits include `Debug` (auto-derivable, uses `{:?}`) and `Display` (manually implemented, uses `{}`).

## Print Macros

Rust provides five core formatting macros, all sharing the same format string syntax:

| Macro | Output Target | Newline |
|-------|--------------|---------|
| `format!` | Returns a `String` | No |
| `print!` | stdout (`io::stdout`) | No |
| `println!` | stdout (`io::stdout`) | Yes |
| `eprint!` | stderr (`io::stderr`) | No |
| `eprintln!` | stderr (`io::stderr`) | Yes |

## Format String Syntax

### Positional and Named Arguments

Arguments can be referenced by position or name:

```rust
println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");
println!("{subject} {verb} {object}", object="the lazy dog",
         subject="the quick brown fox", verb="jumps over");
```

### Numeric Format Specifiers

Rust supports formatting numbers in different bases:

| Specifier | Base | Example (`69420`) |
|-----------|------|-------------------|
| `{}` | Decimal | `69420` |
| `{:b}` | Binary | `10000111100101100` |
| `{:o}` | Octal | `207454` |
| `{:x}` | Lower hex | `10f2c` |
| `{:X}` | Upper hex | `10F2C` |

### Width and Padding

Values can be padded and aligned:

```rust
println!("{number:>5}", number=1);   // "    1" (right-align, width 5)
println!("{number:0>5}", number=1);  // "00001" (right-align, zero-padded)
println!("{number:0<5}", number=1);  // "10000" (left-align)
println!("{number:0>width$}", number=1, width=5); // dynamic width
```

### Capturing Variables (Rust 1.58+)

Variables from the surrounding scope can be captured directly:

```rust
let number: f64 = 1.0;
let width: usize = 5;
println!("{number:>width$}");
```

## Formatting Traits

Formatting is trait-based. Each format specifier maps to a trait:

| Trait | Marker | Description |
|-------|--------|-------------|
| `Display` | `{}` | User-friendly output, must be manually implemented |
| `Debug` | `{:?}` | Debug output, can be auto-derived |
| `Binary` | `{:b}` | Binary representation |
| `Octal` | `{:o}` | Octal representation |
| `LowerHex` | `{:x}` | Lowercase hexadecimal |
| `UpperHex` | `{:X}` | Uppercase hexadecimal |

### Debug (`fmt::Debug`)

The `Debug` trait can be auto-derived for any struct using `#[derive(Debug)]`. All standard library types implement it. Pretty printing is available with `{:#?}`:

```rust
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}
println!("{:#?}", peter); // pretty-printed output
```

`Debug` is the only formatting trait available for generic containers like `Vec<T>`, since `Display` cannot be meaningfully implemented for them.

### Display (`fmt::Display`)

`Display` must be manually implemented for custom types. It produces cleaner, user-facing output:

```rust
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}
```

Implementing `Display` automatically provides the `ToString` trait, enabling `.to_string()` on the type.

### Sequential Display with `?` Operator

For types containing collections (e.g., a `Vec` wrapper), the `?` operator propagates `fmt::Result` errors through sequential `write!` calls:

```rust
impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "[")?;
        for (index, v) in self.0.iter().enumerate() {
            if index != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }
        write!(f, "]")
    }
}
```

## See Also

- [Rust Hello World](rust-hello-world.md) — introduces `println!` macro
- [Rust Primitives](rust-primitives.md) — types being formatted
- [Rust Literals and Operators](rust-literals-and-operators.md) — numeric format specifiers (`{:b}`, `{:x}`, `{:04b}`)
