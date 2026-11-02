---
name: end-to-end-testing
description: "Automated end-to-end testing of user journeys across web browsers, mobile interfaces, and CLI workflows from start to finish."
version: 1.0.0
category: quality
tags: ['testing', 'e2e', 'playwright', 'cypress', 'browser-testing', 'user-journeys']
---

# Skill: End To End Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `end-to-end-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Ensures user-facing applications function flawlessly from the end-user perspective by automating complete browser and client interactions across realistic user flows.

---

## 3. Scope
- **In-Scope**:
  - Automating browser journeys using headless engines (Playwright, Cypress, Puppeteer)\n  - Testing UI form submissions, navigation transitions, and real-time updates\n  - Verifying responsive viewports and cross-browser visual rendering\n  - Validating authentication sessions, cookies, and localStorage persistence
- **Out-of-Scope**:
  - Low-level algorithm verification testable via unit tests

---

## 4. When to Use
- Building critical user conversion flows (signup, checkout, onboarding)\n- Validating complex interactive frontend components with rich client state\n- Running pre-release regression suites against staging deployments

---

## 5. When Not to Use
- For backend-only services without user-facing interfaces

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
### 8.1 E2E Testing Best Practices
1. **Resilient Selectors**: Never bind tests to fragile CSS classes (`.btn-primary-v2-blue`). Use accessible roles and data-testid attributes:
   - Preferred: `page.getByRole('button', { name: 'Submit Order' })`
   - Secondary: `page.getByTestId('submit-order-button')`
2. **Avoid Arbitrary Timeouts**: Never write `sleep(5000)`. Always wait for explicit DOM conditions or network idle events (`waitForSelector`, `waitForResponse`).
3. **Test Data Isolation**: Every test run must generate its own unique test account or transaction data to avoid cross-test interference.
4. **UI/UX Pro Max Verification**: Verify responsive layout at 375px mobile and 1440px desktop with zero horizontal overflow.

---

## 9. Step-by-Step Workflow
1. **Step 1: Define User Journey Script**
   - Identify critical path: login, navigate, complete task, verify confirmation.
2. **Step 2: Implement Automated Journey**
   - Author test script using resilient locators and explicit wait conditions.
3. **Step 3: Run Headless Across Viewports**
   - Execute tests at 375px (mobile) and 1280px (desktop).
4. **Step 4: Capture Traces & Screenshots on Failure**
   - Configure test runner to capture video or DOM traces when an assertion fails.
5. **Step 5: Integrate into PR Pipeline**
   - Ensure E2E suite runs reliably in CI with zero flaky failures.

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
