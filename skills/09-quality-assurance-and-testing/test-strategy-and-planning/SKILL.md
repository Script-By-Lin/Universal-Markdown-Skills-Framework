---
name: test-strategy-and-planning
description: "Formulating comprehensive, risk-based test strategies, testing levels matrix, environment prerequisites, quality budgets, and release criteria."
version: 1.7.0
category: quality
tags: ['testing', 'test-strategy', 'planning', 'risk-management', 'quality-plan']
---

# Skill: Test Strategy & Quality Engineering Planning

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `test-strategy-and-planning`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Define comprehensive quality engineering strategies, testing scopes, tooling selections, and risk-based test plans.
- **When to Use**: Initiating major projects, overhauling quality engineering practices, or preparing compliance test plans.
- **Essential Invariants**:
  1. Align test strategy with system architecture, deployment cadence, and business risk profile.
  2. Define explicit entry and exit quality criteria for each development stage.
  3. Integrate automated verification gates into developer local loops and CI/CD.
- **Minimal Workflow**:
  1. Assess system architecture, technologies, and critical quality risks.
  2. Define testing levels, frameworks, environments, and data strategies.
  3. Establish quality metrics, SLAs, and release gating criteria.
  4. Document strategy in project quality standards and configure CI pipelines.
- **Expected Deliverables**: Comprehensive Test Strategy document and configured quality gate pipeline.
- **Critical Restrictions**: Never treat testing as an afterthought deferred until after code completion.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Establishes the overarching quality strategy for software projects, defining testing levels, tooling choices, risk prioritization, and release gate criteria.

---

### Scope
- **In-Scope**:
  - Authoring comprehensive project test plans (`docs_agent/testing/TEST_STRATEGY.md`)\n  - Mapping the Testing Pyramid (Unit, Integration, E2E) to project architecture\n  - Defining environment prerequisites, test data strategies, and tooling selection\n  - Establishing quality gate thresholds and sign-off criteria
- **Out-of-Scope**:
  - Individual test case code implementation

---

### When to Use
- Initiating a new project, major architectural pivot, or greenfield service\n- Establishing engineering standards and testing culture across a team\n- Conducting project kickoff reviews

---

### When Not to Use
- For minor day-to-day bug fixes

---

### Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in [`TASKS.md`](../../../TASKS.md).

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (TDD invariants & Release Gates).
- Testing environment in [`CONTEXT.md`](../../../CONTEXT.md).
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

### Core Instructions
### 8.1 The Testing Pyramid Strategy
Distribute automated testing according to the standard pyramid:
- **Unit Tests (70%)**: Fast, deterministic, in-memory, zero I/O. Verifies domain logic.
- **Integration Tests (20%)**: Multi-component, real database/ORM, API contracts. Verifies boundaries.
- **End-to-End Tests (10%)**: Top critical user journeys, headless browser. Verifies business integration.

### 8.2 Risk-Based Testing Prioritization
Allocate testing effort based on business risk (Probability x Impact):
- **Critical Risk (High P x High I)**: Authentication, payment transactions, customer data persistence -> 100% automated coverage + security audit.
- **Medium Risk**: Analytics, reporting, email notifications -> Standard unit and integration coverage.
- **Low Risk**: Internal developer tooling, static marketing views -> Basic smoke testing.

---

### Step-by-Step Workflow
1. **Step 1: Architecture & Risk Intake**
   - Review project architecture and business risk profiles.
2. **Step 2: Formulate Testing Levels Matrix**
   - Define which layers require unit, integration, E2E, performance, and security testing.
3. **Step 3: Tooling & Framework Selection**
   - Select native, zero-dependency, or existing installed test runners.
4. **Step 4: Establish Release Gates**
   - Define exact exit criteria for Functional, Regression, Security, and Documentation gates.
5. **Step 5: Publish Test Strategy Document**
   - Author `docs_agent/testing/TEST_STRATEGY.md`.

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
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Record testing architectural trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
