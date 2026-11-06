---
name: mutation-testing
description: "Evaluation of test suite efficacy through deliberate fault injection (mutants) to verify assertion rigor and eliminate weak tests."
version: 1.7.0
category: quality
tags: ['testing', 'mutation-testing', 'fault-injection', 'test-quality', 'mutants']
---

# Skill: Mutation Testing & Test Quality Audit

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `mutation-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Evaluate the true fault-detection capability of test suites by injecting synthetic bugs (mutants) into production code.
- **When to Use**: Auditing test effectiveness, verifying critical algorithms, or strengthening financial/security test suites.
- **Essential Invariants**:
  1. High test coverage does not guarantee test quality; mutation score measures actual defect detection.
  2. Mutants that survive execution represent gaps in test assertions.
  3. Target mutation testing at core domain logic, algorithms, and security filters.
- **Minimal Workflow**:
  1. Configure mutation testing tool (Stryker, Mutmut, Cosmic Ray).
  2. Execute mutation run against core business logic modules.
  3. Analyze surviving mutants to identify missing or weak test assertions.
  4. Enhance test assertions to kill surviving mutants and improve mutation score.
- **Expected Deliverables**: Mutation testing report with high mutation score (>= 80% killed mutants).
- **Critical Restrictions**: Never run mutation testing across un-isolated third-party libraries or auto-generated code.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Validates that automated test suites actually fail when bugs exist by injecting deliberate mutations into production code and confirming that tests catch (kill) the mutants.

---

### Scope
- **In-Scope**:
  - Injecting syntactic mutations (e.g. changing `>` to `>=`, replacing `+` with `-`, negating conditionals)\n  - Measuring the Mutation Score Indicator (percentage of killed mutants)\n  - Detecting weak assertions (tests that pass regardless of logic correctness)\n  - Hardening test assertions to verify exact return values and side effects
- **Out-of-Scope**:
  - Initial test creation for brand-new features

---

### When to Use
- Auditing critical financial, security, or safety calculation logic\n- Investigating why a production bug slipped past an existing test suite\n- Evaluating the quality of existing automated test suites

---

### When Not to Use
- For simple CRUD or boilerplate routing code where unit testing is sufficient

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
### 8.1 Mutation Testing Methodology
1. **Mutant Generation**: A mutation engine modifies a single operator in production code:
   - Conditionals: `if (a > b)` -> `if (a >= b)` or `if (true)`
   - Arithmetic: `return a + b` -> `return a - b`
   - Return values: `return true` -> `return false`
2. **Execution**: The test suite is run against the mutated code.
3. **Evaluation**:
   - **Killed Mutant**: A test fails. This is good: the test caught the bug.
   - **Survived Mutant**: All tests pass. This is bad: the test suite is weak and has missing assertions.
4. **Target Metric**: Aim for **Mutation Score ≥ 80%** on critical business domain logic.

---

### Step-by-Step Workflow
1. **Step 1: Target Critical Business Units**
   - Select core calculation or authorization services.
2. **Step 2: Execute Mutation Test Runner**
   - Run mutation tool (e.g. Stryker for JS/TS, Mutmut for Python) or manual operator mutation.
3. **Step 3: Analyze Survived Mutants**
   - Review which logic changes survived test execution without failing.
4. **Step 4: Strengthen Weak Assertions**
   - Replace generic `expect(res).toBeDefined()` with exact `expect(res).toBe(expectedValue)`.
5. **Step 5: Document Mutation Score**
   - Log results in `docs_agent/testing/QA_ASSESSMENT.md`.

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
