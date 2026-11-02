---
name: security-testing
description: "Strategic planning, automation, and execution of comprehensive software security test suites across SAST, DAST, and CI/CD pipelines."
version: 1.0.0
category: security
tags: ['security', 'security-testing', 'sast', 'dast', 'ci-cd', 'owasp', 'vulnerability']
---

# Skill: Security Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `security-testing`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Provides a systematic framework for planning, automating, and executing security testing throughout the software development lifecycle, ensuring vulnerabilities are identified proactively rather than in production.

---

## 3. Scope
- **In-Scope**:
  - Defining automated security testing suites in CI/CD pipelines\n  - Configuring Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST) workflows\n  - Formulating test scenarios for authentication, data validation, and session integrity\n  - Executing security regression suites on build artifacts
- **Out-of-Scope**:
  - Active adversarial penetration testing and exploitation (delegate to `skills/02-security-engineering/penetration-testing/SKILL.md`)\n  - Architectural threat modeling (delegate to `skills/02-security-engineering/threat-modeling/SKILL.md`)

---

## 4. When to Use
- Integrating automated security checks into the CI/CD pipeline\n- Designing security test plans for new services or major feature releases\n- Executing scheduled security regressions prior to milestone releases

---

## 5. When Not to Use
- For exploratory manual penetration testing (use `skills/02-security-engineering/penetration-testing/SKILL.md`)\n- For non-security functional unit testing (use `skills/09-quality-assurance-and-testing/unit-testing/SKILL.md`)

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
### 8.1 Security Testing Matrix
Implement testing across the full development pipeline:

| Testing Tier | Tooling Class | Target Phase | Primary Focus |
|---|---|---|---|
| **SAST** | Static Analysis | Pre-Commit / Build | Syntax patterns, hardcoded secrets, injection sinks, dangerous functions |
| **SCA** | Dependency Audit | Build / PR Gate | Known CVEs in third-party libraries and lockfiles |
| **DAST** | Dynamic Scanning | Staging / Deploy | Runtime endpoints, header misconfigurations, SSL/TLS, active inputs |
| **IAST** | Interactive Testing | Test Execution | Runtime instrumented data flows and unvalidated deserialization |

### 8.2 Security Test Case Formulation
Every testable feature must define security test cases covering:
1. **Input Fuzzing**: Boundary values, SQL syntax tokens, script tags (`<script>`, `javascript:`), null bytes, overly large payloads.
2. **Authentication State**: Requesting protected endpoints without tokens, with expired tokens, with tampered signatures.
3. **Authorization Boundary**: Accessing tenant A resources using tenant B credentials (IDOR verification).
4. **Transport Encryption**: Enforcing HTTPS and validating Secure/HttpOnly/SameSite cookie attributes.

---

## 9. Step-by-Step Workflow
1. **Step 1: Security Requirements & Scope Intake**
   - Review feature functional spec and identify sensitive assets (PII, credentials, payment tokens).
   - Define security test criteria mapped to OWASP ASVS Level 2 requirements.
2. **Step 2: Static Analysis (SAST) Execution**
   - Run local linting and static security rules against modified source files.
   - Verify zero hardcoded secrets or raw query concatenations.
3. **Step 3: Automated Security Test Authoring**
   - Write automated integration tests targeting authorization failure states and input boundary rejections.
4. **Step 4: Dynamic & Regression Sweep**
   - Execute the test suite and verify that all security assertions return expected HTTP 401/403/422 responses.
5. **Step 5: Documentation & Gate Verification**
   - Document results in `docs_agent/security/SECURITY_ASSESSMENT.md` and confirm Security Release Gate passes.

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
