# Life Without the Standard Library

- Source: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025 (course)
- Collected: 2026-05-29
- Published: 2025

We're not going to dive into this in-depth, but you should be aware that just occasionally you need to work without the standard library. You might be working on a Linux kernel module, a tiny embedded system or similar.

You can make very small binaries, and interface with your platforms libraries---but you've lost a lot of the collections and magic that make using Rust easy.

This is an advanced topic, I mostly wanted you to know that it exists. Rust is a true systems language - you can build an operating system with it if you want!
