---
name: acceptance-testing
description: "Verification of software against business requirements, Given-When-Then / BDD acceptance criteria, and stakeholder definition of done."
version: 1.0.0
category: quality
tags: ['testing', 'acceptance-testing', 'bdd', 'cucumber', 'definition-of-done']
---

# Skill: Acceptance Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `acceptance-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Validates that implemented software satisfies the explicit business requirements, user stories, and acceptance criteria agreed upon with project stakeholders.

---

## 3. Scope
- **In-Scope**:
  - Formulating and verifying Given-When-Then acceptance criteria\n  - Validating business rules, calculations, and domain workflows\n  - Verifying non-functional acceptance criteria (accessibility, performance budgets)\n  - Ensuring compliance with the Definition of Done (DoD)
- **Out-of-Scope**:
  - Internal code structure refactoring without behavioral impact

---

## 4. When to Use
- Conducting story verification before closing user backlog items\n- Reviewing milestone deliverables with product stakeholders\n- Verifying the Functional Release Gate

---

## 5. When Not to Use
- For purely technical infrastructure migrations with no business rule changes

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
### 8.1 Given-When-Then Criteria Structure
Express and verify acceptance criteria in BDD format:
- **Given** [an initial context / state of the world]
- **When** [a specific action or event occurs]
- **Then** [an observable outcome / state change must result]

Example:
```gherkin
Scenario: Premium user receives expedited dispatch
  Given an authenticated user with subscription tier "premium"
  And a cart containing physical items totaling $50
  When the user submits the checkout order
  Then the order shipping method is set to "Expedited Next-Day"
  And the shipping fee is charged as $0.00
```

---

## 9. Step-by-Step Workflow
1. **Step 1: Criteria Extraction**
   - Read user story specification; extract all acceptance criteria.
2. **Step 2: Automated Acceptance Test Formulation**
   - Map each scenario to an executable test asserting the exact outcome.
3. **Step 3: Execute Acceptance Suite**
   - Run tests against staging or local test instance.
4. **Step 4: Acceptance Audit & Signoff**
   - Check off each criterion in `docs_agent/testing/QA_ASSESSMENT.md`.
5. **Step 5: Gate Approval**
   - Certify that the Functional Release Gate is satisfied.

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
