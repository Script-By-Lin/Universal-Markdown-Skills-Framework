---
name: infrastructure-as-code
description: Define, provision, version, and manage cloud infrastructure using declarative, reproducible code (Terraform, OpenTofu, Pulumi).
version: 2.0.0
category: devops-and-infrastructure
tags: [iac, terraform, opentofu, pulumi, cloud, infrastructure, provisioning]
---

# Skill: Infrastructure as Code (IaC) & Cloud Provisioning

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 10-devops-and-infrastructure  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `infrastructure-as-code`
- **Category**: 10-devops-and-infrastructure
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Define, provision, version, and manage cloud infrastructure using declarative, reproducible code (Terraform, OpenTofu, Pulumi, CloudFormation).
- **When to Use**: Provisioning cloud resources, managing DNS/networking, configuring IAM policies, or auditing infrastructure drift.
- **Essential Invariants**:
  1. All infrastructure must be defined declaratively in version-controlled configuration files.
  2. Remote state must be stored in encrypted, versioned backends with distributed state locking enabled.
  3. Infrastructure changes must generate and verify an execution plan (plan) prior to apply.
- **Minimal Workflow**:
  1. Author modular, parameterized IaC configurations adhering to least privilege principles.
  2. Validate syntax and format configurations using native tooling (terraform fmt, tflint).
  3. Generate speculative execution plan to verify intended resource additions, modifications, and deletions.
  4. Apply verified configuration and record state outputs.
- **Expected Deliverables**: Modular declarative infrastructure templates, verified execution plans, and remote state locks.
- **Critical Restrictions**: Never hardcode secrets in .tf/.yaml files; never perform unmanaged manual cloud console modifications.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Define, provision, version, and manage cloud infrastructure using declarative, reproducible code (Terraform, OpenTofu, Pulumi).

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
