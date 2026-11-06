---
name: defect-management
description: "Structured defect logging, reproduction workflows, severity/priority assignment, root cause analysis, and resolution verification."
version: 1.7.0
category: quality
tags: ['testing', 'defects', 'bug-tracking', 'root-cause', 'triage', 'reproduction']
---

# Skill: Defect Tracking & Triage Lifecycle

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `defect-management`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Triage, classify, prioritize, track, and verify resolution of software bugs across their complete lifecycle.
- **When to Use**: Logging newly discovered bugs, conducting bug triage meetings, or managing the defect resolution lifecycle.
- **Essential Invariants**:
  1. Every defect report must contain minimal reproduction steps and expected vs actual behavior.
  2. Classify defects using standard severity tiers (Critical, Major, Minor, Informational).
  3. No defect may be marked Resolved without passing regression test verification.
- **Minimal Workflow**:
  1. Log defect with environment details, reproduction steps, and error logs.
  2. Triage severity and impact, assigning to appropriate milestone and owner.
  3. Verify that a failing regression test is authored to reproduce the bug.
  4. Verify defect fix in target environment and close report with empirical evidence.
- **Expected Deliverables**: Defect tracking record with verified reproduction, fix, and regression test evidence.
- **Critical Restrictions**: Never close a bug report as 'cannot reproduce' without attempting reproduction under documented conditions.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Establishes a rigorous operational workflow for logging, isolating, prioritizing, reproducing, and verifying defects discovered during testing or production operation.

---

### Scope
- **In-Scope**:
  - Capturing minimal, reproducible defect reproduction scripts\n  - Assigning standardized defect severity and business priority\n  - Conducting Root Cause Analysis (RCA) using the 5 Whys methodology\n  - Tracking defect state transitions through verification and closure
- **Out-of-Scope**:
  - Vulnerability management for security flaws (delegate to `skills/02-security-engineering/vulnerability-management/SKILL.md`)

---

### When to Use
- Triage and logging of software bugs discovered during testing or QA review\n- Managing bug reproduction and regression test authoring\n- Reviewing defect trends and quality health prior to release

---

### When Not to Use
- For logging security vulnerabilities with exploit PoCs (use `vulnerability-management`)

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
### 8.1 Defect Severity vs Priority
- **Severity (Technical Impact)**:
  - **S1 (Critical)**: Application crash, data loss, core workflow completely blocked with no workaround.
  - **S2 (Major)**: Important feature broken; workaround exists but is difficult.
  - **S3 (Minor)**: Non-critical feature broken or cosmetic defect.
  - **S4 (Trivial)**: Minor typo, alignment imperfection, or stylistic suggestion.
- **Priority (Business Urgency)**:
  - **P1 (Immediate)**: Fix immediately / hotfix candidate.
  - **P2 (High)**: Resolve in current milestone/sprint.
  - **P3 (Normal)**: Schedule for upcoming sprint.
  - **P4 (Low)**: Backlog / fix when convenient.

### 8.2 The Minimal Reproduction Standard
Every defect record must include:
1. **Prerequisites & Environment**: OS, browser, app version, database state.
2. **Steps to Reproduce**: Numbered, step-by-step exact actions.
3. **Expected Result**: What should have happened.
4. **Actual Result**: What actually happened (with stack trace or console error).
5. **Minimal Reproduction Code**: A standalone test or script reproducing the bug.

---

### Step-by-Step Workflow
1. **Step 1: Triage & Deduplication**
   - Check existing defect records to avoid duplicates.
2. **Step 2: Reproduce & Isolate**
   - Execute reproduction steps; confirm failure is consistent.
3. **Step 3: Assign Severity & Priority**
   - Rate S1-S4 and P1-P4; update `docs_agent/testing/QA_ASSESSMENT.md`.
4. **Step 4: Author Failing Regression Test**
   - Write automated test confirming the defect (TDD RED phase).
5. **Step 5: Verify Fix & Close**
   - Independent QA verifies fix and marks defect `Closed`.

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
