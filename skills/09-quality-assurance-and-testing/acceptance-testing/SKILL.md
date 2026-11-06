---
name: acceptance-testing
description: "Verification of software against business requirements, Given-When-Then / BDD acceptance criteria, and stakeholder definition of done."
version: 1.7.0
category: quality
tags: ['testing', 'acceptance-testing', 'bdd', 'cucumber', 'definition-of-done']
---

# Skill: User Acceptance Testing (UAT)

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `acceptance-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Verify software behavior against business requirements, acceptance criteria, and stakeholder expectations.
- **When to Use**: Delivering feature milestones, validating user stories, or preparing client release handoffs.
- **Essential Invariants**:
  1. Acceptance tests must directly map 1:1 to written acceptance criteria in TASKS.md.
  2. Validate both positive acceptance flows and business rule rejection cases.
  3. Stakeholder or business representative approval criteria must be explicitly documented.
- **Minimal Workflow**:
  1. Extract Given-When-Then acceptance criteria from feature tasks.
  2. Author executable acceptance tests (Cucumber/Gherkin or native test assertions).
  3. Execute acceptance scenarios and generate human-readable verification log.
  4. Confirm all criteria pass before marking task Completed.
- **Expected Deliverables**: Passing acceptance test suite validating 100% of defined acceptance criteria.
- **Critical Restrictions**: Never mark user stories accepted without empirical validation evidence.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Validates that implemented software satisfies the explicit business requirements, user stories, and acceptance criteria agreed upon with project stakeholders.

---

### Scope
- **In-Scope**:
  - Formulating and verifying Given-When-Then acceptance criteria\n  - Validating business rules, calculations, and domain workflows\n  - Verifying non-functional acceptance criteria (accessibility, performance budgets)\n  - Ensuring compliance with the Definition of Done (DoD)
- **Out-of-Scope**:
  - Internal code structure refactoring without behavioral impact

---

### When to Use
- Conducting story verification before closing user backlog items\n- Reviewing milestone deliverables with product stakeholders\n- Verifying the Functional Release Gate

---

### When Not to Use
- For purely technical infrastructure migrations with no business rule changes

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

### Step-by-Step Workflow
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
