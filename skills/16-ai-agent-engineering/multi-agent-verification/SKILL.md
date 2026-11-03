---
name: multi-agent-verification
description: "Orchestration patterns for concurrent multi-agent collaboration: Dev -> QA -> Security handoff loops, consensus protocols, and dispute resolution."
version: 1.0.0
category: agentic
tags: ['agentic', 'multi-agent', 'orchestration', 'consensus', 'handoff', 'verification']
---

# Skill: Multi Agent Verification

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 16 — AI Agent Engineering

---

## 1. Metadata
- **Identifier**: `multi-agent-verification`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Integrations**:
  - [`independent-verification-subagent`](../independent-verification-subagent/SKILL.md)
  - [`independent-qa-agent`](../independent-qa-agent/SKILL.md)
  - [`independent-security-review-agent`](../independent-security-review-agent/SKILL.md)

---

## 2. Purpose
Provides structured interaction protocols, handoff contracts, and dispute resolution rules for environments running multiple specialized AI agents concurrently.

---

## 3. Scope
- **In-Scope**:
  - Defining the structured tripartite handoff pipeline (Dev -> QA -> Security -> Release)\n  - Establishing evidence exchange protocols between specialized agents\n  - Resolving disagreements between Development and QA/Security agents\n  - Enforcing consensus gates prior to declaring tasks complete
- **Out-of-Scope**:
  - Single-agent serial pass workflows (delegate to `skills/16-ai-agent-engineering/agent-role-separation/SKILL.md`)

---

## 4. When to Use
- Running within multi-agent agentic platforms (e.g. Antigravity subagents, Claude Code agent teams)\n- Orchestrating concurrent automated code review pipelines

---

## 5. When Not to Use
- In constrained single-agent CLI sessions

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
### 8.1 Tripartite Verification Pipeline
```
[Agent A: Dev] --(Code + TDD Suite)--> [Agent B: QA]
                                            | (QA Signoff)
                                            v
                                       [Agent C: Security]
                                            | (Security Signoff)
                                            v
                                       [Release Gate Consensus]
```

### 8.2 Dispute Resolution Protocol
If Agent A (Dev) disputes an issue raised by Agent B (QA) or Agent C (Security):
1. **Evidence is Sovereign**: If QA or Security provides a reproducible failing test script or PoC, the finding is valid and Dev must remediate. Speculative debate is disallowed.
2. **Precedence Hierarchy**: Rules in `RULES.md` (Level 2) strictly override developer preference.
3. **Escalation**: If disagreement persists regarding business requirement interpretation, escalate to User with an explicit, neutral question.

---

## 9. Step-by-Step Workflow
1. **Step 1: Agent A Dispatches Deliverables**
   - Dev commits code and tests, updates `TASKS.md`, and notifies QA Agent.
2. **Step 2: Agent B Executes Independent QA Audit**
   - QA pulls branch, runs tests, checks edge cases, logs review in `QA_ASSESSMENT.md`.
3. **Step 3: Agent C Executes Security Evaluation**
   - Security agent probes attack surfaces, checks authorization, updates `SECURITY_ASSESSMENT.md`.
4. **Step 4: Remediation Loop (if required)**
   - If QA or Security rejects, control returns to Agent A with exact reproduction steps.
5. **Step 5: Consensus Gate Signoff**
   - All three agents verify release gates before marking milestone Complete.

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
