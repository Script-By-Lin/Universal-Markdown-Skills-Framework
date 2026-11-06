---
name: multi-agent-verification
description: "Orchestration patterns for concurrent multi-agent collaboration: Dev -> QA -> Security handoff loops, consensus protocols, and dispute resolution."
version: 1.7.0
category: agentic
tags: ['agentic', 'multi-agent', 'orchestration', 'consensus', 'handoff', 'verification']
---

# Skill: Multi-Agent Verification Architecture

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 16 — AI Agent Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `multi-agent-verification`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Orchestrate multi-agent collaborative verification loops between Development (A), Verification (B), and Security (C).
- **When to Use**: Executing high-complexity features, architectural migrations, or enterprise releases requiring multi-role consensus.
- **Essential Invariants**:
  1. Enforce strict role separation: Agent A implements, Agent B verifies, Agent C audits security.
  2. All agent communications and handoffs must use structured, evidence-based payloads.
  3. Maximum of 3 remediation iterations between Agent A and Agent B before escalating as Blocked.
- **Minimal Workflow**:
  1. Agent A implements feature via TDD and compiles handoff briefing.
  2. Agent B independently executes 7-dimensional verification audit.
  3. Agent C conducts adversarial security review if security-sensitive scope is touched.
  4. Agents reach tri-state consensus (VERIFIED) or trigger surgical remediation loop.
- **Expected Deliverables**: Consensus verification report with independent sign-offs from Verification and Security roles.
- **Critical Restrictions**: Never collapse agent roles into a single unverified pass; honest attribution is mandatory in single-agent environments.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides structured interaction protocols, handoff contracts, and dispute resolution rules for environments running multiple specialized AI agents concurrently.

---

### Scope
- **In-Scope**:
  - Defining the structured tripartite handoff pipeline (Dev -> QA -> Security -> Release)\n  - Establishing evidence exchange protocols between specialized agents\n  - Resolving disagreements between Development and QA/Security agents\n  - Enforcing consensus gates prior to declaring tasks complete
- **Out-of-Scope**:
  - Single-agent serial pass workflows (delegate to `skills/16-ai-agent-engineering/agent-role-separation/SKILL.md`)

---

### When to Use
- Running within multi-agent agentic platforms (e.g. Antigravity subagents, Claude Code agent teams)\n- Orchestrating concurrent automated code review pipelines

---

### When Not to Use
- In constrained single-agent CLI sessions

---

### Prerequisites
- Framework architecture verified in [`AGENTS.md`](../../../AGENTS.md).
- Active tasks registered in [`TASKS.md`](../../../TASKS.md).
- Environment reality verified in [`CONTEXT.md`](../../../CONTEXT.md).

---

### Required Context
Before executing this skill, verify:
- Independent agent role specifications in [`AGENTS.md`](../../../AGENTS.md) Section 2.
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (Precedence Level 2).
- Release gate requirements in [`WORKFLOW.md`](../../../WORKFLOW.md).

---

### Core Instructions
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

### Step-by-Step Workflow
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

### Quality Standards
- **Standard 1**: Complete cognitive and evidence independence between Development and Review roles.
- **Standard 2**: Absolute prohibition on accepting conversational completion claims without empirical command verification.
- **Standard 3**: Seamless multi-agent continuity backed by persisted records in `docs_agent/` and `TASKS.md`.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Role Independence | Review checklist inspection | QA and Security passes execute separate review criteria |
| Evidence Verification | Command log inspection | Test exit code 0 and tool logs verified before signoff |
| Gate Compliance | Release gate checklist audit | All four release gates satisfied with inspectable proof |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Developer Self-Approval | High rate of confirmation bias and overlooked edge cases | Enforce independent QA/Security role passes |
| Trusting Conversational Assurances | Unexecuted code breaks in production | Verify raw terminal execution output and exit codes |
| Skipping Single-Agent Passes | Results in untested and insecure code | Execute explicit sequential role-switching passes |

---

### Restrictions
- Do NOT declare features approved without independent verification.
- Do NOT fabricate command outputs, test runs, or security assessment verdicts.
- Do NOT bypass release gates.

---

### Expected Deliverables
- Role-separated assessment logs under `docs_agent/testing/` or `docs_agent/security/`.
- Updated `TASKS.md` with validated milestone statuses.
- Structured session handoff entries in `docs_agent/SESSION_LOG.md`.

---

### Documentation Requirements
- Record reusable multi-agent lessons in [`MEMORY.md`](../../../MEMORY.md).
- Record agent orchestration trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Log session handoff in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
