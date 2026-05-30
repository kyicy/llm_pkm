# Curriculum File Format

A curriculum file is a markdown document that defines a structured learning path. It organizes topics into sections (day, unit, module, etc.) with checklist items and links to wiki articles.

## Format Specification

### Overall Structure

```markdown
# Title — Subtitle

> Sources: Source Name (source-id), Year
> Raw: [source-file.md](../../raw/topic/source-file.md)

## Course Overview

Description of the curriculum. What it covers, format, prerequisites, etc.

## Day 1: Day Title

Description of what this day covers.

- [ ] **Topic Title** — [Linked Article](linked-article.md)
- [ ] **Another Topic** — [Another Article](another-article.md)
- [x] **Completed Topic** — [Completed Article](completed-article.md)
<!-- Day 1 Exam: 100/100 PASSED -->

## Day 2: Next Day Title

Description...

- [ ] **Next Topic** — [Next Article](next-article.md)
```

### Required Elements

| Element | Format | Required |
|---------|--------|----------|
| Title | `# Title` | Yes |
| Section heading | `## <Label> N: Title` (see below) | Yes (or flat list) |
| Topic item | `- [ ] **Topic Name** — [Link](file.md)` | Yes |
| Completed item | `- [x] **Topic Name** — [Link](file.md)` | Optional |
| Exam result | `<!-- <Label> N Exam: SCORE/100 PASSED -->` | Optional (auto-added by tutor) |

### Naming Conventions

- **Section headings** use `## <Label> N: Descriptive Title`. The label is any word (singular, capitalized). Recognized labels include: `Day`, `Unit`, `Module`, `Week`, `Section`, `Chapter`, `Lesson`, `Part`. Numbers can be Arabic numerals (`1`, `2`) or Roman numerals (`I`, `II`).
- **Topic items** use bold `**Topic Name**` followed by ` — ` (space, em-dash, space) and a markdown link to the wiki article.
- **Wiki article links** are relative paths from the curriculum file's directory to the wiki article.
- **Exam comments** are HTML comments placed on the line immediately after the last topic in a section, using the section's label.

### Recognized Heading Patterns

The tutor dynamically recognizes any `## <Label> N:` pattern. Common examples:

```
## Day 1: Title
## Unit 1: Title
## Module 1: Title
## Week 1: Title
## Section 1: Title
## Chapter 1: Title
## Lesson 1: Title
## Part I: Title        (Roman numerals)
```

The tutor uses the label (e.g., "Unit", "Day") in all display strings, announcements, and save comments.

### Supplementary Content Between Heading and Checklist

Section headings may be followed by descriptive content (paragraphs, bullet lists, bold key-skill sections, highlights) before the first checklist item. This content is treated as section metadata:

```markdown
## Unit 1: Derivatives

Definition and computation of derivatives...

**Key skills:** Compute derivatives from the limit definition...

**Highlight — Geometric insight:** The derivative $f'(x_0)$ is the slope of the tangent line.

- [ ] **Lecture 1** — [Derivatives](article.md)
```

The tutor reads this content as teaching context for the section but does NOT treat it as a separate topic or section heading.

### Non-Curriculum Headings

Headings like `## Course Overview`, `## See Also`, `## References`, and similar metadata headings that lack checklist items are ignored as curriculum content. They are not treated as sections for learning progression.

### Topic Item Patterns

Standard topic items look like:

```markdown
- [ ] **Topic Name** — [Article Name](article-file.md)
```

Links should be relative markdown links. The text before the link is the topic name (bold only).

### No-Section Curriculum (Flat List)

If a file has `- [ ]` items but no `## <Label> N:` headings, the tutor treats the entire file as a single section.

```markdown
# Flat Reading List

- [ ] **Topic A** — [Article A](article-a.md)
- [ ] **Topic B** — [Article B](article-b.md)
```

### Reading-Only Curriculum

If a file has `## <Label> N:` headings but no `- [ ]` checklist items, the tutor presents it as a reading list with no exams.

## Examples

### Example 1: Day-based (Rust)

```
wiki/rust/rust-ardan-curriculum.md
```

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
```

### Example 2: Unit-based with supplementary content (MIT Calculus)

```
wiki/mathematics/mit-18.01-curriculum.md
```

```markdown
# MIT 18.01 Single Variable Calculus — Curriculum

> Sources: MIT OpenCourseWare, Fall 2006
> Raw: [mit-18.01-unit1-derivatives.md](../../raw/learning/mit-18.01-unit1-derivatives.md)

## Course Overview

MIT 18.01 Single Variable Calculus is a complete first course in calculus...

## Unit 1: Derivatives

Definition and computation of derivatives...

**Key skills:** Compute derivatives from the limit definition...

**Highlight — Geometric insight:** The derivative $f'(x_0)$ is the slope of the tangent line.

- [ ] **Lecture 1** — Derivatives, Slope, Velocity, and Rate of Change — [MIT 18.01 Unit 1: Derivatives](mit-18.01-unit1-derivatives.md)

...more topics...
```
