---
name: agent-role-separation
description: "Single-agent fallback protocols for clean role-switching passes, cognitive context wiping, distinct checklists, and bias elimination."
version: 1.0.0
category: agentic
tags: ['agentic', 'role-separation', 'single-agent', 'bias-elimination', 'checklists']
---

# Skill: Agent Role Separation

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 16 — AI Agent Engineering

---

## 1. Metadata
- **Identifier**: `agent-role-separation`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Provides structured cognitive isolation protocols enabling a single AI agent to execute separate, unbiased Development, QA, and Security passes without self-confirmation bias.

---

## 3. Scope
- **In-Scope**:
  - Executing distinct, sequential role-switching passes in single-agent environments\n  - Using role-specific checklists and orthogonal evaluation criteria\n  - Preventing implementation assumptions from leaking into QA or Security reviews\n  - Documenting role-separated handoffs within a single conversation session
- **Out-of-Scope**:
  - Native multi-agent concurrent execution (delegate to `skills/16-ai-agent-engineering/multi-agent-verification/SKILL.md`)

---

## 4. When to Use
- Operating in single-agent environments (e.g. Cursor, standard CLI chat, Copilot)\n- Conducting comprehensive development turns requiring self-contained QA and security review

---

## 5. When Not to Use
- When a native multi-agent harness is available and concurrent subagents can be spawned

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
### 8.1 The Single-Agent Role-Switch Protocol
When running as a single agent:
1. **Pass 1: Development Pass (Agent A)**:
   - Focus: Requirements, TDD Red-Green-Refactor, code implementation.
   - Output: Working code, unit tests, passing test suite.
2. **Pass 2: QA Audit Pass (Agent B - Role Switch)**:
   - Mindset Shift: Stop defending the code. Assume there are defects.
   - Action: Read the code as a third-party reviewer. Run edge case tests. Verify UI/UX Pro Max standards.
   - Output: `docs_agent/testing/QA_ASSESSMENT.md`.
3. **Pass 3: Security Review Pass (Agent C - Role Switch)**:
   - Mindset Shift: Adopt an adversarial persona. Hunt for injection, BOLA, XSS, and auth bypass.
   - Action: Probe trust boundaries and check authorization invariants.
   - Output: `docs_agent/security/SECURITY_ASSESSMENT.md`.

---

## 9. Step-by-Step Workflow
1. **Step 1: Complete Pass 1 (Development)**
   - Implement code following TDD. Ensure tests pass.
2. **Step 2: Explicit Context Wipe & Role Switch to QA**
   - Declare: "Switching role to Independent QA Agent".
   - Load QA checklist; independently run tests and audit edge cases.
3. **Step 3: Explicit Context Wipe & Role Switch to Security**
   - Declare: "Switching role to Independent Security Agent".
   - Load security checklist; adversarial audit and boundary verification.
4. **Step 4: Check Release Gates**
   - Confirm Functional, Regression, Security, and Documentation gates.
5. **Step 5: Final Integrated Report**
   - Present final deliverables to user with role-separated verification evidence.

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
