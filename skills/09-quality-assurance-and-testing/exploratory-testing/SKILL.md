---
name: exploratory-testing
description: "Structured, time-boxed, charter-driven exploratory testing, unscripted edge-case discovery, heuristic probing, and anomaly reporting."
version: 1.7.0
category: quality
tags: ['testing', 'exploratory-testing', 'charter', 'heuristics', 'edge-cases']
---

# Skill: Exploratory & Edge-Case Testing

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `exploratory-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Simultaneously learn, design, and execute tests to discover unscripted defects, boundary failures, and usability traps.
- **When to Use**: Testing complex new workflows, evaluating UI responsiveness, or hunting elusive edge cases.
- **Essential Invariants**:
  1. Exploratory testing must be time-boxed with clear mission charters.
  2. Document all discovered defects with exact reproduction steps and environment details.
  3. Convert high-value exploratory discoveries into permanent automated regression tests.
- **Minimal Workflow**:
  1. Formulate exploratory test charter (target module, risk heuristic, time box).
  2. Exercise application with varied inputs, boundary conditions, and unexpected user behaviors.
  3. Log anomalies, unexpected delays, visual glitches, or unhandled exceptions.
  4. Author regression tests and bug tickets for verified defects.
- **Expected Deliverables**: Exploratory test debrief notes and bug tickets with reproduction tests.
- **Critical Restrictions**: Never perform unstructured, aimless clicking without a defined charter and recorded observations.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Discovers unexpected defects, usability gaps, and edge-case anomalies that automated and scripted test suites fail to anticipate, using disciplined human-like exploration.

---

### Scope
- **In-Scope**:
  - Formulating time-boxed exploratory testing charters\n  - Applying testing heuristics (boundary testing, extreme inputs, interrupted flows)\n  - Probing unexpected user interaction sequences and rapid back-button usage\n  - Documenting reproducible defect logs for newly discovered edge cases
- **Out-of-Scope**:
  - Repetitive regression testing automated via CI/CD scripts

---

### When to Use
- Evaluating a newly developed feature before formal release signoff\n- Investigating subtle user-reported bugs that evade automated tests\n- Testing complex UI workflows and stateful multi-step wizards

---

### When Not to Use
- When deterministic automated tests already exist and simply need re-running

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
### 8.1 Charter-Driven Exploratory Sessions
Structure sessions with an explicit charter, time box (e.g. 30-45 minutes), and target:
- **Charter**: *Explore [target component / workflow] with [heuristics / inputs] to discover [potential risks / failures].*
- **Heuristic Exploration Categories**:
  1. **Interruption**: Disconnect network mid-upload, refresh browser during payment processing, back-navigate during form submission.
  2. **Data Extremes**: Submit 10,000-character strings, Unicode emojis, zero values, negative numbers, leap-year dates.
  3. **Concurrency**: Trigger simultaneous requests from multiple tabs using the same session.
  4. **Accessibility**: Navigate with keyboard only, inspect with 200% browser zoom, test high-contrast modes.

---

### Step-by-Step Workflow
1. **Step 1: Draft Session Charter**
   - Define scope, persona, and target risks.
2. **Step 2: Time-Boxed Exploration**
   - Execute unscripted interactions while taking detailed behavioral notes.
3. **Step 3: Isolate & Reproduce Anomalies**
   - When an unexpected failure occurs, isolate the minimal reproduction steps.
4. **Step 4: Log Discovered Defects**
   - Create formal defect entries in `docs_agent/testing/QA_ASSESSMENT.md`.
5. **Step 5: Author Regression Tests**
   - Convert reproducible findings into permanent automated regression tests.

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
