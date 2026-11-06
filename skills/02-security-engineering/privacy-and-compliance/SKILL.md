---
name: privacy-and-compliance
description: Enforce data minimization, PII/PHI protection, consent boundaries, retention limits, and regulatory compliance (GDPR, CCPA, HIPAA).
version: 2.0.0
category: security-engineering
tags: [privacy, compliance, gdpr, hipaa, ccpa, pii, data-minimization]
---

# Skill: Privacy Engineering & Regulatory Compliance

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 02-security-engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `privacy-and-compliance`
- **Category**: 02-security-engineering
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Enforce data minimization, PII/PHI protection, consent boundaries, retention limits, and regulatory compliance (GDPR, CCPA, HIPAA).
- **When to Use**: Handling user personal data, architecting storage for sensitive records, implementing data export/deletion, or regulatory audits.
- **Essential Invariants**:
  1. Practice strict data minimization: collect and retain only data strictly necessary for application functionality.
  2. PII (Personally Identifiable Information) and PHI must be encrypted in transit and at rest.
  3. Provide automated capabilities for user data export, correction, and permanent deletion (Right to Be Forgotten).
- **Minimal Workflow**:
  1. Inventory data models to map all personal data fields and assess regulatory sensitivity.
  2. Implement column-level encryption or pseudonymization for sensitive identifiers.
  3. Enforce retention policies with automated data pruning/anonymization mechanisms.
  4. Verify audit logging tracks data access without logging raw sensitive payload contents.
- **Expected Deliverables**: Data privacy impact evaluation, encryption configuration, and deletion/export endpoint verification.
- **Critical Restrictions**: Never store unencrypted PII in public tables or diagnostic logs; do not bypass user consent flags.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Enforce data minimization, PII/PHI protection, consent boundaries, retention limits, and regulatory compliance (GDPR, CCPA, HIPAA).

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
