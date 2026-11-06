---
name: static-analysis-and-linting
description: Configure and enforce automated AST linters, strict type checkers, cyclomatic complexity limits, and deterministic formatting rules.
version: 2.0.0
category: code-quality-and-maintenance
tags: [static-analysis, linting, type-checking, formatting, complexity, ast]
---

# Skill: Static Analysis, Type Checking & Linting

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 12-code-quality-and-maintenance  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `static-analysis-and-linting`
- **Category**: 12-code-quality-and-maintenance
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Configure and enforce automated AST linters, type checkers, cyclomatic complexity limits, and formatting rules.
- **When to Use**: Setting up codebase quality standards, configuring pre-commit hooks, catching syntax/type errors, or auditing complexity.
- **Essential Invariants**:
  1. Type checking and linting rules must execute in strict mode without suppressed fatal warnings.
  2. Automated formatting must be completely deterministic (zero churn across developer machines).
  3. Code complexity metrics (cyclomatic/cognitive complexity) must enforce maximum threshold gates.
- **Minimal Workflow**:
  1. Configure canonical language linters (ESLint, Ruff, Clippy) and strict type checkers (TypeScript, Mypy).
  2. Set up automated formatter (Prettier, Black, Rustfmt) and integrate with git pre-commit hooks.
  3. Run static analyzer over codebase and resolve all syntax, typing, and style errors.
  4. Configure CI gate to reject commits with lint errors or unformatted files.
- **Expected Deliverables**: Linter and type checker configuration files, pre-commit configuration, and 0-error analysis report.
- **Critical Restrictions**: Prohibit widespread disable comments (eslint-disable, type: ignore) without documented justification.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Configure and enforce automated AST linters, strict type checkers, cyclomatic complexity limits, and deterministic formatting rules.

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
