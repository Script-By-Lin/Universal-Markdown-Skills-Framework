---
name: repository-bootstrap
description: Scaffold and initialize canonical UMSF repository governance structures, files, and templates with zero dependencies.
version: 2.0.0
category: software-development-lifecycle
tags: [bootstrap, governance, initialization, templates, local-first]
---

# Skill: Repository Bootstrap & Governance Initialization

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 01-software-development-lifecycle  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `repository-bootstrap`
- **Category**: 01-software-development-lifecycle
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Scaffold and initialize canonical UMSF repository governance structures (AGENTS.md, RULES.md, CONTEXT.md, TASKS.md, DECISIONS.md, WORKFLOW.md, docs_agent/) with zero dependencies.
- **When to Use**: Initializing a new repository, bootstrapping an existing project for AI agent collaboration, or regenerating missing governance files.
- **Essential Invariants**:
  1. Governance files must be pure CommonMark Markdown without external tool dependencies.
  2. Minimal bootstrap file set must include AGENTS.md, RULES.md, CONTEXT.md, TASKS.md, and docs_agent/ directory.
  3. Bootstrap must never overwrite existing project code, build configurations, or existing git configuration.
- **Minimal Workflow**:
  1. Inspect root repository structure to detect existing documentation and build conventions.
  2. Instantiate minimal governance templates (AGENTS.md, RULES.md, CONTEXT.md, TASKS.md, DECISIONS.md).
  3. Create local-first docs_agent/ directory with .gitkeep for local agent session artifacts.
  4. Verify all relative links across bootstrapped files resolve cleanly.
- **Expected Deliverables**: Canonical UMSF governance markdown templates initialized in project root with valid relative links.
- **Critical Restrictions**: Never populate docs_agent/ with pre-filled fake execution reports; never add mandatory non-markdown runtime scripts.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Scaffold and initialize canonical UMSF repository governance structures, files, and templates with zero dependencies.

### Execution Procedures
1. **Preparation**: Review task scope, prerequisites, and verify project state. If governance files (TASKS.md, CONTEXT.md) are absent, create them from the bootstrap template or record the evidence inline.
2. **Implementation**: Execute the procedures according to the Level 1 Minimal Workflow while upholding all Essential Invariants.
3. **Verification**: Verify outputs empirically with exit codes, static linters, and regression checks.

### Edge Cases & Failure Recovery
- **Ambiguous Constraints**: Halt and trigger human-in-the-loop escalation rather than making unverified assumptions.
- **Execution Failures**: Record failure evidence, isolate root cause, and formulate targeted remediation within bounded iterations.

---

## Level 3 — Optional References & Supplementary Assets

### Level 3 Index
- None (all core procedures codified in Level 1 & Level 2).
