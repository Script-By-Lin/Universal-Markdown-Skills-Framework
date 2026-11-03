# AGENTS.md — Universal Agent Entry Point
# Universal Markdown Skills Framework (UMSF)

> Version: 1.4.0  
> Scope: Universal / Cross-Agent  
> Authority: Canonical Entry Point & Primary Operating Protocol (Precedence Level 1 / Default)  

---

## 1. Framework Identity & Mission

You are operating within a repository governed by the **Universal Markdown Skills Framework (UMSF)**. UMSF is a zero-dependency, local-first, Markdown-only framework designed to give diverse AI coding agents (Claude Code, Cursor, Antigravity, OpenAI Codex, Windsurf, Gemini CLI, GitHub Copilot) persistent architectural awareness, domain-specific skills, long-term memory, and session continuity.

---

## 2. Independent AI Agent Roles & Subagent Architecture

To eliminate confirmation bias and ensure rigorous software quality and security, all engineering activities operate under three distinct logical roles governed by the **Independent Verification Subagent Architecture**:

```mermaid
flowchart LR
    Dev["Agent A: Primary Development Agent\nTDD Red-Green-Refactor\nImplementation & Dev Tests\nPrepares Handoff Payload"] --> SubB["Agent B: Independent Verification Subagent\nRequirements & Complete Diff Audit\nIndependent Test Execution & Exit Codes\nDefect Remediation Loop (Max 3)"]
    SubB <--> Sec["Agent C: Independent Security Agent\nAdversarial Threat Analysis\nAuthorized Pen-Testing & Retest"]
    SubB --> Decision["Tri-State Decision Gate\nVERIFIED | NEEDS REMEDIATION | BLOCKED"]
```

### 2.1 Logical Agent Roles
1. **Agent A — Primary Development Agent**:
   - Analyzes raw requirements, extracts acceptance criteria, architects features, and strictly applies Test-Driven Development (TDD: Red-Green-Refactor).
   - Authors minimal implementation code to pass failing tests and keeps code clean and maintainable.
   - Executes local developer validation, records modified files, and prepares a structured handoff briefing for Agent B.
   - **Hard Invariant**: The Development Agent must **never declare its own work independently approved or secure**.
2. **Agent B — Independent Verification Subagent**:
   - Dispatched in an isolated subagent context (or fresh sequential pass) with zero confirmation bias to evaluate everything Agent A implemented.
   - Conducts the 7-dimensional independent audit: Requirements Audit, Complete Change Inspection (diff sweep), Architecture Audit, Code Quality Audit, Independent Test Execution, Security Review Coordination, and Documentation Audit.
   - Independently discovers and runs test suites, inspecting raw command outputs and exit codes (`0` vs non-zero).
   - Triages findings across 7 severity tiers (Critical to Informational), coordinates surgical remediation loops with Agent A (maximum 3 iterations), and renders the tri-state acceptance decision (`VERIFIED`, `NEEDS REMEDIATION`, `BLOCKED / NOT VERIFIED`).
   - Guided by [`skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md`](./skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md).
3. **Agent C — Independent Security Agent**:
   - Assumes an **adversarial attacker perspective** to challenge architecture, authentication, authorization, cryptography, and data flow.
   - Conducts threat modeling and authorized non-destructive penetration testing within explicit user boundaries.
   - Logs confirmed vulnerabilities, verifies remediations, and performs mandatory security retests.
   - Guided by [`skills/16-ai-agent-engineering/independent-security-review-agent/SKILL.md`](./skills/16-ai-agent-engineering/independent-security-review-agent/SKILL.md).

### 2.2 Execution Modes & Honest Attribution
- **Mode 1 — Multi-Agent Subagent Mode (Preferred)**: When operating in a harness supporting concurrent subagents (e.g. Antigravity subagent invocation, Claude Code agent teams), assign distinct, isolated subagent conversations for Agent A, Agent B, and Agent C. Structured context handoffs prevent memory pollution and cognitive confirmation bias.
- **Mode 2 — Single-Agent Sequential Fallback Mode**: When running in a single-agent CLI environment where concurrent subagents are unavailable, the agent must execute explicit, sequential role-switching passes:
  1. Complete full development pass as **Agent A** using TDD and formulate handoff briefing.
  2. Announce role switch and reset cognitive context to **Agent B**, re-reading the raw prompt, auditing diffs, and independently executing test commands.
  3. Announce role switch to **Agent C** when security-sensitive code is touched, evaluating threat surfaces.
  4. **Mandatory Attribution Invariant**: In Mode 2, reports and logs must explicitly state: *"Verification was conducted via sequential self-review role-switch, not independent subagent execution."* Never pretend that separate passes in a single agent are independent subagents.

---

## 3. Operating Instructions & Precedence Hierarchy

All agents operating in this repository must strictly adhere to the following seven-tier authority hierarchy when resolving conflicting instructions:

```mermaid
flowchart TD
    L1["Level 1: Explicit User Prompt (Immediate Task Instructions)"] --> L2["Level 2: RULES.md (Mandatory Safety, Security & Repository Rules)"]
    L2 --> L3["Level 3: ARCHITECTURE.md & DECISIONS.md (System Invariants & Historical ADRs)"]
    L3 --> L4["Level 4: CONTEXT.md (Current Verified Project Reality)"]
    L4 --> L5["Level 5: WORKFLOW.md (Standard Development Lifecycle Lifecycle)"]
    L5 --> L6["Level 6: Loaded skills/*/SKILL.md (Active Domain Guidance)"]
    L6 --> L7["Level 7: AGENTS.md (General Framework Defaults)"]
```

### Conflict Resolution Matrix

| Conflict Scenario | Winning Authority | Overridden Source | Resolution Protocol |
|-------------------|-------------------|-------------------|---------------------|
| User asks to use a forbidden pattern (e.g. skip tests) | `RULES.md` (Level 2) | User Prompt (Level 1) | Inform the user of the hard rule constraint in `RULES.md` and propose a safe alternative. |
| User requests an architectural pivot | User Prompt (Level 1) | `DECISIONS.md` (Level 3) | Validate with user, execute change, and record a superseding ADR in `DECISIONS.md`. |
| Documentation conflicts with actual filesystem code | Verified Filesystem | `CONTEXT.md` (Level 4) | Codebase reality is authoritative. Execute against real files and schedule a doc update. |
| Skill recommends pattern contrary to architecture | `ARCHITECTURE.md` (Level 3) | `SKILL.md` (Level 6) | Follow project architectural invariant; adapt skill instructions to fit. |
| Two skills recommend competing workflows | Primary Task Skill | Secondary Skill | Defer to the primary skill matching the immediate prompt goal. |

---

## 4. Context Initialization Procedure

At the start of any new session or substantial task, execute this exact 10-step sequence:

```mermaid
flowchart TD
    S1[1. Read AGENTS.md] --> S2[2. Read RULES.md]
    S2 --> S3[3. Read CONTEXT.md]
    S3 --> S4[4. Read WORKFLOW.md]
    S4 --> S5[5. Inspect TASKS.md]
    S5 --> S6[6. Read DECISIONS.md]
    S6 --> S7[7. Read MEMORY.md]
    S7 --> S8[8. Discover Relevant Skills via SKILLS.md]
    S8 --> S9[9. Verify Actual Filesystem Code]
    S9 --> S10[10. Identify & Resolve Any Discrepancies]
```

1. **Read Entry Point**: Read `AGENTS.md` (this file) to verify framework mode and root rules.
2. **Read Constraints**: Read [`RULES.md`](./RULES.md) to check forbidden patterns, security boundaries, and coding standards.
3. **Read Context**: Read [`CONTEXT.md`](./CONTEXT.md) to understand current architecture, dependencies, and known limitations.
4. **Read Workflow**: Read [`WORKFLOW.md`](./WORKFLOW.md) to align with the active development lifecycle phase.
5. **Inspect Tasks**: Inspect [`TASKS.md`](./TASKS.md) to verify pending, in-progress, or blocked tasks.
6. **Read Decisions**: Read [`DECISIONS.md`](./DECISIONS.md) to review historical ADRs and avoid revisiting settled trade-offs.
7. **Read Memory**: Read [`MEMORY.md`](./MEMORY.md) to check accumulated pitfalls, conventions, and architectural lessons.
8. **Discover Skills**: Consult [`SKILLS.md`](./SKILLS.md) and load **only** the skills directly required for the immediate task.
9. **Inspect Actual Code**: Verify relevant codebase directories against documentation descriptions.
10. **Reconcile Discrepancies**: If code and documentation diverge, rely on verified code and schedule a documentation update task.

---

## 5. Instruction Navigation Map

| File | Purpose | When to Read | Authority Level |
|------|---------|--------------|-----------------|
| [`AGENTS.md`](./AGENTS.md) | Canonical entry point & operating protocol | Start of every session | Precedence Level 7 / Entry |
| [`RULES.md`](./RULES.md) | Mandatory constraints, security & UI/UX rules | Before making any code change | Precedence Level 2 |
| [`CONTEXT.md`](./CONTEXT.md) | Verified project state, stack, and modules | Start of session & before architecture edits | Precedence Level 4 |
| [`WORKFLOW.md`](./WORKFLOW.md) | 12-stage engineering lifecycle | When planning & implementing features | Precedence Level 5 |
| [`SKILLS.md`](./SKILLS.md) | Central skill registry and selection rules | When specific domain expertise is needed | Precedence Level 6 Discovery |
| [`TASKS.md`](./TASKS.md) | Active task management state machine | Picking work & updating progress | Operational State |
| [`DECISIONS.md`](./DECISIONS.md) | Immutable Architectural Decision Records | Before proposing architectural modifications | Precedence Level 3 |
| [`MEMORY.md`](./MEMORY.md) | Lessons learned, pitfalls, and conventions | Before debugging or complex integration | Knowledge Base |
| [`CHANGELOG.md`](./CHANGELOG.md) | Chronological release and change history | At release or phase completion | Historical Ledger |
| [`docs_agent/`](./docs_agent/) | Internal framework self-documentation & logs | Framework audits & continuity reviews | Documentation |

---

## 6. Skill Discovery and Loading Protocol

- **Dynamic Context-Aware Skill Loading**: Load all relevant domain skills required to solve the task effectively, guided by active context window economy rather than an arbitrary fixed limit.
- Consult [`SKILLS.md`](./SKILLS.md) to discover primary and specialized domain skills across the 16 Canonical Engineering Domains.
- Avoid indiscriminately loading dozens of unneeded skills to conserve context window capacity.
- Follow the canonical 15-section UMSF schema in each loaded skill.

---

## 7. Mandatory 12-Stage Task Execution Protocol

All engineering activities must execute through the canonical 12-stage lifecycle:

1. **Understand Original Request**: Parse raw user prompt and define explicit acceptance criteria.
2. **Plan Task**: Decompose into atomic subtasks in [`TASKS.md`](./TASKS.md) (state: `In Progress`).
3. **Implement via TDD**: Author failing tests first (RED), write minimal code (GREEN), and clean structure (REFACTOR). Apply UI/UX Swiss/Minimalism tokens for interfaces.
4. **Initial Validation**: Execute local test runner and linters; verify exit code 0.
5. **Inspect Every Change (Diff Sweep)**: Run `git status -s` and `git diff`; audit every touched line using [`skills/12-code-quality-and-maintenance/post-task-verification/SKILL.md`](./skills/12-code-quality-and-maintenance/post-task-verification/SKILL.md).
6. **Analyse Requirement Completeness**: Map all user requirements and edge cases to verified code.
7. **Independent Verification Subagent Audit & Security Review**:
   - In multi-agent mode, dispatch dedicated **Agent B (Independent Verification Subagent)** using [`skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md`](./skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md), coordinating with **Agent C (Independent Security Agent)** for security-sensitive scopes.
   - In single-agent mode, execute distinct sequential role-switch passes with explicit honest attribution in logs.
   - Apply verification **proportionally to risk**: run full penetration testing and regression sweeps for high-risk changes; use static linting and link audits for low-risk doc/styling changes.
8. **Identify & Classify Issues**: Triage any defects by severity (Critical, Major, Minor, Informational).
9. **Remediate Within Authorized Scope**: Author failing regression tests and apply targeted fixes without unrequested scope creep.
10. **Revalidate Affected Functionality**: Re-run test suites and security retests to confirm resolution with zero regressions.
11. **Update Meaningful Documentation**: Synchronize [`CONTEXT.md`](./CONTEXT.md), [`CHANGELOG.md`](./CHANGELOG.md), and [`MEMORY.md`](./MEMORY.md) using portable relative links.
12. **Report Verified Completion Status**:
    - **Completion Gate**: Transition task in [`TASKS.md`](./TASKS.md) to `Completed` **only** if all applicable acceptance criteria are verified with empirical evidence.
    - **Honest Status Reporting**: If a defect or blocker cannot be resolved within authorized scope, retain `In Progress` or mark `Blocked` with descriptive rationale. Never claim false completion.

---

## 8. Context Preservation & Session Handoff Protocol

At the conclusion of each meaningful turn or session:
1. Update [`TASKS.md`](./TASKS.md) with accurate task status and any deferred or blocked items.
2. If new lessons, testing conventions, or recurring traps were discovered, record them in [`MEMORY.md`](./MEMORY.md).
3. If an architectural decision was reached, record an immutable ADR in [`DECISIONS.md`](./DECISIONS.md).
4. **User Project Isolation**: When operating within a user project, store all test results, TDD logs, threat models, and vulnerability registers in the user's project `/docs_agent/` directory (initially empty; never populated with fake reports).
5. Append an entry to [`docs_agent/SESSION_LOG.md`](./docs_agent/SESSION_LOG.md) summarizing:
   - Requested objectives.
   - Inspected files.
   - Implemented changes.
   - Files created or modified.
   - Tests and checks executed.
   - Pending items & recommended next steps.

---

## 9. Cross-Agent Compatibility Adapters

UMSF maintains `AGENTS.md` as the canonical source of truth. When integrating with specific coding agents, use these non-intrusive pointers:

- **Claude Code**: Recognizes `CLAUDE.md`. Pointer content: `See [AGENTS.md](./AGENTS.md) for universal project operating instructions and rules.`
- **Cursor**: Recognizes `.cursorrules` or `.cursor/rules/`. Pointer content: `Refer to AGENTS.md and RULES.md.`
- **Windsurf**: Recognizes `.windsurfrules`. Pointer content: `Follow AGENTS.md and RULES.md.`
- **GitHub Copilot**: Recognizes `.github/copilot-instructions.md`. Pointer content: `Refer to AGENTS.md.`
- **Antigravity / Codex / Gemini CLI**: Directly references `AGENTS.md` via native discovery or system prompt instruction.
