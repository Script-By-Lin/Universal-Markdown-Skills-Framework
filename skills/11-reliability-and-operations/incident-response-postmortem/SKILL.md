---
name: incident-response-postmortem
description: Manage production incident response, severity classification (SEV-1 to SEV-4), containment, root-cause analysis, and postmortems.
version: 2.0.0
category: reliability-and-operations
tags: [incident-response, postmortem, blameless, root-cause, 5-whys, reliability]
---

# Skill: Incident Response & Blameless Postmortems

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 11-reliability-and-operations  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `incident-response-postmortem`
- **Category**: 11-reliability-and-operations
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Manage production incident response, severity classification (SEV-1 to SEV-4), containment, root-cause analysis (5 Whys), and blameless postmortems.
- **When to Use**: Responding to production outages, performance degradations, data corruption, or facilitating post-incident reviews.
- **Essential Invariants**:
  1. Incident response priorities are strictly: 1) Triage & Containment, 2) Service Restoration, 3) Root Cause Investigation.
  2. Postmortems must be blameless: focus on systemic, architectural, and procedural failures rather than individual human error.
  3. Every confirmed incident must produce tracked corrective action items with assigned owners and due dates.
- **Minimal Workflow**:
  1. Triage incident severity and establish unified communication channel.
  2. Execute rapid containment (traffic redirection, canary rollback, feature-flag killswitch).
  3. Reconstruct incident chronological timeline using telemetry, deployment records, and server logs.
  4. Conduct 5-Whys root cause analysis and author blameless postmortem document with actionable preventions.
- **Expected Deliverables**: Structured postmortem document containing timeline, root cause analysis, and tracked preventative action items.
- **Critical Restrictions**: Never assign individual blame in postmortems; do not close incidents without verified corrective action tracking.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Manage production incident response, severity classification (SEV-1 to SEV-4), containment, root-cause analysis, and postmortems.

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
