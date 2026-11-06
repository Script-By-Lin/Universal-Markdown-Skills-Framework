---
name: article-writing
description: Write articles, guides, blog posts, tutorials, newsletter issues, and other long-form content in a distinctive voice derived from supplied examples or brand guidance. Use when the user wants polished written content longer than a paragraph, especially when voice consistency, structure, and credibility matter.
metadata:
  origin: ECC
version: 1.7.0
---

# Skill: Technical Article & Long-Form Writing

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 15 — Documentation & Technical Communication  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `article-writing`
- **Category**: Documentation & Technical Communication (Domain 15)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Author compelling, polished technical articles, tutorials, blog posts, and whitepapers in a distinctive, authoritative voice.
- **When to Use**: Writing technical blog posts, engineering deep dives, architectural case studies, or release announcements.
- **Essential Invariants**:
  1. Ensure technical accuracy; all cited code examples and architectural concepts must be verified.
  2. Maintain an authoritative, direct, and engaging voice with zero corporate filler or generic AI fluff.
  3. Structure content logically with compelling hooks, clear progression, and actionable takeaways.
- **Minimal Workflow**:
  1. Define article objective, target technical audience, and key technical thesis.
  2. Outline narrative structure (hook, problem statement, technical solution, benchmarks, lessons).
  3. Draft long-form prose with concrete code snippets and architectural diagrams.
  4. Review for clarity, voice consistency, factual accuracy, and technical depth.
- **Expected Deliverables**: Polished, publication-ready technical article with verified code examples.
- **Critical Restrictions**: Avoid repetitive clichés, generic buzzwords, and unsubstantiated technical claims.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

Write long-form content that sounds like an actual person with a point of view, not an LLM smoothing itself into paste.

### When to Activate

- drafting blog posts, essays, launch posts, guides, tutorials, or newsletter issues
- turning notes, transcripts, or research into polished articles
- matching an existing founder, operator, or brand voice from examples
- tightening structure, pacing, and evidence in already-written long-form copy

### Core Rules

1. Lead with the concrete thing: artifact, example, output, anecdote, number, screenshot, or code.
2. Explain after the example, not before.
3. Keep sentences tight unless the source voice is intentionally expansive.
4. Use proof instead of adjectives.
5. Never invent facts, credibility, or customer evidence.

### Voice Handling

If the user wants a specific voice, run `brand-voice` first and reuse its `VOICE PROFILE`.
Do not duplicate a second style-analysis pass here unless the user explicitly asks for one.

If no voice references are given, default to a sharp operator voice: concrete, unsentimental, useful.

### Banned Patterns

Delete and rewrite any of these:
- "In today's rapidly evolving landscape"
- "game-changer", "cutting-edge", "revolutionary"
- "here's why this matters" as a standalone bridge
- fake vulnerability arcs
- a closing question added only to juice engagement
- biography padding that does not move the argument
- generic AI throat-clearing that delays the point

### Writing Process

1. Clarify the audience and purpose.
2. Build a hard outline with one job per section.
3. Start sections with proof, artifact, conflict, or example.
4. Expand only where the next sentence earns space.
5. Cut anything that sounds templated, overexplained, or self-congratulatory.

### Structure Guidance

### Technical Guides

- open with what the reader gets
- use code, commands, screenshots, or concrete output in major sections
- end with actionable takeaways, not a soft recap

### Essays / Opinion

- start with tension, contradiction, or a specific observation
- keep one argument thread per section
- make opinions answer to evidence

### Newsletters

- keep the first screen doing real work
- do not front-load diary filler
- use section labels only when they improve scanability

### Quality Gate

Before delivering:
- factual claims are backed by provided sources
- generic AI transitions are gone
- the voice matches the supplied examples or the agreed `VOICE PROFILE`
- every section adds something new
- formatting matches the intended medium

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
