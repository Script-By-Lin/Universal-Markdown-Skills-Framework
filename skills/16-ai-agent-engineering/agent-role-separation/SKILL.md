---
name: agent-role-separation
description: "Single-agent fallback protocols for clean role-switching passes, cognitive context wiping, distinct checklists, and bias elimination."
version: 1.7.0
category: agentic
tags: ['agentic', 'role-separation', 'single-agent', 'bias-elimination', 'checklists']
---

# Skill: Agent Role Separation & Cognitive Isolation

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 16 — AI Agent Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `agent-role-separation`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Enforce cognitive isolation and boundary separation between Development, QA, and Security agent personas.
- **When to Use**: Configuring subagent harnesses, defining agent system prompts, or orchestrating multi-agent teams.
- **Essential Invariants**:
  1. Development agents must focus strictly on implementation and minimal local developer tests.
  2. Verification agents must possess zero stake in defending implementation choices.
  3. Isolate subagent context windows to prevent memory pollution and cognitive confirmation bias.
- **Minimal Workflow**:
  1. Define distinct system prompts and tool access for each agent role.
  2. Pass only verified requirements, acceptance criteria, and git diffs to verification agents.
  3. Prevent verification agents from inheriting internal reasoning or rationalizations of developer agent.
  4. Audit role boundary adherence in session logs.
- **Expected Deliverables**: Isolated agent role configurations with verified context boundary enforcement.
- **Critical Restrictions**: Never allow an agent to evaluate its own work within the same uninterrupted cognitive context.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides structured cognitive isolation protocols enabling a single AI agent to execute separate, unbiased Development, QA, and Security passes without self-confirmation bias.

---

### Scope
- **In-Scope**:
  - Executing distinct, sequential role-switching passes in single-agent environments\n  - Using role-specific checklists and orthogonal evaluation criteria\n  - Preventing implementation assumptions from leaking into QA or Security reviews\n  - Documenting role-separated handoffs within a single conversation session
- **Out-of-Scope**:
  - Native multi-agent concurrent execution (delegate to `skills/16-ai-agent-engineering/multi-agent-verification/SKILL.md`)

---

### When to Use
- Operating in single-agent environments (e.g. Cursor, standard CLI chat, Copilot)\n- Conducting comprehensive development turns requiring self-contained QA and security review

---

### When Not to Use
- When a native multi-agent harness is available and concurrent subagents can be spawned

---

### Prerequisites
- Framework architecture verified in `AGENTS.md`.
- Active tasks registered in `TASKS.md`.
- Environment reality verified in `CONTEXT.md`.

---

### Required Context
Before executing this skill, verify:
- Independent agent role specifications in `AGENTS.md` Section 2.
- Mandatory constraints in `RULES.md` (Precedence Level 2).
- Release gate requirements in `WORKFLOW.md`.

---

### Core Instructions
### 8.1 The Single-Agent Role-Switch Protocol
When running in a single-agent environment where concurrent subagents are unavailable:
1. **Pass 1: Primary Development Pass (Agent A)**:
   - Focus: Requirements, TDD Red-Green-Refactor, code implementation, developer unit tests.
   - Deliverable: Working code, developer test evidence, and structured handoff briefing.
   - **Invariant**: Agent A must never declare its own work independently approved or secure.
2. **Pass 2: Independent Verification Pass (Agent B - Role Switch)**:
   - Mindset Shift: Stop defending the code. Assume defect presence. Re-read original user prompt from scratch.
   - Action: Execute the 7-dimensional audit from [`independent-verification-subagent`](../../independent-verification-subagent/SKILL.md) (Requirements, Diff Sweep, Architecture, Code Quality, Independent Test Execution, Security Coordination, Documentation).
   - Test Execution: Independently discover and run test commands; directly inspect raw stdout/stderr and exit codes.
   - Output: Audit assessment in `docs_agent/testing/QA_ASSESSMENT.md` or session logs.
3. **Pass 3: Security Review Pass (Agent C - Role Switch)**:
   - Mindset Shift: Adopt an adversarial attacker persona. Hunt for injection, BOLA, XSS, secrets, and auth bypass.
   - Action: Probe trust boundaries, review threat surfaces, and execute authorized non-destructive checks per [`independent-security-review-agent`](../../independent-security-review-agent/SKILL.md).
   - Output: `docs_agent/security/SECURITY_ASSESSMENT.md`.

### 8.2 Mandatory Honest Attribution Invariant
In single-agent sequential review mode, the agent must explicitly state in all assessment reports, logs, and user summaries:
> *"Verification was conducted via sequential self-review role-switch, not independent subagent execution."*  
**Never pretend that separate passes in a single agent are independent subagents.**

---

### Step-by-Step Workflow
1. **Step 1: Complete Pass 1 (Development)**
   - Implement code following TDD. Ensure developer tests pass locally. Prepare handoff briefing.
2. **Step 2: Explicit Context Wipe & Role Switch to Independent Verification Subagent**
   - Declare: "Switching role to Independent Verification Subagent (Agent B)".
   - Re-read original user prompt and execute 7-dimensional audit against git diff.
   - Run tests directly in terminal and verify exit code 0.
3. **Step 3: Explicit Context Wipe & Role Switch to Security**
   - Declare: "Switching role to Independent Security Agent (Agent C)".
   - Load security checklist; conduct adversarial audit and boundary verification for security-sensitive scopes.
4. **Step 4: Check Release Gates & Render Tri-State Decision**
   - Confirm Functional, Regression, Security, and Documentation gates.
   - Render `VERIFIED`, `NEEDS REMEDIATION`, or `BLOCKED / NOT VERIFIED`.
5. **Step 5: Final Integrated Report with Honest Attribution**
   - Present final deliverables to user citing executed commands, empirical evidence, and sequential self-review attribution.

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
| Pretending Single-Agent is Multi-Agent | False assurance of multi-agent redundancy | Explicitly declare sequential self-review role-switch |

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
- Record reusable multi-agent lessons in `MEMORY.md`.
- Record agent orchestration trade-offs in `DECISIONS.md`.
- Log session handoff in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
