---
name: refactoring
description: Systematic techniques for safely restructuring code to improve readability and maintainability without altering observable external behavior.
version: 1.0.0
category: modernization
tags: [refactoring, clean-code, tech-debt, design-patterns, behavioral-invariance]
---

# Skill: Safe Code Refactoring & Modernization

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `refactoring`
- **Category**: Code Modernization & Maintenance
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes strict discipline for refactoring codebases. It enables developers and AI coding agents to improve code readability, reduce cyclomatic complexity, eliminate duplication, and decouple tightly bound modules while guaranteeing absolute behavioral invariance through test coverage.

---

## 3. Scope
- **In-Scope**:
  - Restructuring existing code without altering external observable behavior.
  - Decomposing monolithic functions, classes, and modules into cohesive units.
  - Replacing procedural code with standard design patterns (Strategy, Factory, Adapter).
  - Eliminating code smells (Long Method, God Class, Feature Envy, Primitive Obsession).
  - Ensuring continuous test passing throughout incremental transformations.
- **Out-of-Scope**:
  - Adding new user-facing features (delegate to [`skills/backend-development/SKILL.md`](../backend-development/SKILL.md) or [`skills/frontend-development/SKILL.md`](../frontend-development/SKILL.md)).
  - Fixing functional bugs (delegate to [`skills/debugging/SKILL.md`](../debugging/SKILL.md)).

---

## 4. When to Use
- When code complexity hinders readability, testing, or feature extension.
- Prior to adding major new features to legacy or poorly structured code ("Make the change easy, then make the easy change").
- When resolving architectural tech debt identified during code review.

---

## 5. When Not to Use
- When comprehensive test coverage is absent (tests must be added *before* refactoring).
- Under emergency production outage conditions where fast surgical bugfixes are required.

---

## 6. Prerequisites
- Target code covered by a comprehensive automated test suite.
- Baseline test suite verified green (100% passing) before touching code.

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- Architectural boundaries defined in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).

---

## 8. Core Instructions
1. **Behavioral Invariance (Non-Negotiable)**:
   - Refactoring never adds new functionality and never changes existing behavior.
   - All existing tests that pass before refactoring must pass after refactoring without test modification.
2. **Small, Atomic Transformations**:
   - Apply refactoring in micro-steps (e.g., Extract Function -> Run Tests -> Rename Variable -> Run Tests).
   - Never perform large multi-file rewrites in a single unverified leap.
3. **Characterization Tests First**:
   - If legacy code lacks adequate test coverage, author characterization tests capturing current behavior *before* modifying the implementation.
4. **Preserve Documentation & Comments**:
   - Retain important docstrings, comments explaining domain nuances, and licensing headers.

---

## 9. Step-by-Step Workflow
1. **Step 1: Verify Baseline Test Suite**
   - Run existing tests. Confirm 100% passing status. If tests are missing, author them first.
2. **Step 2: Identify Specific Code Smells**
   - Pinpoint: Long method (&gt; 30 lines), deep nesting (&gt; 3 levels), duplicate logic, primitive obsession.
3. **Step 3: Select Refactoring Recipe**
   - Choose standard recipe: Extract Method, Introduce Parameter Object, Replace Conditional with Polymorphism, Pull Up Method.
4. **Step 4: Execute Micro-Transformation**
   - Perform atomic edit. Immediately re-run tests.
5. **Step 5: Iterate and Clean Up**
   - Repeat until code satisfies clean code standards.
6. **Step 6: Final Verification**
   - Run entire test suite and linters to verify zero regressions.

---

## 10. Quality Standards
- **Zero Behavioral Drift**: 100% of existing tests pass without modification.
- **Complexity Reduction**: Cyclomatic complexity reduced; function length reduced.
- **Maintainability**: Clearer naming, single responsibilities, and zero duplicate blocks.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Invariance Verification | Automated test suite execution | 100% test pass rate with zero changes to test files |
| Linter Audit | Project linter execution | Zero linter warnings or errors introduced |
| Complexity Audit | Cyclomatic complexity check | Maximum nesting ≤ 3; functions concise |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Refactoring Without Tests | Inevitably introduces silent functional regressions | Write characterization tests first |
| Mixing Features with Refactoring | Makes diffs unreviewable and complicates git bisect | Keep refactoring commits strictly separate from feature commits |

---

## 13. Restrictions
- Do NOT alter external API contracts or database schemas during a refactoring task.
- Do NOT modify test assertions to accommodate unintentional behavioral changes.

---

## 14. Expected Deliverables
- Cleaned, refactored code modules.
- Characterization tests (if newly introduced).

---

## 15. Documentation Requirements
- Record refactoring patterns and architectural lessons in [`MEMORY.md`](../../MEMORY.md).
- Update [`TASKS.md`](../../TASKS.md) with task completion.

