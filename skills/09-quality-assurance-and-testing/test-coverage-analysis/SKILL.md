---
name: test-coverage-analysis
description: "Measurement, analysis, and optimization of code coverage metrics (statement, branch, function, line) to identify untested critical paths."
version: 1.0.0
category: quality
tags: ['testing', 'code-coverage', 'metrics', 'branch-coverage', 'risk-analysis']
---

# Skill: Test Coverage Analysis

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `test-coverage-analysis`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Analyzes test coverage data to discover blind spots in testing suites, ensuring that high-risk business logic and error handlers are thoroughly exercised by automated tests.

---

## 3. Scope
- **In-Scope**:
  - Executing coverage instrumentation tools across supported languages\n  - Analyzing statement, branch, function, and condition coverage\n  - Identifying untested error handling and boundary rejection branches\n  - Establishing meaningful coverage thresholds without rewarding vanity metrics
- **Out-of-Scope**:
  - Writing production application code

---

## 4. When to Use
- Conducting pre-merge code review on new pull requests\n- Evaluating regression safety before major architectural refactoring\n- Auditing legacy codebases to identify untested critical paths

---

## 5. When Not to Use
- Using raw percentage coverage as a replacement for high-quality assertions

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
### 8.1 Meaningful Coverage vs Vanity Metrics
- **Branch Coverage is Paramount**: 100% line coverage can still miss 50% of logic if conditional branches (`if/else`, switch cases, ternary operators) are unexercised. Always optimize for **branch and condition coverage**.
- **Error Handling Coverage**: Pay special attention to `catch`, `except`, and non-happy-path error branches—these frequently harbor unhandled bugs.
- **Coverage Target Invariants**:
  - Critical Business Logic / Financial Engines: **≥ 95% branch coverage**.
  - General Services & Controllers: **≥ 80% branch coverage**.
  - Pure Type Declarations / Boilerplate Config: Exclude from coverage metrics.

---

## 9. Step-by-Step Workflow
1. **Step 1: Run Coverage Instrumentation**
   - Execute project test suite with coverage flag (e.g. `npm test -- --coverage`, `pytest --cov`, `go test -coverprofile`).
2. **Step 2: Inspect Coverage Report**
   - Identify files and functions with sub-threshold branch coverage.
3. **Step 3: Identify Untested Critical Paths**
   - Examine red/uncovered lines in HTML or terminal coverage summaries.
4. **Step 4: Author Targeted Edge Case Tests**
   - Add unit tests specifically exercising the uncovered conditional paths.
5. **Step 5: Document Coverage Metrics**
   - Record coverage statistics in `docs_agent/testing/COVERAGE_REPORT.md`.

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
