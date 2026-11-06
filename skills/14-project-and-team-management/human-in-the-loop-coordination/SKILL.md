---
name: human-in-the-loop-coordination
description: Standardize structured agent-to-human communication, decision checkpoints, escalation triggers, and handoff briefings.
version: 2.0.0
category: project-and-team-management
tags: [human-in-the-loop, coordination, escalation, handoff, decisions, approvals]
---

# Skill: Human-in-the-Loop Coordination & Decision Gates

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 14-project-and-team-management  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `human-in-the-loop-coordination`
- **Category**: 14-project-and-team-management
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Standardize structured agent-to-human communication, decision checkpoints, escalation triggers, and handoff briefings.
- **When to Use**: Escalating blocked tasks, requesting architectural guidance, confirming irreversible/destructive actions, or delivering final handoffs.
- **Essential Invariants**:
  1. Agents must immediately halt autonomous execution and consult a human when encountering ambiguous specs, destructive operations, or credentials.
  2. Escalation messages must be structured: Context, Explicit Question, Options Considered with Trade-offs, Recommended Course.
  3. Never proceed with irreversible production changes without explicit human approval.
- **Minimal Workflow**:
  1. Identify escalation trigger (ambiguity, destructive risk, permission boundary, or iteration limit exhaustion).
  2. Compile concise escalation payload detailing context, discovered constraints, and concrete options.
  3. Await explicit human feedback or approval before executing downstream steps.
  4. Record human decision in project notes or DECISIONS.md before resuming execution.
- **Expected Deliverables**: Structured escalation message with clear decision options or final verified handoff summary.
- **Critical Restrictions**: Never guess user intent when data loss or security risk exists; do not proceed past approval gates autonomously.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Standardize structured agent-to-human communication, decision checkpoints, escalation triggers, and handoff briefings.

### Execution Procedures
1. **Preparation**: Review task scope, prerequisites, and verify project state. If governance files (TASKS.md, CONTEXT.md) are absent, create them from the bootstrap template or record the evidence inline.
2. **Implementation**: Execute the procedures according to the Level 1 Minimal Workflow while upholding all Essential Invariants.
3. **Verification**: Verify outputs empirically with exit codes, static linters, and regression checks.

### Edge Cases & Failure Recovery
- **Ambiguous Constraints**: Halt and trigger human-in-the-loop escalation rather than making unverified assumptions.
- **Execution Failures**: Record failure evidence, isolate root cause, and formulate targeted remediation within bounded iterations.

---

## Level 3 — Optional References & Supplementary Assets

### Level 3 Index
- None (all core procedures codified in Level 1 & Level 2).
