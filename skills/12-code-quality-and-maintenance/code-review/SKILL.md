---
name: code-review
description: Systematic guidelines for evaluating pull requests and code modifications against clean code, security, performance, DRY, and SOLID rubrics.
version: 1.7.0
category: quality
tags: [code-review, clean-code, solid, dry, lint, maintainability, audit]
---

# Skill: Peer & Automated Code Review

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 12 — Code Quality & Maintenance  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `code-review`
- **Category**: Code Quality & Maintenance (Domain 12)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Conduct systematic, constructive code reviews verifying correctness, maintainability, architectural invariants, and tests.
- **When to Use**: Reviewing pull requests, evaluating peer contributions, or pre-merge code inspection.
- **Essential Invariants**:
  1. Review for correctness and architectural conformance before style or aesthetics.
  2. Verify that adequate automated tests accompany every functional change.
  3. Provide concrete, actionable feedback with code examples for requested changes.
- **Minimal Workflow**:
  1. Read PR description and map changes against user requirements and issue tickets.
  2. Inspect git diff line-by-line; check for edge cases, error handling, and security flaws.
  3. Verify local or CI test execution results and code coverage metrics.
  4. Approve PR or provide structured, actionable review comments.
- **Expected Deliverables**: Structured code review feedback log or approved PR status with verified criteria.
- **Critical Restrictions**: Never approve PRs containing failing tests, unhandled errors, or unverified architectural violations.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes an objective, thorough peer-review and code-auditing protocol. It evaluates diffs for adherence to SOLID principles, DRY standards, security boundaries, performance budgets, accessibility rules, and maintainability.

---

### Scope
- **In-Scope**:
  - Analyzing code diffs against mandatory repository rules in [`RULES.md`](../../../RULES.md).
  - Checking SOLID design principles, clean naming, and modularity.
  - Verifying test coverage for new code paths and bug fixes.
  - Inspecting UI code against UI/UX Pro Max standards (contrast, touch targets, tokens).
  - Providing actionable, constructive, and respectful review feedback.
- **Out-of-Scope**:
  - Direct implementation of major feature refactoring (delegate to [`skills/refactoring/SKILL.md`](../../refactoring/SKILL.md)).
  - Executing deep hypothesis-driven debugging (delegate to [`skills/debugging/SKILL.md`](../../debugging/SKILL.md)).

---

### When to Use
- Prior to merging any branch, completing a major phase, or marking a task `Completed`.
- Stage 7 of the canonical lifecycle in [`WORKFLOW.md`](../../../WORKFLOW.md).
- When conducting architectural health audits across existing modules.

---

### When Not to Use
- During exploratory prototyping sessions before code stabilization.

---

### Prerequisites
- Target code diff or pull request available.
- Acceptance criteria and task specifications identified in [`TASKS.md`](../../../TASKS.md).

---

### Required Context
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- System architecture in [`docs_agent/ARCHITECTURE.md`](../../../docs_agent/ARCHITECTURE.md).

---

### Core Instructions
1. **The Five Review Dimensions**:
   - **Correctness**: Does the code accurately fulfill requirements without edge-case regressions?
   - **Security**: Are inputs validated? Are queries parameterized? Are secrets excluded?
   - **Performance**: Are there N+1 queries, unindexed filters, or memory leaks?
   - **UI/UX (UI/UX Pro Max)**: Are semantic tokens used? Is contrast ≥ 4.5:1? Are hit targets ≥ 44×44px? Are emojis avoided as icons?
   - **Maintainability & Clean Code**: Is naming descriptive? Is logic decoupled? Are functions concise?
2. **Actionable Feedback Protocol**:
   - Frame feedback with clear categorization:
     - `[BLOCKER]`: Critical defect, security flaw, or mandatory rule violation that must be fixed before merge.
     - `[SUGGESTION]`: Maintainability or clean code optimization that improves quality.
     - `[QUESTION]`: Inquiring about non-obvious design rationale.
3. **Preserve Documentation Integrity**:
   - Verify that comments and docstrings are accurate and that unrelated comments were not accidentally deleted.

---

### Step-by-Step Workflow
1. **Step 1: Scope & Context Check**
   - Review task description in `TASKS.md`. Ensure diff addresses only the requested scope without extraneous edits.
2. **Step 2: Automated Analysis Check**
   - Confirm linters, formatters, and test suites pass with zero warnings.
3. **Step 3: Security & Invariant Audit**
   - Check diff against Anti-Pattern Blacklist in [`RULES.md`](../../../RULES.md).
4. **Step 4: UI/UX Pro Max Check (if UI touched)**
   - Run Pre-Delivery Checklist:
     - [ ] SVG icons only (no emojis).
     - [ ] Semantic tokens used (no raw hex).
     - [ ] Hit targets ≥ 44×44px with 8px+ spacing.
     - [ ] Contrast ≥ 4.5:1.
5. **Step 5: Synthesize Review Report**
   - Produce a structured summary of findings, citing line numbers and recommended fixes.

---

### Quality Standards
- **Zero False Approvals**: Code with security flaws or failing tests is never approved.
- **Constructive Clarity**: Every flagged issue includes a concrete, correct code example.
- **Traceability**: Review findings link directly to rules in `RULES.md` or architecture specs.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Rule Adherence | Audit against `RULES.md` | Zero violations of mandatory constraints |
| Test Coverage | Coverage report inspection | 100% of new business logic paths covered by tests |
| UI/UX Verification | UI checklist review | Zero violations of UI/UX Pro Max standards |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Superficial Review ("Looks good!") | Misses subtle concurrency bugs, SQLi, and accessibility failures | Follow the 5 review dimensions systematically |
| Nitpicking Style over Substance | Argues over personal preferences instead of standards | Rely strictly on repository lint rules and `RULES.md` |

---

### Restrictions
- Do NOT approve diffs that introduce external dependencies without ADR documentation.
- Do NOT approve diffs with failing tests or unhandled exceptions.

---

### Expected Deliverables
- Structured Code Review Report with categorized findings (`[BLOCKER]`, `[SUGGESTION]`).
- Verification checklist confirmation.

---

### Documentation Requirements
- Record recurring review findings in [`MEMORY.md`](../../../MEMORY.md).
- Update review status in [`TASKS.md`](../../../TASKS.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
