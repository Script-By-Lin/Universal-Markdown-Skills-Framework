---
name: testing
description: Comprehensive testing strategies, unit testing, integration boundaries, mock design, coverage expectations, and test reliability standards.
version: 1.7.0
category: quality
tags: [testing, unit-tests, integration-tests, mocks, tdd, regression, coverage]
---

# Skill: Comprehensive Software Testing Strategy

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Establish testing pyramids, quality gates, and automated test orchestration across all architectural tiers.
- **When to Use**: Setting up test infrastructure, defining repository testing standards, or conducting test suite audits.
- **Essential Invariants**:
  1. Maintain the testing pyramid: high-volume unit tests, targeted integration tests, lean E2E tests.
  2. All tests must be deterministic, isolated, and repeatable in CI/CD environments.
  3. Test runners must return exit code 0 on success and non-zero on failure.
- **Minimal Workflow**:
  1. Configure test runners (Jest, Vitest, Pytest, Go test) with parallel execution.
  2. Define test categorization tags (unit, integration, e2e, smoke).
  3. Establish CI/CD quality gates that block merges on any test failure.
  4. Monitor test suite duration and optimize slow or flaky test cases.
- **Expected Deliverables**: Configured test framework with automated CI/CD execution and passing baseline.
- **Critical Restrictions**: Never skip test execution in CI/CD pipelines; never ignore failing tests.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes universal standards for testing software systems across the test pyramid: unit tests for domain business logic, integration tests for persistence and network boundaries, and contract tests for APIs. It ensures determinism, isolates tests from external volatility, and prevents flaky tests.

---

### Scope
- **In-Scope**:
  - Designing and authoring unit tests, integration tests, and regression tests.
  - Applying Test-Driven Development (TDD) workflows (Red-Green-Refactor).
  - Designing isolated mocks, stubs, and fixtures for external boundaries.
  - Measuring code coverage and identifying untested edge cases.
- **Out-of-Scope**:
  - Defect root-cause investigation (delegate to [`skills/debugging/SKILL.md`](../../debugging/SKILL.md)).
  - Automated deployment CI pipeline infrastructure (infrastructure concern).

---

### When to Use
- Authoring tests for new features, endpoints, or data models.
- Increasing test coverage for legacy or fragile modules.
- Executing Stage 6 of the canonical lifecycle in [`WORKFLOW.md`](../../../WORKFLOW.md).

---

### When Not to Use
- When analyzing purely conceptual requirements before code structures exist.

---

### Prerequisites
- Target code module or interface available for testing.
- Test runner and framework identified in [`CONTEXT.md`](../../../CONTEXT.md) (e.g. Jest, Pytest, Go test, JUnit).

---

### Required Context
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- Past testing lessons recorded in [`MEMORY.md`](../../../MEMORY.md).

---

### Core Instructions
1. **The Test Pyramid**:
   - Maintain a heavy base of fast, isolated **Unit Tests** (70–80%).
   - Maintain a moderate layer of **Integration Tests** verifying database queries and API routes (15–20%).
   - Maintain a lean set of critical **End-to-End Tests** (5–10%).
2. **Determinism (Zero Flakiness)**:
   - Tests must produce the exact same outcome on every run.
   - Never use real network calls, real sleep timers, or unseeded random generators in tests.
3. **The AAA Pattern (Arrange-Act-Assert)**:
   - Every test must clearly partition its structure:
     - **Arrange**: Set up fixtures, inputs, and mock expectations.
     - **Act**: Invoke the single method under test.
     - **Assert**: Verify return values, side effects, or error states.
4. **Test Boundaries & Mocking**:
   - Mock only external boundaries (payment processors, third-party APIs, disk I/O, email gateways).
   - Do NOT mock internal domain logic; test real domain objects together whenever possible.

---

### Step-by-Step Workflow
1. **Step 1: Identify Target Invariants & Boundaries**
   - Review function signature, input domain, edge cases (empty strings, zero, negative numbers, max values), and error states.
2. **Step 2: Author Unit Tests (Red Stage)**
   - Write tests exercising happy paths and edge cases. Verify that tests fail if code is missing or broken.
3. **Step 3: Implement Code Under Test (Green Stage)**
   - Implement the minimal necessary logic to satisfy test assertions.
4. **Step 4: Refactor with Test Safety (Refactor Stage)**
   - Clean up code, remove duplication, and optimize while keeping tests green.
5. **Step 5: Run Full Test Suite**
   - Execute the entire project test suite to verify zero regressions.

---

### Quality Standards
- **Isolation**: Each test runs independently; tests can run in parallel without shared state collisions.
- **Speed**: Unit tests execute in milliseconds.
- **Clarity**: Test failure output states clearly what was expected versus what was received.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Determinism Check | Execute test suite 3 consecutive times | 100% pass rate on all 3 runs (zero flaky tests) |
| Edge Case Coverage | Inspect tests for null/empty/boundary inputs | All boundary conditions covered by explicit assertions |
| Mock Isolation | Check network activity during test run | Zero outgoing network requests |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Testing Implementation Details | Tests break during harmless refactorings | Test observable behavior and public interfaces |
| Timeouts / Sleep in Tests | Causes random test failures on slow CI runners | Use deterministic polling or event-based assertions |
| Over-Mocking Domain Objects | Tests pass while real integrated components fail | Mock only at external I/O boundaries |

---

### Restrictions
- Do NOT delete or disable failing tests to fake a passing suite.
- Do NOT make live network requests to production APIs during testing.

---

### Expected Deliverables
- Comprehensive unit and integration test files.
- Verified test execution reports.

---

### Documentation Requirements
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Update test tasks in [`TASKS.md`](../../../TASKS.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
