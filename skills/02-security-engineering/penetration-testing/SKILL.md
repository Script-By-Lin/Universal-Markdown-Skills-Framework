---
name: penetration-testing
description: "Authorized, non-destructive penetration testing methodology, explicit scope verification, controlled proof-of-concept exploitation, and risk reporting."
version: 1.0.0
category: security
tags: ['security', 'penetration-testing', 'ethical-hacking', 'poc', 'authorization-boundary', 'owasp']
---

# Skill: Penetration Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `penetration-testing`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Governs ethical, authorized penetration testing against application targets to discover reproducible vulnerabilities through controlled adversarial simulation without risking data loss or service disruption.

---

## 3. Scope
- **In-Scope**:
  - Validating explicit user authorization boundaries before active probing\n  - Executing non-destructive security test attacks against staging/local environments\n  - Developing minimal proof-of-concept (PoC) demonstrations\n  - Distinguishing confirmed vulnerabilities from false positives
- **Out-of-Scope**:
  - Destructive testing, denial-of-service (DoS), or mass data exfiltration (strictly prohibited by RULES.md)\n  - Testing systems outside explicit written authorization scope

---

## 4. When to Use
- Conducting pre-release security validation on staging environments\n- Auditing critical authentication, authorization, or payment workflow surfaces\n- Verifying exploitability of vulnerabilities flagged by static scanners

---

## 5. When Not to Use
- When user ownership or testing authorization is ambiguous (restrict to static code review)\n- On live production environments with unbacked customer data

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
### 8.1 Mandatory Authorization Protocol
Before executing any active security probe:
1. **Scope Verification**: Confirm specific target URLs, hostnames, IP ranges, and API versions.
2. **Prohibited Targets**: Identify explicitly excluded paths (e.g. production DBs, third-party webhook receivers).
3. **Backup Status**: Confirm that database snapshots and environment restores are available.
4. **Intensity Level**: Default to low-intensity single-probe requests to avoid accidental service degradation.

### 8.2 Non-Destructive Proof-of-Concept Standard
When demonstrating exploitability:
- **SQL Injection**: Use non-destructive boolean probes (e.g. `1=1` vs `1=2`) or version extraction (`SELECT @@version`). Never execute `DROP`, `DELETE`, or `UPDATE`.
- **Cross-Site Scripting (XSS)**: Inject inert proof tokens like `console.log("poc-xss-token")` or benign DOM markers. Never inject credential stealers.
- **Path Traversal**: Read standard non-sensitive target indicators (e.g. safe dummy test files). Never access `/etc/shadow` or private host keys.
- **IDOR / Privilege Escalation**: Verify that user A cannot access user B's test record. Demonstrate access using two test accounts created explicitly for the test.

---

## 9. Step-by-Step Workflow
1. **Step 1: Authorization & Boundary Confirmation**
   - Confirm target environment is local development or authorized test staging.
   - Record authorization scope in `docs_agent/security/SECURITY_TEST_PLAN.md`.
2. **Step 2: Passive Reconnaissance & Attack Surface Mapping**
   - Map all exposed endpoints, HTTP verbs, parameters, headers, and authentication mechanisms.
3. **Step 3: Threat-Driven Vulnerability Probing**
   - Probe authentication, authorization, input validation, and business logic using non-destructive payloads.
4. **Step 4: PoC Development & Evidence Collection**
   - For every reproducible weakness, capture raw request/response pairs demonstrating the issue.
5. **Step 5: Vulnerability Registration & Reporting**
   - Record findings in `docs_agent/security/VULNERABILITY_REGISTER.md` with severity, impact, and remediation steps.

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
