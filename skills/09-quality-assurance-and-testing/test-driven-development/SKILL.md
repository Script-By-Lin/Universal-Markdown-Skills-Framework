---
name: test-driven-development
description: "The canonical Test-Driven Development (TDD) engineering discipline: Red-Green-Refactor, automated test authoring first, edge case coverage, and behavioral invariance."
version: 1.7.0
category: quality
tags: ['testing', 'tdd', 'red-green-refactor', 'unit-testing', 'quality', 'test-first']
---

# Skill: Test-Driven Development (TDD)

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `test-driven-development`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Author minimal failing tests before writing production code, implementing features via Red-Green-Refactor cycles.
- **When to Use**: Authoring any new feature logic, fixing bugs, or implementing algorithmic service components.
- **Essential Invariants**:
  1. Author failing test FIRST (Red) before writing any implementation code.
  2. Write the minimal code necessary to pass the test (Green).
  3. Refactor code and tests to maintain clean structure while tests remain Green (Refactor).
- **Minimal Workflow**:
  1. Write focused unit test asserting required behavior or defect reproduction.
  2. Execute test runner to verify test fails for the expected reason (Red).
  3. Write minimal production code to satisfy the assertion (Green).
  4. Refactor implementation for readability, performance, and structure.
  5. Re-run test suite to confirm exit code 0 and zero regressions.
- **Expected Deliverables**: Passing test suite with high coverage written synchronously before implementation.
- **Critical Restrictions**: Never write implementation code before an automated test exists to verify it.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Mandates and guides the strict application of Test-Driven Development (TDD) across all testable application features, ensuring requirements are proven by failing tests prior to implementation.

---

### Scope
- **In-Scope**:
  - Executing the mandatory Red-Green-Refactor cycle\n  - Authoring failing unit and integration tests prior to application code\n  - Enumerating positive, negative, boundary, and edge case scenarios\n  - Refactoring code structure under continuous test verification\n  - Logging justified TDD exceptions in `docs_agent/testing/TDD_LOG.md`
- **Out-of-Scope**:
  - System-wide exploratory testing (delegate to `skills/09-quality-assurance-and-testing/exploratory-testing/SKILL.md`)\n  - Adversarial security penetration testing (delegate to `skills/02-security-engineering/penetration-testing/SKILL.md`)

---

### When to Use
- Implementing new application features, services, or functions\n- Fixing defects and reproducing reported bugs (reproduction test first)\n- Refactoring existing business domain logic

---

### When Not to Use
- Exploratory architectural spike prototypes (must be logged as exception)\n- Pure static documentation edits without code modifications

---

### Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in `TASKS.md`.

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in `RULES.md` (TDD invariants & Release Gates).
- Testing environment in `CONTEXT.md`.
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

### Core Instructions
### 8.1 The Three Mandatory TDD Phases
1. **PHASE 1: RED (Test Authoring & Failure Verification)**
   - Deconstruct acceptance criteria into atomic assertions.
   - Write automated test capturing:
     - **Positive / Happy Path**: Valid inputs produce expected outputs.
     - **Negative Cases**: Invalid inputs raise typed domain errors or HTTP 400/422.
     - **Boundary & Edge Cases**: Empty collections, zero values, max string lengths, null/undefined handling.
   - Run test suite and **confirm failure**: The test must fail specifically because the production code does not exist or lacks the capability. If the test fails due to syntax or broken harness, fix the test first.
2. **PHASE 2: GREEN (Minimal Implementation)**
   - Author only the minimum production code necessary to make the failing test pass.
   - Do NOT implement future speculative features or optimize prematurely.
   - Run test suite and confirm all tests pass cleanly.
3. **PHASE 3: REFACTOR (Quality & Maintainability)**
   - Clean up code structure, eliminate duplication, improve variable naming, and extract reusable helpers.
   - Re-run test suite after every micro-edit to ensure continuous green state.

### 8.2 Strict TDD Invariants (RULES.md Level 2)
- Never write tests after writing code to match what was already built (confirmation bias prohibition).
- Never modify an existing test to force buggy implementation code to pass.
- Never delete failing tests without documented authorization.
- Never claim tests passed without executing the test command and inspecting exit code 0.

---

### Step-by-Step Workflow
1. **Step 1: Requirement Intake & Case Matrix**
   - Review story acceptance criteria. List positive, negative, and edge test cases.
2. **Step 2: RED Phase Execution**
   - Write automated test in appropriate test directory.
   - Run test runner: verify test fails with assertion failure (Exit code != 0).
3. **Step 3: GREEN Phase Execution**
   - Implement minimal production code to satisfy assertion.
   - Run test runner: verify test passes (Exit code == 0).
4. **Step 4: REFACTOR Phase Execution**
   - Clean architecture, enforce types, run linter. Confirm tests stay green.
5. **Step 5: Log Progress in TDD Log**
   - Record test additions in `docs_agent/testing/TDD_LOG.md`.

---

### Quality Standards
- **Standard 1**: 100% adherence to the mandatory TDD Red-Green-Refactor protocol.
- **Standard 2**: All tests must run deterministically with zero flakiness.
- **Standard 3**: Absolute prohibition on claiming tests passed without verifying execution exit code 0.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Test Execution | Automated test runner execution | 100% passing tests; exit code 0 |
| Regression Safety | Full regression suite execution | Zero regressions in existing capabilities |
| Coverage Integrity | Coverage instrumentation | Branch coverage meets agreed project threshold |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Writing Tests After Implementation | High susceptibility to confirmation bias | Follow TDD: write failing test first (RED phase) |
| Hardcoded Sleeps | Causes flaky, brittle, and slow test runs | Wait explicitly for state or DOM conditions |
| Shared Mutable Test Data | Tests fail unpredictably when run in parallel | Use isolated data factories and per-test cleanups |

---

### Restrictions
- Do NOT modify tests merely to force incorrect implementation code to pass.
- Do NOT delete failing tests without documented architectural authorization.
- Do NOT bypass Functional or Regression Release Gates.

---

### Expected Deliverables
- Automated test suites (unit, integration, or E2E).
- Updated testing logs in `docs_agent/testing/TDD_LOG.md` or `TEST_RESULTS.md`.
- Regression verification report.

---

### Documentation Requirements
- Record testing conventions and discovered edge cases in `MEMORY.md`.
- Record testing architectural trade-offs in `DECISIONS.md`.
- Update task tracking in `TASKS.md` and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
