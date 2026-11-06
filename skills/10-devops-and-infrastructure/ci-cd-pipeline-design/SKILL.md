---
name: ci-cd-pipeline-design
description: Architect, optimize, and maintain automated Continuous Integration and Continuous Deployment pipelines (GitHub Actions, GitLab CI).
version: 2.0.0
category: devops-and-infrastructure
tags: [ci-cd, github-actions, gitlab-ci, automation, pipelines, testing-gates]
---

# Skill: CI/CD Pipeline Design & Automation

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 10-devops-and-infrastructure  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `ci-cd-pipeline-design`
- **Category**: 10-devops-and-infrastructure
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Architect, optimize, and maintain automated Continuous Integration and Continuous Deployment pipelines (GitHub Actions, GitLab CI).
- **When to Use**: Setting up build workflows, automating test matrix execution, configuring artifact caching, or automating deployment gates.
- **Essential Invariants**:
  1. CI pipelines must be deterministic: build from pinned dependencies with hermetic environments.
  2. Main branch commits must pass automated test, lint, and security scan gates before deployment.
  3. Production deployments must include automated smoke verification and rollback capabilities.
- **Minimal Workflow**:
  1. Define declarative workflow YAML specifying triggers, concurrency groups, and environment matrix.
  2. Configure dependency caching to optimize execution duration without compromising freshness.
  3. Sequence jobs logically: Lint/Format -> Unit/Integration Tests -> Build/Package -> Deploy/Verify.
  4. Validate workflow locally via linting (actionlint) or test runner before committing.
- **Expected Deliverables**: Declarative CI/CD pipeline definition with automated testing gates and caching configuration.
- **Critical Restrictions**: Never store raw plaintext secrets in workflow definitions; do not disable failing test gates.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Architect, optimize, and maintain automated Continuous Integration and Continuous Deployment pipelines (GitHub Actions, GitLab CI).

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
