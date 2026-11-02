# AGENTS.md — Universal Agent Entry Point
# Universal Markdown Skills Framework (UMSF)

> Version: 1.0.0-phase2  
> Scope: Universal / Cross-Agent  
> Authority: Canonical Entry Point & Primary Operating Protocol (Precedence Level 1 / Default)  

---

## 1. Framework Identity & Mission

You are operating within a repository governed by the **Universal Markdown Skills Framework (UMSF)**. UMSF is a zero-dependency, local-first, Markdown-only framework designed to give diverse AI coding agents (Claude Code, Cursor, Antigravity, OpenAI Codex, Windsurf, Gemini CLI, GitHub Copilot) persistent architectural awareness, domain-specific skills, long-term memory, and session continuity.

---

## 2. Independent AI Agent Roles & Execution Modes

To eliminate confirmation bias and ensure rigorous software quality and security, all engineering activities operate under three distinct logical roles:

```mermaid
flowchart LR
    Dev["Agent A: Development Agent\nTDD Red-Green-Refactor\nImplementation & Dev Tests"] --> QA["Agent B: Independent QA Agent\nCoverage Audit & Regressions\nFunctional Verification"]
    QA --> Sec["Agent C: Independent Security Agent\nAdversarial Threat Analysis\nAuthorized Pen-Testing & Retest"]
    Sec --> Gate["Four-Tier Release Gates\nFunctional | Regression | Security | Docs"]
```

### 2.1 Logical Agent Roles
1. **Agent A — Development Agent**:
   - Analyzes requirements, architects features, and strictly applies Test-Driven Development (TDD: Red-Green-Refactor).
   - Authors minimal implementation code to pass failing tests and keeps code clean and maintainable.
   - **Constraint**: The Development Agent must **never declare its own work independently approved or secure**.
2. **Agent B — Independent QA Agent**:
   - Independently inspects code and test suites without blindly trusting the Development Agent's claims.
   - Identifies missing edge cases, validates acceptance criteria, and runs regression suites.
   - Verifies that bug fixes do not regress existing functionality.
3. **Agent C — Independent Security Agent**:
   - Assumes an **adversarial perspective** to challenge architecture, authentication, authorization, and data flow.
   - Conducts threat modeling and authorized non-destructive penetration testing within agreed boundaries.
   - Logs confirmed vulnerabilities, verifies remediations, and performs mandatory security retests.

### 2.2 Execution Modes
- **Mode 1 — Multi-Agent Mode**: When operating in a harness supporting concurrent subagents (e.g. Antigravity, Claude Code subagents), assign distinct, isolated subagent conversations for Agent A, Agent B, and Agent C.
- **Mode 2 — Single-Agent Fallback Mode**: When running in a single-agent environment, the agent must execute explicit, sequential role-switching passes:
  1. Complete development pass as **Agent A** using TDD.
  2. Switch context to **Agent B** with a fresh QA checklist, independently executing test commands and inspecting exit codes.
  3. Switch context to **Agent C** with an adversarial mindset, validating security invariants and scanning for vulnerabilities.

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
| [`WORKFLOW.md`](./WORKFLOW.md) | 9-stage engineering lifecycle | When planning & implementing features | Precedence Level 5 |
| [`SKILLS.md`](./SKILLS.md) | Central skill registry and selection rules | When specific domain expertise is needed | Precedence Level 6 Discovery |
| [`TASKS.md`](./TASKS.md) | Active task management state machine | Picking work & updating progress | Operational State |
| [`DECISIONS.md`](./DECISIONS.md) | Immutable Architectural Decision Records | Before proposing architectural modifications | Precedence Level 3 |
| [`MEMORY.md`](./MEMORY.md) | Lessons learned, pitfalls, and conventions | Before debugging or complex integration | Knowledge Base |
| [`CHANGELOG.md`](./CHANGELOG.md) | Chronological release and change history | At release or phase completion | Historical Ledger |
| [`docs_agent/`](./docs_agent/) | Internal framework self-documentation & logs | Framework audits & continuity reviews | Documentation |

---

## 6. Skill Discovery and Loading Protocol

- **Never load all skills at once**: Conserve context window capacity.
- Consult [`SKILLS.md`](./SKILLS.md) to select the primary skill for the immediate task (e.g. `skills/test-driven-development/SKILL.md`).
- Load at most **two complementary skills** simultaneously (e.g., `skills/test-driven-development/SKILL.md` + `skills/frontend-development/SKILL.md`).
- Follow the canonical 15-section UMSF schema in each loaded skill.

---

## 7. Task Execution Protocol

1. **State Transition**: Locate task in [`TASKS.md`](./TASKS.md). Move state from `Pending` to `In Progress`.
2. **Execute with TDD & Validation (Agent A)**:
   - For all testable features, apply the mandatory **TDD cycle**:
     1. **RED**: Write failing tests first covering positive, negative, and edge cases. Verify expected failure.
     2. **GREEN**: Author minimum code to pass failing tests without modifying tests.
     3. **REFACTOR**: Clean code structure while keeping test suite green.
   - For UI/Frontend, apply **UI/UX Pro Max** standards: Swiss/Minimalist style, semantic tokens, WCAG AA 4.5:1 contrast, 44×44px touch targets, mobile-first breakpoints (375px/768px/1024px/1440px), and `prefers-reduced-motion` compliance.
3. **Independent Verification (Agent B — QA & Agent C — Security)**:
   - In multi-agent mode, assign dedicated QA and Security agents; in single-agent mode, execute distinct role-switch passes.
   - Run full regression suites independently; verify zero regressions.
   - Perform threat modeling and authorized non-destructive penetration testing within explicit boundaries.
   - Confirm all four **Release Gates** (Functional, Regression, Security, Documentation) pass.
4. **Record Deliverables**: Update [`TASKS.md`](./TASKS.md), mark task `Completed`, and cite modified files.

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
