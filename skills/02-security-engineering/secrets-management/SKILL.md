---
name: secrets-management
description: Govern lifecycle, injection, isolation, rotation, and leakage prevention of credentials, API keys, tokens, and certificates.
version: 2.0.0
category: security-engineering
tags: [secrets, credentials, security, env-vars, vault, encryption]
---

# Skill: Secrets Management & Credential Protection

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 02-security-engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `secrets-management`
- **Category**: 02-security-engineering
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Govern the lifecycle, injection, isolation, rotation, and leakage prevention of credentials, API keys, tokens, and certificates.
- **When to Use**: Configuring application secrets, reading environment variables, preventing credential leaks in logs/git, or auditing secret vaults.
- **Essential Invariants**:
  1. Plaintext secrets, tokens, private keys, and passwords must NEVER be committed to version control.
  2. All configuration secrets must be loaded dynamically via environment variables or encrypted secret stores.
  3. Secret values must be sanitized and redacted from all application logs, error messages, and agent command outputs.
- **Minimal Workflow**:
  1. Audit repository with static secret scanners to ensure zero credentials are committed.
  2. Define .env.example templates specifying variable names and formats with safe dummy values.
  3. Configure environment variable injection or vault access with principle of least privilege.
  4. Verify error handlers and logging pipelines redact sensitive token patterns.
- **Expected Deliverables**: Secret-free codebase, sanitized .env.example, and verified secret redaction configuration.
- **Critical Restrictions**: Never echo or print decrypted secrets into tool outputs or prompt context; never hardcode credentials.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Govern lifecycle, injection, isolation, rotation, and leakage prevention of credentials, API keys, tokens, and certificates.

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
