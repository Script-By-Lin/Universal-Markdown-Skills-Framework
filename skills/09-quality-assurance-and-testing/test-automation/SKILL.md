---
name: test-automation
description: "Architecture, implementation, and maintenance of deterministic, robust test automation frameworks across CI/CD environments."
version: 1.0.0
category: quality
tags: ['testing', 'test-automation', 'ci-cd', 'frameworks', 'flaky-tests']
---

# Skill: Test Automation

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `test-automation`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Establishes resilient, maintainable test automation architectures that execute deterministically in automated pipelines without flaky failures or excessive maintenance overhead.

---

## 3. Scope
- **In-Scope**:
  - Designing automated test runners, test harness configurations, and reporters\n  - Eliminating test flakiness through proper synchronization and isolation\n  - Structuring parallel test execution for fast pipeline feedback\n  - Integrating automated test stages into CI/CD workflows
- **Out-of-Scope**:
  - Manual unscripted exploration (delegate to `skills/09-quality-assurance-and-testing/exploratory-testing/SKILL.md`)

---

## 4. When to Use
- Configuring automated test runners for a new project or repository\n- Refactoring brittle or flaky test suites that fail intermittently\n- Optimizing CI test pipeline execution time

---

## 5. When Not to Use
- For one-off scratch verification scripts

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
### 8.1 Eradicating Test Flakiness
Test flakiness destroys developer trust. Enforce these anti-flakiness rules:
1. **Zero Hardcoded Sleeps**: Replace `sleep()` with polling loops asserting specific state conditions with timeouts.
2. **Order Independence**: Every test must run cleanly in isolation or in any arbitrary randomized sequence.
3. **Database Sandboxing**: Use isolated database schemas or transaction rollbacks for each test worker.
4. **Deterministic Clock**: Mock or freeze system time when testing time-dependent logic (e.g. token expiration, billing cycles).
5. **Port Allocation**: Use dynamic ephemeral ports (`port: 0`) for test servers to avoid port collisions in parallel workers.

---

## 9. Step-by-Step Workflow
1. **Step 1: Select Native / Zero-Dependency Test Runner**
   - Inspect project stack and configure standard test runner (Jest, Vitest, PyTest, Go test, Cargo test).
2. **Step 2: Configure Fixtures & Factories**
   - Create deterministic test helper libraries and data factories.
3. **Step 3: Setup CI Pipeline Stages**
   - Configure fast unit tests (< 1 min) before slower integration tests (< 5 mins).
4. **Step 4: Run Flakiness Stress Test**
   - Execute test suite 10 consecutive times locally; confirm 100% pass rate.
5. **Step 5: Document Automation Suite**
   - Update `docs_agent/testing/TEST_STRATEGY.md` with execution commands.

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
