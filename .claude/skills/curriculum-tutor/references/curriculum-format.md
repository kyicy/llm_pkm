# Curriculum File Format

A curriculum file is a markdown document that defines a structured learning path. It organizes topics into days (or modules) with checklist items and links to wiki articles.

## Format Specification

### Overall Structure

```markdown
# Title — Subtitle

> Sources: Source Name (source-id), Year
> Raw: [source-file.md](../../raw/topic/source-file.md)

## Course Overview

Description of the curriculum. What it covers, format, prerequisites, etc.

## Day N: Day Title

Description of what this day covers.

- [ ] **Topic Title** — [Linked Article](linked-article.md)
- [ ] **Another Topic** — [Another Article](another-article.md)
- [x] **Completed Topic** — [Completed Article](completed-article.md)
<!-- Day N Exam: 100/100 PASSED -->

## Day N+1: Next Day Title

Description...

- [ ] **Next Topic** — [Next Article](next-article.md)
```

### Required Elements

| Element | Format | Required |
|---------|--------|----------|
| Title | `# Title` | Yes |
| Day heading | `## Day N: Title` | Yes (or `## Module N: Title`) |
| Topic item | `- [ ] **Topic Name** — [Link](file.md)` | Yes |
| Completed item | `- [x] **Topic Name** — [Link](file.md)` | Optional |
| Exam result | `<!-- Day N Exam: SCORE/100 PASSED -->` | Optional (auto-added by tutor) |

### Naming Conventions

- **Day headings** use `## Day N: Descriptive Title`. `Day` can be replaced with `Module`, `Week`, `Section`, or `Part`.
- **Topic items** use bold `**Topic Name**` followed by ` — ` (space, em-dash, space) and a markdown link to the wiki article.
- **Wiki article links** are relative paths from the curriculum file's directory to the wiki article.
- **Exam comments** are HTML comments placed on the line immediately after the last topic in a day.

### Alternative Heading Formats

The tutor also recognizes these heading patterns:

- `## Module 1: Title`
- `## Week 1: Title`
- `## Section 1: Title`
- `## Part I: Title` (Roman numerals)

### Topic Item Patterns

Standard topic items look like:

```markdown
- [ ] **Topic Name** — [Article Name](article-file.md)
```

Links should be relative markdown links. The text before the link is the topic name (bold only).

### No-Day Curriculum

If a file has `- [ ]` items but no `## Day N:` headings, the tutor treats the entire file as a single day.

```markdown
# Flat Reading List

- [ ] **Topic A** — [Article A](article-a.md)
- [ ] **Topic B** — [Article B](article-b.md)
```

### Reading-Only Curriculum

If a file has `## Day N:` headings but no `- [ ]` checklist items, the tutor presents it as a reading list with no exams.

## Example

See `wiki/rust/rust-ardan-curriculum.md` for a complete example.

```markdown
# Ardan Ultimate Rust Foundations — Curriculum

> Sources: Ardan Ultimate Rust Foundations (thebracket/ArdanUltimateRustFoundations), 2025
> Raw: [ardan-curriculum.md](../../raw/rust/ardan-curriculum.md)

## Course Overview

Presented by Ardan Labs, Ultimate Rust: Foundations is a "zero to hero" workshop...

## Day 1: Core Rust

Basics of Rust: project setup, fundamental types, collections, serialization, and CLI applications.

- [ ] **Class Introduction & Setup** — [Rust Cargo and Project Setup](rust-cargo-and-project-setup.md)
- [ ] **Hello World** — [Rust Hello World](rust-hello-world.md)
...
<!-- Day 1 Exam: 100/100 PASSED -->

## Day 2: Ownership & Concurrency

Modules, documentation, error handling, borrow checker, lifetimes, OOP, RAII, threading...

- [ ] **Modules & Visibility** — [Rust Modules and Visibility](rust-modules-and-visibility.md)
...
```
