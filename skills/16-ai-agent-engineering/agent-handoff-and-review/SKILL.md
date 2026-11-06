---
name: agent-handoff-and-review
description: "Structured context handoff protocols, verification checklists, state persistence, and loss-free continuity across agent boundaries and sessions."
version: 1.7.0
category: agentic
tags: ['agentic', 'handoff', 'continuity', 'state-persistence', 'session-log']
---

# Skill: Agent Handoff & Structured Review Briefing

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 16 — AI Agent Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `agent-handoff-and-review`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Structure context handoffs and review briefings between sequential or concurrent AI agents to prevent context loss.
- **When to Use**: Passing work from Agent A to Agent B, handing off tasks across sessions, or escalating blockers.
- **Essential Invariants**:
  1. Handoff payloads must include: original prompt, acceptance criteria, modified files list, and test commands.
  2. Never omit known limitations, failed tests, or unresolved edge cases from handoff payloads.
  3. Verification agents must re-read raw prompt and actual filesystem code, not merely handoff summary.
- **Minimal Workflow**:
  1. Compile structured handoff payload containing requirements, change inventory, and test commands.
  2. Transmit payload to receiving subagent or record in docs_agent/handoffs/.
  3. Receiving agent verifies payload contents against actual repository state.
  4. Receiving agent confirms receipt and begins independent evaluation pass.
- **Expected Deliverables**: Structured, complete handoff briefing payload with zero context loss.
- **Critical Restrictions**: Never truncate critical requirement context or conceal failing tests during agent handoff.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Guarantees seamless, lossless continuity when work transitions between different AI agent instances, specialized subagents, or human developers across sessions.

---

### Scope
- **In-Scope**:
  - Authoring structured session logs (`docs_agent/SESSION_LOG.md`)\n  - Maintaining the operational task state machine (`TASKS.md`)\n  - Persisting technical discoveries and traps in `MEMORY.md`\n  - Formatting explicit handoff briefings for receiving agents
- **Out-of-Scope**:
  - Ad-hoc unstructured chat messages without file persistence

---

### When to Use
- Concluding any agent work turn or milestone\n- Handing off a feature from Development Agent to QA or Security Agent\n- Resuming an existing codebase in a new agent chat session

---

### When Not to Use
- During rapid mid-turn tool call sequences within a single invocation

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
### 8.1 Mandatory Handoff Structure
Every session handoff must record:
1. **Objectives Addressed**: Explicit list of user prompts resolved.
2. **Files Inspected & Modified**: Verifiable list of touched files.
3. **Testing Evidence**: Commands run and pass/fail exit codes.
4. **Current State Machine**: Updated `TASKS.md` with active, completed, or blocked tasks.
5. **Known Traps / Discoveries**: New architectural lessons recorded in `MEMORY.md`.
6. **Recommended Next Actions**: Concrete, prioritized instructions for the receiving agent.

---

### Step-by-Step Workflow
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
