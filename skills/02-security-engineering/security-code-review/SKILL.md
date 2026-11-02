---
name: security-code-review
description: "Static manual and automated code inspection for security anti-patterns, dangerous sinks, unsanitized inputs, and cryptographic misconfigurations."
version: 1.0.0
category: security
tags: ['security', 'code-review', 'sast', 'secure-coding', 'anti-patterns', 'audit']
---

# Skill: Security Code Review

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `security-code-review`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Instructs engineers and agents in conducting deep, security-focused source code reviews to catch vulnerabilities early in the pull request and development lifecycle.

---

## 3. Scope
- **In-Scope**:
  - Detecting dangerous API functions and sinks (e.g. `eval`, `child_process.exec`, raw query strings)\n  - Auditing input validation, type casting, and sanitization routines\n  - Verifying cryptographic implementations and secret management hygiene\n  - Checking error handling for information disclosure
- **Out-of-Scope**:
  - General code readability and styling review (delegate to `skills/12-code-quality-and-maintenance/code-review/SKILL.md`)

---

## 4. When to Use
- Reviewing pull requests touching authentication, authorization, or data persistence\n- Auditing third-party libraries or internal shared utilities\n- Conducting pre-merge security sign-offs

---

## 5. When Not to Use
- For dynamic runtime penetration testing (use `skills/02-security-engineering/penetration-testing/SKILL.md`)

---

## 6. Prerequisites
- Target application components and architecture inspected.
- Context verified against [`CONTEXT.md`](../../../CONTEXT.md).
- Security testing boundaries established in compliance with [`RULES.md`](../../../RULES.md).

---

## 7. Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (Precedence Level 2).
- Security posture in [`CONTEXT.md`](../../../CONTEXT.md).
- Active vulnerability records in [`docs_agent/security/VULNERABILITY_REGISTER.md`](../../../templates/VULNERABILITY_REGISTER.md) (if present).

---

## 8. Core Instructions
### 8.1 Critical Source Code Sinks to Inspect
Audit code paths reaching any of the following sensitive sinks:
1. **Command Execution Sinks**: `exec`, `system`, `popen`, `child_process.exec`, `Runtime.getRuntime().exec`. Must use parameter arrays, never concatenated shell strings.
2. **Database Query Sinks**: Raw SQL query methods, string formatting inside ORM `raw()` calls. Must use parameterized placeholders (`$1`, `?`).
3. **File System Sinks**: `fs.readFile`, `open()`, path joins with user input. Must sanitize using base-path canonicalization (`path.resolve` + startsWith check).
4. **Serialization Sinks**: `pickle.loads`, `yaml.load` (without SafeLoader), `unserialize()`. Must use safe formats like JSON.
5. **Cryptographic Sinks**: `MD5`, `SHA1` for passwords, ECB mode in AES. Must use Argon2id/bcrypt for passwords and AES-GCM for encryption.

---

## 9. Step-by-Step Workflow
1. **Step 1: Diff & Scope Identification**
   - Inspect git diff to locate newly added or modified sensitive functions and endpoints.
2. **Step 2: Trace User Data Flows (Source-to-Sink)**
   - Identify entry points (controller parameters, headers, query params) and trace data to persistence/execution.
3. **Step 3: Security Rule Checklist Audit**
   - Verify input sanitization, authorization gates, and error boundaries.
4. **Step 4: Formulate Actionable Review Comments**
   - Provide explicit code remediation examples rather than vague warnings.
5. **Step 5: Sign-off or Block PR**
   - Block merge if Critical or High security vulnerabilities are identified.

---

## 10. Quality Standards
- **Standard 1**: 100% adherence to non-destructive testing boundaries defined in [`RULES.md`](../../../RULES.md).
- **Standard 2**: All findings verified with reproducible evidence; zero speculative claims.
- **Standard 3**: Absolute prohibition on logging or exfiltrating sensitive credentials, keys, or customer data.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Authorization Boundary | Pre-execution scope verification | Explicit user authorization confirmed; target in scope |
| Exploit Verification | Controlled PoC test | Weakness verified without data destruction or DoS |
| Remediation Invariance | Automated regression test | Exploit payload rejected; legitimate traffic unimpacted |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Testing Production Without Authorization | Violates legal and safety boundaries; risks data loss | Test strictly against local dev or authorized staging |
| Blacklist Sanitization | Easily bypassed with alternative encodings or syntax | Use parameterized queries, safe parsers, and strict allowlists |
| Closing Findings Without Independent Retest | High rate of incomplete or regressed patches | Require independent verification retest before closure |

---

## 13. Restrictions
- Do NOT perform destructive testing or denial-of-service (DoS) attacks.
- Do NOT exfiltrate or record actual customer data, passwords, or secrets.
- Do NOT bypass security release gates when unresolved Critical or High vulnerabilities exist.

---

## 14. Expected Deliverables
- Security assessment reports or threat models under `docs_agent/security/`.
- Updated vulnerability records in `docs_agent/security/VULNERABILITY_REGISTER.md`.
- Automated security regression tests.

---

## 15. Documentation Requirements
- Record reusable security lessons and attack vectors in [`MEMORY.md`](../../../MEMORY.md).
- Record architectural security decisions in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).
