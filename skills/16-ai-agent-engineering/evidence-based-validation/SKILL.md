---
name: evidence-based-validation
description: "Verification protocol requiring empirical proof (test execution logs, exit codes, diffs) before accepting completion claims."
version: 1.0.0
category: agentic
tags: ['agentic', 'validation', 'empirical-evidence', 'verification', 'quality-gate']
---

# Skill: Evidence Based Validation

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 16 — AI Agent Engineering

---

## 1. Metadata
- **Identifier**: `evidence-based-validation`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Enforces an uncompromising empirical verification standard across the framework: no task, test, or security claim is accepted without inspectable evidence.

---

## 3. Scope
- **In-Scope**:
  - Requiring command execution logs and exit code 0 for passing tests\n  - Validating filesystem changes directly using file reads and git status\n  - Rejecting speculative or conversational assertions of completion\n  - Verifying that documentation matches actual code reality
- **Out-of-Scope**:
  - Blindly accepting conversational assurances without tooling verification

---

## 4. When to Use
- Evaluating whether a development task is ready to transition to Completed\n- Conducting QA and Security release gate reviews\n- Auditing pull requests and commits

---

## 5. When Not to Use
- When brainstorming conceptual ideas before execution begins

---

## 6. Prerequisites
- Framework architecture verified in [`AGENTS.md`](../../../AGENTS.md).
- Active tasks registered in [`TASKS.md`](../../../TASKS.md).
- Environment reality verified in [`CONTEXT.md`](../../../CONTEXT.md).

---

## 7. Required Context
Before executing this skill, verify:
- Independent agent role specifications in [`AGENTS.md`](../../../AGENTS.md) Section 2.
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (Precedence Level 2).
- Release gate requirements in [`WORKFLOW.md`](../../../WORKFLOW.md).

---

## 8. Core Instructions
### 8.1 The Empirical Evidence Standard
- **The Rule of Proof**: "If you didn't execute it, you don't know if it works. If you can't show the exit code, you can't claim it passed."
- **Required Evidence Artifacts**:
  1. **Test Verification**: Terminal output showing test count, duration, and `Exit code 0`.
  2. **Code Change Verification**: `git status` or file diff showing exact modified lines.
  3. **Lint & Type Check**: Clean compiler/transpiler output with zero errors.
  4. **Security Verification**: Clean retest log demonstrating exploit rejection.

---

## 9. Step-by-Step Workflow
1. **Step 1: Identify Expected Evidence**
   - Determine what proof demonstrates task completion.
2. **Step 2: Execute Verification Command**
   - Run test runner, build command, or security probe in terminal.
3. **Step 3: Inspect Raw Output & Exit Code**
   - Confirm exit code is 0; inspect output for hidden warnings or skipped tests.
4. **Step 4: Cross-Check Against Code Reality**
   - Read modified source files to verify changes align with documentation.
5. **Step 5: Certify Verification**
   - Record pass/fail verdict with evidence citation in `docs_agent/`.

---

## 10. Quality Standards
- **Standard 1**: Complete cognitive and evidence independence between Development and Review roles.
- **Standard 2**: Absolute prohibition on accepting conversational completion claims without empirical command verification.
- **Standard 3**: Seamless multi-agent continuity backed by persisted records in `docs_agent/` and `TASKS.md`.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Role Independence | Review checklist inspection | QA and Security passes execute separate review criteria |
| Evidence Verification | Command log inspection | Test exit code 0 and tool logs verified before signoff |
| Gate Compliance | Release gate checklist audit | All four release gates satisfied with inspectable proof |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Developer Self-Approval | High rate of confirmation bias and overlooked edge cases | Enforce independent QA/Security role passes |
| Trusting Conversational Assurances | Unexecuted code breaks in production | Verify raw terminal execution output and exit codes |
| Skipping Single-Agent Passes | Results in untested and insecure code | Execute explicit sequential role-switching passes |

---

## 13. Restrictions
- Do NOT declare features approved without independent verification.
- Do NOT fabricate command outputs, test runs, or security assessment verdicts.
- Do NOT bypass release gates.

---

## 14. Expected Deliverables
- Role-separated assessment logs under `docs_agent/testing/` or `docs_agent/security/`.
- Updated `TASKS.md` with validated milestone statuses.
- Structured session handoff entries in `docs_agent/SESSION_LOG.md`.

---

## 15. Documentation Requirements
- Record reusable multi-agent lessons in [`MEMORY.md`](../../../MEMORY.md).
- Record agent orchestration trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Log session handoff in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).
