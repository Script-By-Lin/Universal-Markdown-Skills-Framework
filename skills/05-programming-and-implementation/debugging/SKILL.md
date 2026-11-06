---
name: debugging
description: Hypothesis-driven root cause analysis, reproduction scripts, diagnostic tracing, and verified remediation workflows.
version: 1.7.0
category: diagnostics
tags: [debugging, troubleshooting, root-cause, reproduction, logs, stack-trace]
---

# Skill: Systematic Defect Debugging

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 05 — Programming & Implementation  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `debugging`
- **Category**: Programming & Implementation (Domain 05)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Isolate, diagnose, and resolve runtime errors, performance bottlenecks, and logic defects using scientific root-cause analysis.
- **When to Use**: Investigating failing tests, stack traces, unhandled exceptions, memory leaks, or erratic system behavior.
- **Essential Invariants**:
  1. Reproduce the bug deterministically before attempting any code fix.
  2. Every bug fix must be preceded by an automated failing test (TDD Red-Green).
  3. Fix root causes; never apply superficial 'band-aid' patches that mask underlying flaws.
- **Minimal Workflow**:
  1. Gather stack traces, reproduction inputs, and environmental context.
  2. Formulate and test hypotheses to isolate the exact defect location.
  3. Author minimal failing unit/integration test reproducing the defect.
  4. Apply targeted code fix, verify test passes (Green), and check for regressions.
- **Expected Deliverables**: Passing regression test reproducing the original defect and targeted surgical code fix.
- **Critical Restrictions**: Never commit trial-and-error changes without understanding root cause; do not silence errors with bare catch blocks.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill provides a scientific, hypothesis-driven methodology for isolating bugs, analyzing stack traces, formulating minimal reproduction tests, identifying root causes, and executing verified fixes without collateral regressions.

---

### Scope
- **In-Scope**:
  - Analyzing exception logs, stack traces, and failure modes.
  - Formulating falsifiable diagnostic hypotheses.
  - Constructing minimal reproduction scripts or failing test cases.
  - Root-cause identification and targeted surgical remediation.
  - Authoring regression tests preventing bug recurrence.
- **Out-of-Scope**:
  - Broad system refactoring during a bugfix (delegate to [`skills/refactoring/SKILL.md`](../../refactoring/SKILL.md)).
  - Routine test suite authoring (delegate to [`skills/testing/SKILL.md`](../../testing/SKILL.md)).

---

### When to Use
- Whenever a test fails, an exception is thrown, or unexpected behavior is reported.
- During incident triage, performance regression investigation, or bug remediation.
- Stage 5 / Stage 6 bug fix lifecycles in [`WORKFLOW.md`](../../../WORKFLOW.md).

---

### When Not to Use
- When planning brand-new features with no existing defects.
- When pure styling adjustments are requested without defect symptoms.

---

### Prerequisites
- Error description, stack trace, or observed defect behavior available.
- Relevant source code inspected and verified against [`CONTEXT.md`](../../../CONTEXT.md).

---

### Required Context
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- Lessons learned and past bug discoveries in [`MEMORY.md`](../../../MEMORY.md).

---

### Core Instructions
1. **Never Guess or "Shotgun Debug"**:
   - Do not make random changes hoping the defect disappears. Formulate an explicit hypothesis before editing code.
2. **Reproduce First (Mandatory Invariant)**:
   - Before attempting any code fix, create a minimal failing test or reproduction script that reliably triggers the bug.
   - If you cannot reproduce the bug, you do not understand the bug.
3. **Isolate Variables**:
   - Change only one factor or line at a time to confirm or refute the hypothesis.
4. **Fix the Root Cause, Not the Symptom**:
   - Do not add `if (x == null) return;` if `x` should never have been null. Trace back to where `x` became invalid.
5. **Preserve Regression Test**:
   - The minimal reproduction test must be permanently added to the test suite to ensure the bug cannot silently regress.

---

### Step-by-Step Workflow
1. **Step 1: Defect Characterization**
   - Identify: What was expected vs. What actually occurred? Capture the exact inputs, error message, and stack trace.
2. **Step 2: Construct Minimal Reproduction Case**
   - Author an isolated unit test or scratch script demonstrating the failure. Verify that it fails.
3. **Step 3: Formulate Falsifiable Hypotheses**
   - Hypothesize: "The failure occurs because component X assumes condition Y, which is invalidated when input Z occurs."
4. **Step 4: Trace and Verify Root Cause**
   - Inspect variables, state transitions, or execution traces to confirm the hypothesis.
5. **Step 5: Apply Targeted Surgical Fix**
   - Make the minimal necessary change resolving the root cause.
6. **Step 6: Verify Reproduction Pass & Regression Suite**
   - Run the reproduction test; verify that it passes. Run the entire test suite; verify zero regressions.

---

### Quality Standards
- **Surgical Precision**: Diffs should be minimal, touching only the lines responsible for the defect.
- **Regression Immunization**: 100% of bugfixes accompanied by an automated test that originally failed.
- **Zero Side Effects**: Full test suite passes after fix is applied.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Reproduction Verification | Run reproduction test before fix | Test fails with reported defect |
| Fix Verification | Run reproduction test after fix | Test passes cleanly |
| Regression Invariance | Run entire project test suite | 100% test pass with zero new failures |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Fixing Without Reproduction | Agent assumes the cause, edits code, but fails to fix the actual bug | Always write the failing test first |
| Masking Errors (`catch {}` or `return null`) | Transforms loud errors into silent data corruption | Fix the state transition that caused the invalid data |

---

### Restrictions
- Do NOT modify unrelated codebase files during a bug fix.
- Do NOT delete existing tests to force a failing suite to pass.

---

### Expected Deliverables
- Targeted surgical bug fix in source code.
- Permanent regression test added to the test suite.
- Diagnostic explanation documented in commit or handoff log.

---

### Documentation Requirements
- Record recurring pitfalls and root-cause discoveries in [`MEMORY.md`](../../../MEMORY.md).
- Update task state in [`TASKS.md`](../../../TASKS.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
