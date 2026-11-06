---
name: refactoring
description: Systematic techniques for safely restructuring code to improve readability and maintainability without altering observable external behavior.
version: 1.7.0
category: modernization
tags: [refactoring, clean-code, tech-debt, design-patterns, behavioral-invariance]
---

# Skill: Safe Code Refactoring

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 05 — Programming & Implementation  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `refactoring`
- **Category**: Programming & Implementation (Domain 05)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Improve internal code structure, maintainability, and readability without altering external observable behavior.
- **When to Use**: Eliminating technical debt, modularizing large functions, improving naming, or preparing code for new features.
- **Essential Invariants**:
  1. Refactoring must NOT alter external observable behavior or public API contracts.
  2. A comprehensive, passing test suite is mandatory before refactoring begins.
  3. Execute refactorings in small, atomic, independently committable steps.
- **Minimal Workflow**:
  1. Run existing test suite to establish green baseline (exit code 0).
  2. Perform incremental restructuring (extract function, rename symbol, decompose class).
  3. Re-run test suite after each atomic transformation to verify behavior preservation.
  4. Review git diff to ensure zero unintentional functional alterations.
- **Expected Deliverables**: Cleaner, more maintainable code with 100% passing test baseline and zero behavioral regressions.
- **Critical Restrictions**: Never combine refactoring with feature additions or behavioral changes in the same step.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes strict discipline for refactoring codebases. It enables developers and AI coding agents to improve code readability, reduce cyclomatic complexity, eliminate duplication, and decouple tightly bound modules while guaranteeing absolute behavioral invariance through test coverage.

---

### Scope
- **In-Scope**:
  - Restructuring existing code without altering external observable behavior.
  - Decomposing monolithic functions, classes, and modules into cohesive units.
  - Replacing procedural code with standard design patterns (Strategy, Factory, Adapter).
  - Eliminating code smells (Long Method, God Class, Feature Envy, Primitive Obsession).
  - Ensuring continuous test passing throughout incremental transformations.
- **Out-of-Scope**:
  - Adding new user-facing features (delegate to [`skills/backend-development/SKILL.md`](../../backend-development/SKILL.md) or [`skills/ui-ux-pro-max/SKILL.md`](../../ui-ux-pro-max/SKILL.md)).
  - Fixing functional bugs (delegate to [`skills/debugging/SKILL.md`](../../debugging/SKILL.md)).

---

### When to Use
- When code complexity hinders readability, testing, or feature extension.
- Prior to adding major new features to legacy or poorly structured code ("Make the change easy, then make the easy change").
- When resolving architectural tech debt identified during code review.

---

### When Not to Use
- When comprehensive test coverage is absent (tests must be added *before* refactoring).
- Under emergency production outage conditions where fast surgical bugfixes are required.

---

### Prerequisites
- Target code covered by a comprehensive automated test suite.
- Baseline test suite verified green (100% passing) before touching code.

---

### Required Context
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- Architectural boundaries defined in [`docs_agent/ARCHITECTURE.md`](../../../docs_agent/ARCHITECTURE.md).

---

### Core Instructions
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

### Step-by-Step Workflow
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

### Quality Standards
- **Zero Behavioral Drift**: 100% of existing tests pass without modification.
- **Complexity Reduction**: Cyclomatic complexity reduced; function length reduced.
- **Maintainability**: Clearer naming, single responsibilities, and zero duplicate blocks.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Invariance Verification | Automated test suite execution | 100% test pass rate with zero changes to test files |
| Linter Audit | Project linter execution | Zero linter warnings or errors introduced |
| Complexity Audit | Cyclomatic complexity check | Maximum nesting ≤ 3; functions concise |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Refactoring Without Tests | Inevitably introduces silent functional regressions | Write characterization tests first |
| Mixing Features with Refactoring | Makes diffs unreviewable and complicates git bisect | Keep refactoring commits strictly separate from feature commits |

---

### Restrictions
- Do NOT alter external API contracts or database schemas during a refactoring task.
- Do NOT modify test assertions to accommodate unintentional behavioral changes.

---

### Expected Deliverables
- Cleaned, refactored code modules.
- Characterization tests (if newly introduced).

---

### Documentation Requirements
- Record refactoring patterns and architectural lessons in [`MEMORY.md`](../../../MEMORY.md).
- Update [`TASKS.md`](../../../TASKS.md) with task completion.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
