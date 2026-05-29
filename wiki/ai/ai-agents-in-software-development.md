# AI Agents in Software Development

> Sources: George Hotz, 2026-05-24
> Raw: [the-eternal-sloptember.md](../../raw/ai/2026-05-24-the-eternal-sloptember.md)

## Overview

George Hotz argues that AI coding agents cannot truly program and that their widespread adoption in software development will be a costly mistake. While useful as a better search engine and for quick prototypes, agents produce superficially correct but fundamentally broken output that becomes harder to detect as models improve statistically. The core claim is that the process of creation matters — LLMs mimic the distribution of programming output without the underlying reasoning, and this gap becomes obvious when humans try to build upon AI-generated artifacts.

## The "Slot Machine" Problem

Hotz describes a pattern he experienced firsthand when using agents for real projects at tinygrad: the agent front-loads progress, then turns into a "slot machine" — you keep pulling the lever hoping it will polish the work, but it never quite gets there. He reports that in each case (writing GPU emulation code, reversing a USB-to-PCIe chip), he suspected he could have done it better and faster manually.

He pushes back against the "you're using it wrong" response, noting he has tried different models, harnesses, and prompts without the core problem changing.

## Organizational Impact

The impact differs across contexts:

- **High-performing individuals and small orgs**: Skilled engineers have strong error-correction abilities and learn when to trust vs. distrust agent output. They tend to carefully read and understand each line.
- **Large organizations**: Slower feedback loops and less alignment. Lower performers without self-checking habits produce "10x output" via agents, flooding the codebase with low-quality code ("slop"). This degrades average output quality at scale.

> "Agents will end up producing more code, more apps, and more features than ever before. It is a golden era for buckets and buckets of slop, and a dark age for gems of quality."

## Process vs. Statistics

A central argument is that AI-produced artifacts are created by a fundamentally different process than human ones. People assume human-like intent behind artifacts, but this assumption no longer holds. Old quality proxies like syntax and grammar remain intact, masking brokenness that only surfaces when someone tries to build upon the artifact.

Hotz aligns with LeCun and Marcus: current LLM architectures may never be capable of real programming because they lack world models. He distinguishes between:
- Statistical mimicry of programming output distributions
- Actual programming, which requires reasoning about process and intent

## Practical Utility

Hotz does not dismiss AI entirely. He acknowledges it is:
- A better Google for most searches
- Absurdly fast for quick prototypes where polish doesn't matter

The key skill is knowing when to use it and when not to.

## See Also

- [LLM-Maintained Knowledge Bases](../knowledge-management/llm-maintained-knowledge-bases.md) — a contrasting perspective on LLM capabilities and the human/LLM collaboration model
