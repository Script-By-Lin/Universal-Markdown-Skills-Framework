---
name: security-remediation-and-retesting
description: "Surgical remediation of confirmed vulnerabilities, patch verification, regression security sweeps, and independent retest reporting."
version: 1.7.0
category: security
tags: ['security', 'remediation', 'retesting', 'patching', 'regression-testing', 'verification']
---

# Skill: Security Remediation & Retesting

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 02 — Security Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `security-remediation-and-retesting`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Develop minimal, effective security patches and execute rigorous retesting to prove vulnerability elimination.
- **When to Use**: Remediating confirmed vulnerabilities, patching CVEs, or conducting post-exploit verification.
- **Essential Invariants**:
  1. Every security patch must include a failing regression test reproducing the exploit before fix application.
  2. Remediation must address root cause, not merely filter the specific proof-of-concept payload.
  3. Re-run full regression suites to guarantee zero functional regressions.
- **Minimal Workflow**:
  1. Author automated exploit reproduction test confirming failure (Red).
  2. Apply minimal surgical patch resolving root cause (Green).
  3. Execute adversarial variant testing to ensure no bypasses exist.
  4. Document verified fix in docs_agent/security/ and close tracking ticket.
- **Expected Deliverables**: Verified security patch accompanied by permanent regression test and retest log.
- **Critical Restrictions**: Never declare a vulnerability resolved without providing passing retest logs.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides disciplined procedures for writing targeted security fixes that eliminate the root cause of vulnerabilities without breaking application functionality, followed by independent verification.

---

### Scope
- **In-Scope**:
  - Root cause remediation of security vulnerabilities\n  - Authoring permanent regression tests for resolved security bugs\n  - Independent verification retesting of remediated endpoints\n  - Authoring formal retest reports (`docs_agent/security/RETEST_REPORT.md`)
- **Out-of-Scope**:
  - Initial threat modeling and surface discovery

---

### When to Use
- Fixing vulnerabilities reported in `docs_agent/security/VULNERABILITY_REGISTER.md`\n- Validating that a security patch successfully closes an exploit vector\n- Conducting pre-release security gate sign-offs

---

### When Not to Use
- For regular non-security feature development

---

### Prerequisites
- Target application components and architecture inspected.
- Context verified against `CONTEXT.md`.
- Security testing boundaries established in compliance with `RULES.md`.

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in `RULES.md` (Precedence Level 2).
- Security posture in `CONTEXT.md`.
- Active vulnerability records in [`docs_agent/security/VULNERABILITY_REGISTER.md`](../../../templates/VULNERABILITY_REGISTER.md) (if present).

---

### Core Instructions
### 8.1 The Remediation Protocol
1. **Fix Root Cause, Not Symptoms**: Do not simply blacklist known payload strings. Fix the architectural flaw (e.g. switch to parameterized queries, use strict schema validation, enforce server-side authorization).
2. **Minimal Surgical Edits**: Keep security patches focused and atomic. Avoid combining a critical security fix with wide refactorings.
3. **Automate the Exploit Test**: Turn the original vulnerability proof-of-concept into an automated test that asserts rejection (e.g. asserts HTTP 403 or sanitized output).
4. **Independent Retesting Mandatory**: The developer who wrote the fix cannot approve the retest. The Independent Security Agent must re-execute the test.

---

### Step-by-Step Workflow
1. **Step 1: Review Vulnerability Register & PoC**
   - Inspect finding description, affected code, and reproduction steps in `VULNERABILITY_REGISTER.md`.
2. **Step 2: Implement Surgical Patch**
   - Apply clean architectural remediation conforming to `RULES.md`.
3. **Step 3: Author Automated Security Regression Test**
   - Add automated test ensuring the exploit payload is permanently rejected.
4. **Step 4: Execute Independent Retest**
   - Independent Security Agent re-executes original PoC probe and confirms vulnerability is neutralized.
5. **Step 5: Publish Retest Report**
   - Author `docs_agent/security/RETEST_REPORT.md` and mark vulnerability `Closed`.

---

### Quality Standards
- **Standard 1**: 100% adherence to non-destructive testing boundaries defined in `RULES.md`.
- **Standard 2**: All findings verified with reproducible evidence; zero speculative claims.
- **Standard 3**: Absolute prohibition on logging or exfiltrating sensitive credentials, keys, or customer data.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Authorization Boundary | Pre-execution scope verification | Explicit user authorization confirmed; target in scope |
| Exploit Verification | Controlled PoC test | Weakness verified without data destruction or DoS |
| Remediation Invariance | Automated regression test | Exploit payload rejected; legitimate traffic unimpacted |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Testing Production Without Authorization | Violates legal and safety boundaries; risks data loss | Test strictly against local dev or authorized staging |
| Blacklist Sanitization | Easily bypassed with alternative encodings or syntax | Use parameterized queries, safe parsers, and strict allowlists |
| Closing Findings Without Independent Retest | High rate of incomplete or regressed patches | Require independent verification retest before closure |

---

### Restrictions
- Do NOT perform destructive testing or denial-of-service (DoS) attacks.
- Do NOT exfiltrate or record actual customer data, passwords, or secrets.
- Do NOT bypass security release gates when unresolved Critical or High vulnerabilities exist.

---

### Expected Deliverables
- Security assessment reports or threat models under `docs_agent/security/`.
- Updated vulnerability records in `docs_agent/security/VULNERABILITY_REGISTER.md`.
- Automated security regression tests.

---

### Documentation Requirements
- Record reusable security lessons and attack vectors in `MEMORY.md`.
- Record architectural security decisions in `DECISIONS.md`.
- Update task tracking in `TASKS.md` and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
