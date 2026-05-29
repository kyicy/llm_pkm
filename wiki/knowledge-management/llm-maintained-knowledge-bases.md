# LLM-Maintained Knowledge Bases

> Sources: Andrej Karpathy, Unknown
> Raw: [llm-wiki.md](../../raw/knowledge-management/llm-wiki.md)

## Overview

Instead of RAG-style retrieval where an LLM re-discovers knowledge from raw documents on every query, the LLM Wiki pattern has the LLM incrementally build and maintain a persistent, structured wiki that compounds over time. The LLM reads sources, extracts key information, integrates it into existing articles, updates cross-references, notes contradictions, and keeps the synthesis current. The human curates sources, directs analysis, asks questions, and thinks about meaning. The LLM handles all the bookkeeping.

## Core Insight: Compounding Knowledge

The key difference from RAG is that **the wiki is a persistent, compounding artifact**. Cross-references already exist. Contradictions are already flagged. The synthesis already reflects everything ingested. Each new source or query enriches the wiki, and nothing is re-derived from scratch.

## Three-Layer Architecture

1. **Raw sources**: Immutable collection of source documents. The LLM reads but never modifies them. Source of truth.
2. **The wiki**: LLM-generated markdown files — summaries, entity pages, concept pages, comparisons. The LLM owns this layer entirely.
3. **The schema**: A configuration document (e.g., CLAUDE.md) that defines structure, conventions, and workflows. Makes the LLM a disciplined wiki maintainer.

In practice: Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase.

## Three Operations

### Ingest

Adding a new source involves: reading it, discussing key takeaways, writing a summary page, updating the index, updating affected entity/concept pages across the wiki, and logging the operation. A single source might touch 10–15 wiki pages. Can be done one-at-a-time (with human guidance) or batch-ingested.

### Query

The LLM searches relevant pages, reads them, and synthesizes an answer with citations. Answers can take multiple forms: markdown page, comparison table, slide deck (Marp), chart, canvas. Key insight: **good answers can be filed back into the wiki**, so explorations compound like ingested sources.

### Lint

Periodic health checks: detect contradictions, stale claims, orphan pages, missing cross-references, concepts lacking pages, data gaps. The LLM surfaces issues and suggests new questions to investigate.

## Navigation: Index and Log

Two special files serve different purposes:

- **index.md**: Content-oriented catalog — every page listed with a link and one-line summary. Read first when answering queries to find relevant pages.
- **log.md**: Chronological, append-only record of operations. Parseable with simple unix tools (e.g., `grep "^## \[" log.md | tail -5`).

## Why It Works

The bottleneck in maintaining a knowledge base is not reading or thinking — it's bookkeeping. Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don't get bored, don't forget cross-references, and can touch many files in one pass. The cost of maintenance approaches zero.

The idea traces back to Vannevar Bush's Memex (1945) — a personal, curated knowledge store with associative trails between documents. Bush couldn't solve who does the maintenance. The LLM handles that.

## Application Domains

- **Personal**: Goals, health, psychology, self-improvement — building a structured picture of yourself over time
- **Research**: Deep dives over weeks/months with an evolving thesis
- **Reading**: Chapter-by-chapter companion wikis for books (characters, themes, plot threads)
- **Business/team**: Internal wikis fed by Slack, meetings, project docs; LLM does the maintenance no one wants to do
- **Competitive analysis, due diligence, trip planning, course notes, hobby deep-dives**

## See Also

- [AI Agents in Software Development](../ai/ai-agents-in-software-development.md) — a skeptical viewpoint on LLM capabilities in software engineering
