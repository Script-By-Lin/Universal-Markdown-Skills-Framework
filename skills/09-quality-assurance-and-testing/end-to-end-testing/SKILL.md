---
name: end-to-end-testing
description: "Automated end-to-end testing of user journeys across web browsers, mobile interfaces, and CLI workflows from start to finish."
version: 1.7.0
category: quality
tags: ['testing', 'e2e', 'playwright', 'cypress', 'browser-testing', 'user-journeys']
---

# Skill: End-to-End (E2E) Browser & Flow Testing

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `end-to-end-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Automate complete user journey workflows through actual browsers or client interfaces (Playwright, Cypress).
- **When to Use**: Validating critical user flows (signup, checkout, authentication) through real browser engines.
- **Essential Invariants**:
  1. E2E tests must rely on user-facing semantic locators (roles, text, accessible labels), not fragile CSS classes.
  2. Isolate test user accounts and data to prevent parallel execution collisions.
  3. Keep E2E suites lean and focused on high-value user journeys to minimize execution time.
- **Minimal Workflow**:
  1. Define critical path user journeys (e.g. registration -> login -> create resource -> export).
  2. Author Playwright/Cypress test scripts using semantic role locators.
  3. Execute tests in headless browser matrix (Chromium, Firefox, WebKit).
  4. Capture trace recordings and screenshots on unexpected failure for immediate triage.
- **Expected Deliverables**: Passing automated E2E test suite verifying critical user journeys.
- **Critical Restrictions**: Never use arbitrary hard-coded sleep timeouts; always use explicit event or selector assertions.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Ensures user-facing applications function flawlessly from the end-user perspective by automating complete browser and client interactions across realistic user flows.

---

### Scope
- **In-Scope**:
  - Automating browser journeys using headless engines (Playwright, Cypress, Puppeteer)\n  - Testing UI form submissions, navigation transitions, and real-time updates\n  - Verifying responsive viewports and cross-browser visual rendering\n  - Validating authentication sessions, cookies, and localStorage persistence
- **Out-of-Scope**:
  - Low-level algorithm verification testable via unit tests

---

### When to Use
- Building critical user conversion flows (signup, checkout, onboarding)\n- Validating complex interactive frontend components with rich client state\n- Running pre-release regression suites against staging deployments

---

### When Not to Use
- For backend-only services without user-facing interfaces

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
### 8.1 E2E Testing Best Practices
1. **Resilient Selectors**: Never bind tests to fragile CSS classes (`.btn-primary-v2-blue`). Use accessible roles and data-testid attributes:
   - Preferred: `page.getByRole('button', { name: 'Submit Order' })`
   - Secondary: `page.getByTestId('submit-order-button')`
2. **Avoid Arbitrary Timeouts**: Never write `sleep(5000)`. Always wait for explicit DOM conditions or network idle events (`waitForSelector`, `waitForResponse`).
3. **Test Data Isolation**: Every test run must generate its own unique test account or transaction data to avoid cross-test interference.
4. **UI/UX Pro Max Verification**: Verify responsive layout at 375px mobile and 1440px desktop with zero horizontal overflow.

---

### Step-by-Step Workflow
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
