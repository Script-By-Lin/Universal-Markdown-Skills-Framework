---
name: defect-management
description: "Structured defect logging, reproduction workflows, severity/priority assignment, root cause analysis, and resolution verification."
version: 1.0.0
category: quality
tags: ['testing', 'defects', 'bug-tracking', 'root-cause', 'triage', 'reproduction']
---

# Skill: Defect Management

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `defect-management`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Establishes a rigorous operational workflow for logging, isolating, prioritizing, reproducing, and verifying defects discovered during testing or production operation.

---

## 3. Scope
- **In-Scope**:
  - Capturing minimal, reproducible defect reproduction scripts\n  - Assigning standardized defect severity and business priority\n  - Conducting Root Cause Analysis (RCA) using the 5 Whys methodology\n  - Tracking defect state transitions through verification and closure
- **Out-of-Scope**:
  - Vulnerability management for security flaws (delegate to `skills/02-security-engineering/vulnerability-management/SKILL.md`)

---

## 4. When to Use
- Triage and logging of software bugs discovered during testing or QA review\n- Managing bug reproduction and regression test authoring\n- Reviewing defect trends and quality health prior to release

---

## 5. When Not to Use
- For logging security vulnerabilities with exploit PoCs (use `vulnerability-management`)

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

## 9. Step-by-Step Workflow
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
