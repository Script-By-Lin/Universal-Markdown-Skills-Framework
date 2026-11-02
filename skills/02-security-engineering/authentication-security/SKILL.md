---
name: authentication-security
description: "Implementation, audit, and hardening of authentication mechanisms, password hashing, session tokens, JWTs, and MFA workflows."
version: 1.0.0
category: security
tags: ['security', 'authentication', 'passwords', 'jwt', 'sessions', 'mfa', 'owasp']
---

# Skill: Authentication Security

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `authentication-security`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Governs the design, implementation, and verification of secure user and machine identity verification, protecting against credential stuffing, session hijacking, and auth bypass.

---

## 3. Scope
- **In-Scope**:
  - Secure password hashing using Argon2id or bcrypt with adaptive work factors\n  - Session management, token generation (CSPRNG), and rotation\n  - JWT validation (signature, expiry, audience, issuer, algorithm enforcement)\n  - Brute-force protection, account lockouts, and rate limiting\n  - Multi-Factor Authentication (MFA / TOTP) verification
- **Out-of-Scope**:
  - Post-authentication permission checks (delegate to `skills/02-security-engineering/authorization-security/SKILL.md`)

---

## 4. When to Use
- Designing or refactoring login, signup, password reset, or token exchange workflows\n- Auditing session persistence and cookie security parameters\n- Implementing machine-to-machine API key or OAuth2 client credentials flows

---

## 5. When Not to Use
- For public static assets or unauthenticated public views

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
### 8.1 Password & Credential Security Rules
- **Hashing**: Use **Argon2id** (memory: 64MB, iterations: 3) or **bcrypt** (cost: 12+). Never use MD5, SHA-1, SHA-256, or plain hashes without salts.
- **Timing Attacks**: Use constant-time comparison functions (e.g. `crypto.timingSafeEqual`) when validating hashes, tokens, or signatures.
- **Account Enumeration**: Return identical error messages for invalid username and invalid password (e.g. "Invalid email or password").

### 8.2 Session & Token Security Rules
- **Session Tokens**: Generate with a cryptographically secure pseudo-random number generator (CSPRNG, min 128 bits of entropy).
- **Cookies**: Always set `Secure; HttpOnly; SameSite=Lax` (or `SameSite=Strict`).
- **Session Expiration**: Enforce idle timeouts (e.g. 15-30 minutes) and absolute session limits (e.g. 12-24 hours).
- **JWT Verification**:
  - Explicitly whitelist permitted algorithms (e.g. `algorithms: ['RS256']`). Never allow `alg: none`.
  - Always validate `exp`, `nbf`, `iss`, and `aud` claims. Store access tokens in memory or HttpOnly cookies, not `localStorage`.

---

## 9. Step-by-Step Workflow
1. **Step 1: Authentication Surface Inventory**
   - Identify all login, registration, token refresh, and password recovery endpoints.
2. **Step 2: Password Storage & Hash Audit**
   - Inspect user model to confirm Argon2id/bcrypt hashing with automatic per-user salt.
3. **Step 3: Session Lifecycle & Invalidation Test**
   - Test password change and logout flows; verify that old sessions and refresh tokens are immediately invalidated in the database/cache.
4. **Step 4: Brute-Force & Rate Limiting Test**
   - Verify that sequential failed login attempts trigger account lockouts or exponential delays.
5. **Step 5: Verification & Gate Review**
   - Author automated tests verifying token expiry and rejection of tampered tokens.

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
