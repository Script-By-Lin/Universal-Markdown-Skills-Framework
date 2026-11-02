---
name: regression-testing
description: "Systematic regression test suite design, selective regression execution, impact analysis, and accumulation of bug-reproduction tests."
version: 1.0.0
category: quality
tags: ['testing', 'regression', 'regression-testing', 'impact-analysis', 'quality-gate']
---

# Skill: Regression Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `regression-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Guarantees that new code additions, bug fixes, dependency upgrades, or refactorings do not inadvertently break pre-existing application functionality.

---

## 3. Scope
- **In-Scope**:
  - Designing and maintaining targeted regression test suites\n  - Performing change impact analysis to identify regression risk areas\n  - Permanently preserving bug reproduction tests in the test suite\n  - Verifying the Regression Release Gate prior to deployment
- **Out-of-Scope**:
  - Initial greenfield feature testing prior to code stabilization

---

## 4. When to Use
- Before merging pull requests or releasing release candidate builds\n- Following dependency upgrades or infrastructure refactoring\n- Verifying that previously resolved defects remain fixed

---

## 5. When Not to Use
- When writing brand-new standalone features with no pre-existing code interactions

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
### 8.1 Change Impact Analysis
Before running tests, analyze the blast radius of changes:
1. **Direct Impact**: The specific file and function modified.
2. **Upstream Callers**: Components and controllers invoking the modified code.
3. **Downstream Dependencies**: Database tables, shared events, and external APIs affected.
4. **Cross-Cutting Concerns**: Authentication filters, caching layers, and serialization schemas.

### 8.2 The Regression Invariance Rule
- Every bug fix **must commit a test that failed before the fix and passes after the fix**.
- That test becomes a permanent member of the regression suite and must never be deleted without documented architectural justification.

---

## 9. Step-by-Step Workflow
1. **Step 1: Git Diff & Impact Review**
   - Run `git diff` to inventory modified components and identify related subsystems.
2. **Step 2: Selective Fast Regression Run**
   - Run unit and integration tests covering the directly affected modules.
3. **Step 3: Full System Regression Sweep**
   - Execute the complete automated test suite to detect indirect regressions.
4. **Step 4: Defect Verification**
   - Run historical bug regression tests; confirm 100% pass rate.
5. **Step 5: Document Regression Verdict**
   - Author `docs_agent/testing/REGRESSION_REPORT.md` confirming Regression Gate sign-off.

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
