---
name: mutation-testing
description: "Evaluation of test suite efficacy through deliberate fault injection (mutants) to verify assertion rigor and eliminate weak tests."
version: 1.0.0
category: quality
tags: ['testing', 'mutation-testing', 'fault-injection', 'test-quality', 'mutants']
---

# Skill: Mutation Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `mutation-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Validates that automated test suites actually fail when bugs exist by injecting deliberate mutations into production code and confirming that tests catch (kill) the mutants.

---

## 3. Scope
- **In-Scope**:
  - Injecting syntactic mutations (e.g. changing `>` to `>=`, replacing `+` with `-`, negating conditionals)\n  - Measuring the Mutation Score Indicator (percentage of killed mutants)\n  - Detecting weak assertions (tests that pass regardless of logic correctness)\n  - Hardening test assertions to verify exact return values and side effects
- **Out-of-Scope**:
  - Initial test creation for brand-new features

---

## 4. When to Use
- Auditing critical financial, security, or safety calculation logic\n- Investigating why a production bug slipped past an existing test suite\n- Evaluating the quality of existing automated test suites

---

## 5. When Not to Use
- For simple CRUD or boilerplate routing code where unit testing is sufficient

---

## 6. Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in [`TASKS.md`](../../../TASKS.md).

---

## 7. Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (TDD invariants & Release Gates).
- Testing environment in [`CONTEXT.md`](../../../CONTEXT.md).
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

## 8. Core Instructions
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

## 9. Step-by-Step Workflow
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

## 10. Quality Standards
- **Standard 1**: 100% adherence to the mandatory TDD Red-Green-Refactor protocol.
- **Standard 2**: All tests must run deterministically with zero flakiness.
- **Standard 3**: Absolute prohibition on claiming tests passed without verifying execution exit code 0.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Test Execution | Automated test runner execution | 100% passing tests; exit code 0 |
| Regression Safety | Full regression suite execution | Zero regressions in existing capabilities |
| Coverage Integrity | Coverage instrumentation | Branch coverage meets agreed project threshold |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Writing Tests After Implementation | High susceptibility to confirmation bias | Follow TDD: write failing test first (RED phase) |
| Hardcoded Sleeps | Causes flaky, brittle, and slow test runs | Wait explicitly for state or DOM conditions |
| Shared Mutable Test Data | Tests fail unpredictably when run in parallel | Use isolated data factories and per-test cleanups |

---

## 13. Restrictions
- Do NOT modify tests merely to force incorrect implementation code to pass.
- Do NOT delete failing tests without documented architectural authorization.
- Do NOT bypass Functional or Regression Release Gates.

---

## 14. Expected Deliverables
- Automated test suites (unit, integration, or E2E).
- Updated testing logs in `docs_agent/testing/TDD_LOG.md` or `TEST_RESULTS.md`.
- Regression verification report.

---

## 15. Documentation Requirements
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Record testing architectural trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).
