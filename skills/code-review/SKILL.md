---
name: code-review
description: Systematic guidelines for evaluating pull requests and code modifications against clean code, security, performance, DRY, and SOLID rubrics.
version: 1.0.0
category: quality
tags: [code-review, clean-code, solid, dry, lint, maintainability, audit]
---

# Skill: Code Review & Quality Auditing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `code-review`
- **Category**: Quality & Assurance
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes an objective, thorough peer-review and code-auditing protocol. It evaluates diffs for adherence to SOLID principles, DRY standards, security boundaries, performance budgets, accessibility rules, and maintainability.

---

## 3. Scope
- **In-Scope**:
  - Analyzing code diffs against mandatory repository rules in [`RULES.md`](../../RULES.md).
  - Checking SOLID design principles, clean naming, and modularity.
  - Verifying test coverage for new code paths and bug fixes.
  - Inspecting UI code against UI/UX Pro Max standards (contrast, touch targets, tokens).
  - Providing actionable, constructive, and respectful review feedback.
- **Out-of-Scope**:
  - Direct implementation of major feature refactoring (delegate to [`skills/refactoring/SKILL.md`](../refactoring/SKILL.md)).
  - Executing deep hypothesis-driven debugging (delegate to [`skills/debugging/SKILL.md`](../debugging/SKILL.md)).

---

## 4. When to Use
- Prior to merging any branch, completing a major phase, or marking a task `Completed`.
- Stage 7 of the canonical lifecycle in [`WORKFLOW.md`](../../WORKFLOW.md).
- When conducting architectural health audits across existing modules.

---

## 5. When Not to Use
- During exploratory prototyping sessions before code stabilization.

---

## 6. Prerequisites
- Target code diff or pull request available.
- Acceptance criteria and task specifications identified in [`TASKS.md`](../../TASKS.md).

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- System architecture in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).

---

## 8. Core Instructions
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

## 9. Step-by-Step Workflow
1. **Step 1: Scope & Context Check**
   - Review task description in `TASKS.md`. Ensure diff addresses only the requested scope without extraneous edits.
2. **Step 2: Automated Analysis Check**
   - Confirm linters, formatters, and test suites pass with zero warnings.
3. **Step 3: Security & Invariant Audit**
   - Check diff against Anti-Pattern Blacklist in [`RULES.md`](../../RULES.md).
4. **Step 4: UI/UX Pro Max Check (if UI touched)**
   - Run Pre-Delivery Checklist:
     - [ ] SVG icons only (no emojis).
     - [ ] Semantic tokens used (no raw hex).
     - [ ] Hit targets ≥ 44×44px with 8px+ spacing.
     - [ ] Contrast ≥ 4.5:1.
5. **Step 5: Synthesize Review Report**
   - Produce a structured summary of findings, citing line numbers and recommended fixes.

---

## 10. Quality Standards
- **Zero False Approvals**: Code with security flaws or failing tests is never approved.
- **Constructive Clarity**: Every flagged issue includes a concrete, correct code example.
- **Traceability**: Review findings link directly to rules in `RULES.md` or architecture specs.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Rule Adherence | Audit against `RULES.md` | Zero violations of mandatory constraints |
| Test Coverage | Coverage report inspection | 100% of new business logic paths covered by tests |
| UI/UX Verification | UI checklist review | Zero violations of UI/UX Pro Max standards |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Superficial Review ("Looks good!") | Misses subtle concurrency bugs, SQLi, and accessibility failures | Follow the 5 review dimensions systematically |
| Nitpicking Style over Substance | Argues over personal preferences instead of standards | Rely strictly on repository lint rules and `RULES.md` |

---

## 13. Restrictions
- Do NOT approve diffs that introduce external dependencies without ADR documentation.
- Do NOT approve diffs with failing tests or unhandled exceptions.

---

## 14. Expected Deliverables
- Structured Code Review Report with categorized findings (`[BLOCKER]`, `[SUGGESTION]`).
- Verification checklist confirmation.

---

## 15. Documentation Requirements
- Record recurring review findings in [`MEMORY.md`](../../MEMORY.md).
- Update review status in [`TASKS.md`](../../TASKS.md).

