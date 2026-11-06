---
name: documentation
description: Standards for authoring technical specifications, runbooks, architecture decision records, API documentation, and Markdown maintenance.
version: 1.7.0
category: documentation
tags: [documentation, technical-writing, markdown, runbooks, specs, api-docs]
---

# Skill: Technical Documentation & Knowledge Architecture

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 15 — Documentation & Technical Communication  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `documentation`
- **Category**: Documentation & Technical Communication (Domain 15)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Author, organize, and maintain accurate technical documentation, architecture blueprints, API specs, and runbooks.
- **When to Use**: Documenting features, updating project architectural state, writing guides, or authoring READMEs.
- **Essential Invariants**:
  1. Documentation must reflect verified repository filesystem reality, not outdated assumptions.
  2. Use portable relative markdown links with line-range anchors where appropriate.
  3. Keep documentation concise, structured, and free of speculative or redundant content.
- **Minimal Workflow**:
  1. Audit existing documentation files (README.md, CONTEXT.md, ARCHITECTURE.md).
  2. Verify code samples and terminal commands against actual working implementations.
  3. Author or update clear, structured documentation with mermaid diagrams and tables.
  4. Verify all internal markdown links resolve to valid target files with zero 404s.
- **Expected Deliverables**: Accurate, well-structured technical documentation with verified relative links.
- **Critical Restrictions**: Never document unreleased or speculative features as current verified reality.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes universal standards for technical documentation engineering. It governs the structure, precision, tone, visual diagrams, and lifecycle maintenance of developer guides, API references, architecture decision records, runbooks, and Markdown project assets.

---

### Scope
- **In-Scope**:
  - Authoring developer onboarding guides, READMEs, and technical runbooks.
  - Formulating Mermaid architecture flowcharts, sequence diagrams, and state diagrams.
  - Documenting API contracts, parameter tables, and usage examples.
  - Maintaining Markdown typographical standards and clickable file links.
  - Keeping project reality documentation (`CONTEXT.md`, `MEMORY.md`) synchronized with code.
- **Out-of-Scope**:
  - Marketing copy and non-technical promotional content.
  - Code implementation (delegate to respective development skills).

---

### When to Use
- When introducing a new repository, subsystem, API, or operational tool.
- At Stage 8 of the canonical engineering lifecycle in `WORKFLOW.md`.
- When documenting historical ADRs, debugging post-mortems, or session continuity handoffs.

---

### When Not to Use
- During exploratory, pre-architectural prototyping before system behavior is known.

---

### Prerequisites
- Target code, architecture, or workflow verified and functional.
- Target audience (developers, operators, AI coding agents) identified.

---

### Required Context
- Markdown design standards in [`docs_agent/ARCHITECTURE.md`](../../../docs_agent/ARCHITECTURE.md) Section 6.
- Mandatory constraints in `RULES.md`.

---

### Core Instructions
1. **Accuracy Above All Else (Zero Fabrication)**:
   - Every file path, command, configuration setting, and parameter must be verified against actual repository code before writing.
   - Distinguish verified facts from assumptions.
2. **Actionable & Concise Tone**:
   - Write in direct, active voice ("Configure the port", not "The port should be configured by the user").
   - Prefer structured tables, bullet points, and code snippets over sprawling walls of prose.
3. **Typographical & Markdown Standards**:
   - Always declare syntax tags on code blocks (`bash`, `json`, `yaml`, `typescript`, `mermaid`).
   - Use standard GitHub-style alerts (`> [!NOTE]`, `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`, `> [!CAUTION]`).
   - Maintain strict heading hierarchies (`#` -> `##` -> `###`).
4. **Visual Diagrams via Mermaid**:
   - Use Mermaid flowcharts (`flowchart TD`) and sequence diagrams (`sequenceDiagram`) to communicate multi-step workflows and component relationships.
5. **Clickable Relative Links**:
   - Always use clickable Markdown links for files (``AGENTS.md``).

---

### Step-by-Step Workflow
1. **Step 1: Information Gathering & Code Inspection**
   - Inspect actual source files, CLI flags, schemas, and configurations.
2. **Step 2: Define Document Architecture**
   - Outline document with clear section headings, target audience, and prerequisite list.
3. **Step 3: Draft Technical Content**
   - Write concise explanations, command invocations, and illustrative code snippets.
4. **Step 4: Embed Visual Architecture Diagrams**
   - Author Mermaid diagrams illustrating component interactions or workflows.
5. **Step 5: Verify Links, Commands, and Syntax**
   - Verify every file link exists on disk; verify commands execute cleanly.

---

### Quality Standards
- **Executability**: Every code snippet and command in documentation can be copied and run without syntax errors.
- **Completeness**: Prerequisites, configuration parameters, and edge cases are documented.
- **Link Integrity**: 100% of internal file references resolve to existing files.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Link Integrity | Automated path check script | All linked Markdown files exist |
| Command Veracity | Shell execution of documented commands | Commands execute with exit code 0 |
| Markdown Linting | Syntax and heading structure check | Strict hierarchical headings; valid code fences |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Outdated Documentation Drift | Code changes but docs remain stale, misleading future developers | Update documentation in the same commit/task as code changes |
| Untested Example Snippets | Users copy-paste broken examples, eroding trust | Test every documented code sample in an isolated test |

---

### Restrictions
- Do NOT document unverified assumptions as facts.
- Do NOT create redundant, duplicated documentation files that fork sources of truth.

---

### Expected Deliverables
- Clear, accurate, and comprehensive Markdown documentation files.
- Mermaid diagrams illustrating complex flows.

---

### Documentation Requirements
- Synchronize updates across `CONTEXT.md` and `README.md`.
- Record documentation updates in [`docs_agent/DEVELOPMENT_LOG.md`](../../../docs_agent/DEVELOPMENT_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
