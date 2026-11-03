---
name: agent-handoff-and-review
description: "Structured context handoff protocols, verification checklists, state persistence, and loss-free continuity across agent boundaries and sessions."
version: 1.0.0
category: agentic
tags: ['agentic', 'handoff', 'continuity', 'state-persistence', 'session-log']
---

# Skill: Agent Handoff And Review

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 16 — AI Agent Engineering

---

## 1. Metadata
- **Identifier**: `agent-handoff-and-review`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Integrations**:
  - [`independent-verification-subagent`](../independent-verification-subagent/SKILL.md)
  - [`independent-qa-agent`](../independent-qa-agent/SKILL.md)
  - [`multi-agent-verification`](../multi-agent-verification/SKILL.md)

---

## 2. Purpose
Guarantees seamless, lossless continuity when work transitions between different AI agent instances, specialized subagents, or human developers across sessions.

---

## 3. Scope
- **In-Scope**:
  - Authoring structured session logs (`docs_agent/SESSION_LOG.md`)\n  - Maintaining the operational task state machine (`TASKS.md`)\n  - Persisting technical discoveries and traps in `MEMORY.md`\n  - Formatting explicit handoff briefings for receiving agents
- **Out-of-Scope**:
  - Ad-hoc unstructured chat messages without file persistence

---

## 4. When to Use
- Concluding any agent work turn or milestone\n- Handing off a feature from Development Agent to QA or Security Agent\n- Resuming an existing codebase in a new agent chat session

---

## 5. When Not to Use
- During rapid mid-turn tool call sequences within a single invocation

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
### 8.1 Mandatory Handoff Structure
Every session handoff must record:
1. **Objectives Addressed**: Explicit list of user prompts resolved.
2. **Files Inspected & Modified**: Verifiable list of touched files.
3. **Testing Evidence**: Commands run and pass/fail exit codes.
4. **Current State Machine**: Updated `TASKS.md` with active, completed, or blocked tasks.
5. **Known Traps / Discoveries**: New architectural lessons recorded in `MEMORY.md`.
6. **Recommended Next Actions**: Concrete, prioritized instructions for the receiving agent.

---

## 9. Step-by-Step Workflow
1. **Step 1: Verify Task State in TASKS.md**
   - Ensure completed tasks are marked `Completed` and new items are `Pending`.
2. **Step 2: Capture Architectural Decisions**
   - If an architectural choice was made, verify ADR in `DECISIONS.md`.
3. **Step 3: Capture Lessons in MEMORY.md**
   - Document any pitfalls or non-obvious conventions.
4. **Step 4: Author Session Entry**
   - Append standardized entry to `docs_agent/SESSION_LOG.md`.
5. **Step 5: Provide Clean Summary to User**
   - Summarize deliverables and next steps clearly without conversational bloat.

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
