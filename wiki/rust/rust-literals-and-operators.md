# Rust Literals and Operators

> Sources: Rust by Example, Unknown
> Raw: [literals-and-operators.md](../../raw/rust/2026-05-29-literals-and-operators.md)

## Overview

Rust supports literals for all primitive types and a set of operators with C-like precedence. Integers can be expressed in multiple bases (decimal, hex, octal, binary), and numeric literals support underscores for readability and scientific E-notation for floats.

## Numeric Literals

### Integer Literals by Base

| Base | Prefix | Example |
|------|--------|---------|
| Decimal | (none) | `69420` |
| Hexadecimal | `0x` | `0x10f2c` |
| Octal | `0o` | `0o207454` |
| Binary | `0b` | `0b10000111100101100` |

### Type Suffixes

Literal types can be specified with suffixes: `1u32`, `1i32`, `1u8`, etc. Without a suffix, integers default to `i32` and floats to `f64`.

### Readability and Notation

Underscores improve readability in large numbers:

```rust
let million = 1_000_000u32;    // same as 1000000
let small  = 0.000_001;        // same as 0.000001
```

Scientific E-notation is supported for floats (`1e6`, `7.6e-4`), with the resulting type being `f64`.

### Other Literal Types

- Characters: `'a'`
- Strings: `"abc"`
- Booleans: `true`, `false`
- Unit type: `()`

## Operators

### Arithmetic Operators

Standard arithmetic: `+`, `-`, `*`, `/`, `%`. Types matter — subtracting two unsigned integers that result in a negative value causes a compile-time error:

```rust
println!("1 - 2 = {}", 1i32 - 2);  // works (-1)
// println!("{}", 1u32 - 2);       // compile error: overflow
```

### Boolean Operators

Short-circuiting logical operators: `&&` (AND), `||` (OR), `!` (NOT).

### Bitwise Operators

```rust
0b0011u32 & 0b0101   // AND  → 0b0001
0b0011u32 | 0b0101   // OR   → 0b0111
0b0011u32 ^ 0b0101   // XOR  → 0b0110
1u32 << 5             // left shift
0x80u32 >> 2          // right shift
```

### Operator Precedence

Operator precedence in Rust is similar to C-like languages. The full reference is available in the [Rust Reference](https://doc.rust-lang.org/reference/expressions.html#expression-precedence).

## See Also

- [Rust Primitives](rust-primitives.md) — the types these literals represent
- [Rust Printing and Formatting](rust-printing-and-formatting.md) — format specifiers for numeric output (`{:b}`, `{:x}`, `{:04b}`)
