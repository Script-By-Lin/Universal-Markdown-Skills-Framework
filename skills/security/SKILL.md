---
name: security
description: Threat modeling, input sanitization, OWASP Top 10 mitigation, secure credential management, authentication, and authorization hardening.
version: 1.0.0
category: security
tags: [security, owasp, auth, sanitization, encryption, vulnerability, xss, csrf]
---

# Skill: Application Security & Threat Mitigation

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `security`
- **Category**: Security & Hardening
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes mandatory security engineering practices to protect software systems from common vulnerabilities (including OWASP Top 10), prevent sensitive data exposure, enforce robust authentication and authorization checks, and sanitize external inputs.

---

## 3. Scope
- **In-Scope**:
  - Threat modeling and vulnerability assessment of application flows.
  - Mitigating OWASP Top 10 risks (SQLi, XSS, CSRF, broken access control, SSRF).
  - Secure credential and API secret handling (zero hardcoding, environment injection).
  - Enforcing authorization and role-based access control (RBAC) at backend layers.
  - Cryptographic best practices (standard hashing, token generation).
- **Out-of-Scope**:
  - Physical infrastructure security and cloud VPC firewall routing.
  - Penetration testing tooling deployment.

---

## 4. When to Use
- When authoring authentication, authorization, or permission checking logic.
- When creating endpoints that accept raw user input, file uploads, or external URLs.
- During security audits, code reviews, and dependency vulnerability scans.

---

## 5. When Not to Use
- For pure typographical or layout documentation edits with no security surface.

---

## 6. Prerequisites
- Target endpoint, data flow, or authentication architecture identified.
- Security constraints in [`RULES.md`](../../RULES.md) reviewed.

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md) (Precedence Level 2).
- System architecture in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).

---

## 8. Core Instructions
1. **Zero Hardcoded Secrets (Non-Negotiable)**:
   - Never commit passwords, private keys, API tokens, or bearer secrets into git.
   - Load secrets exclusively via environment variables. Ensure `.env` is listed in `.gitignore`.
2. **Defend Against Injection**:
   - For database queries: Use parameterized queries or ORM bindings exclusively. Never concatenate raw user input into SQL or NoSQL queries.
   - For OS commands: Avoid shell execution. If necessary, use argument arrays without shell interpolation.
3. **Prevent Cross-Site Scripting (XSS)**:
   - Escape and sanitize all user-supplied data before rendering it into HTML/DOM contexts.
   - Use framework-native auto-escaping (React JSX, Vue templates). Never bypass escaping with `dangerouslySetInnerHTML` or `v-html` unless strictly sanitized.
4. **Enforce Backend Authorization**:
   - Never rely on client-side UI visibility to secure features.
   - Validate user identity and permissions on every incoming request at the server/controller layer.
5. **Least Privilege & Safe Cryptography**:
   - Store passwords using industry-standard salted hashing algorithms (Argon2id, bcrypt). Never use MD5, SHA-1, or plain SHA-256 for passwords.

---

## 9. Step-by-Step Workflow
1. **Step 1: Identify Trust Boundaries & Attack Surfaces**
   - Map entry points: HTTP parameters, headers, query strings, webhooks, file uploads.
2. **Step 2: Threat Modeling (STRIDE)**
   - Analyze potential threats: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege.
3. **Step 3: Implement Defenses**
   - Add input validation schema.
   - Apply parameterized database queries.
   - Enforce authentication middleware and RBAC permission checks.
4. **Step 4: Audit Output & Logging**
   - Verify that logs sanitize sensitive data (credit cards, passwords, SSNs, bearer tokens).
5. **Step 5: Automated Security Verification**
   - Run automated security linters and negative test cases verifying that unauthenticated or unauthorized requests are rejected (HTTP 401/403).

---

## 10. Quality Standards
- **Zero Known Vulnerabilities**: Passes static security analysis (Semgrep, Sonar, bandit, npm audit) with zero critical/high findings.
- **Fail Closed**: In the event of an authentication or authorization failure, the system denies access by default.
- **Data Protection**: PII and secrets are encrypted in transit (TLS) and masked in logs.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Secret Scan | Repository grep for keys/tokens | Zero API keys, private keys, or passwords committed |
| Injection Verification | Static code inspection | All database queries use parameterized placeholders |
| Authorization Test | Automated negative test | Unauthenticated/unauthorized request receives 401/403 |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Client-Only Security | Attackers bypass UI and call backend endpoints directly | Enforce permissions on every backend route |
| Logging Raw Request Bodies | Leaks user passwords and tokens into plaintext server logs | Mask or filter sensitive fields before logging |

---

## 13. Restrictions
- Do NOT disable CSRF protection, CORS checks, or SSL verification without explicit documented justification.
- Do NOT invent custom encryption or hashing algorithms.

---

## 14. Expected Deliverables
- Hardened code modules with input validation and parameterization.
- Negative security test cases verifying protection mechanisms.

---

## 15. Documentation Requirements
- Record threat model findings and security invariants in [`MEMORY.md`](../../MEMORY.md).
- Update [`TASKS.md`](../../TASKS.md) with security review status.

