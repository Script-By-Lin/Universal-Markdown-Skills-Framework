---
name: authentication-security
description: "Implementation, audit, and hardening of authentication mechanisms, password hashing, session tokens, JWTs, and MFA workflows."
version: 1.7.0
category: security
tags: ['security', 'authentication', 'passwords', 'jwt', 'sessions', 'mfa', 'owasp']
---

# Skill: Authentication Security Engineering

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 02 — Security Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `authentication-security`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Implement robust, attack-resistant user authentication, credential storage, MFA, and session lifecycle management.
- **When to Use**: Building or modifying login, registration, password reset, token issuance, or session validation flows.
- **Essential Invariants**:
  1. Passwords must be hashed using Argon2id, bcrypt, or PBKDF2 with adequate work factors; never MD5/SHA.
  2. Session tokens must be cryptographically random with high entropy (>= 128 bits) and bounded lifetimes.
  3. Enforce rate limiting and account lockout/backoff on credential verification endpoints.
- **Minimal Workflow**:
  1. Verify password hashing algorithm and salt generation parameters.
  2. Audit session token issuance, rotation, and revocation endpoints.
  3. Implement timing-safe string comparison for token/signature verification.
  4. Run automated authentication regression suite verifying failed and successful login states.
- **Expected Deliverables**: Hardened authentication module with comprehensive automated security tests.
- **Critical Restrictions**: Never store plaintext credentials; never pass session tokens in URL query parameters.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Governs the design, implementation, and verification of secure user and machine identity verification, protecting against credential stuffing, session hijacking, and auth bypass.

---

### Scope
- **In-Scope**:
  - Secure password hashing using Argon2id or bcrypt with adaptive work factors\n  - Session management, token generation (CSPRNG), and rotation\n  - JWT validation (signature, expiry, audience, issuer, algorithm enforcement)\n  - Brute-force protection, account lockouts, and rate limiting\n  - Multi-Factor Authentication (MFA / TOTP) verification
- **Out-of-Scope**:
  - Post-authentication permission checks (delegate to `skills/02-security-engineering/authorization-security/SKILL.md`)

---

### When to Use
- Designing or refactoring login, signup, password reset, or token exchange workflows\n- Auditing session persistence and cookie security parameters\n- Implementing machine-to-machine API key or OAuth2 client credentials flows

---

### When Not to Use
- For public static assets or unauthenticated public views

---

### Prerequisites
- Target application components and architecture inspected.
- Context verified against [`CONTEXT.md`](../../../CONTEXT.md).
- Security testing boundaries established in compliance with [`RULES.md`](../../../RULES.md).

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (Precedence Level 2).
- Security posture in [`CONTEXT.md`](../../../CONTEXT.md).
- Active vulnerability records in [`docs_agent/security/VULNERABILITY_REGISTER.md`](../../../templates/VULNERABILITY_REGISTER.md) (if present).

---

### Core Instructions
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

### Step-by-Step Workflow
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

### Quality Standards
- **Standard 1**: 100% adherence to non-destructive testing boundaries defined in [`RULES.md`](../../../RULES.md).
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
- Record reusable security lessons and attack vectors in [`MEMORY.md`](../../../MEMORY.md).
- Record architectural security decisions in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
