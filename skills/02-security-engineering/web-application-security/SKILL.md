---
name: web-application-security
description: "Audit, defense, and remediation of OWASP Top 10 web vulnerabilities including XSS, CSRF, SSRF, path traversal, open redirects, and security headers."
version: 1.7.0
category: security
tags: ['security', 'web-security', 'owasp', 'xss', 'csrf', 'ssrf', 'security-headers']
---

# Skill: Web Application Security

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 02 — Security Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `web-application-security`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Harden web application frontends and backends against XSS, CSRF, SSRF, SQLi, clickjacking, and session hijacking.
- **When to Use**: Authoring web interfaces, handling user session tokens, configuring HTTP security headers, or processing forms.
- **Essential Invariants**:
  1. Context-aware output encoding is mandatory for all untrusted user content.
  2. Enforce strict Content Security Policy (CSP), CORS, and secure cookie attributes (HttpOnly, Secure, SameSite).
  3. Parameterized queries or ORM bindings are mandatory for all database operations.
- **Minimal Workflow**:
  1. Audit HTML rendering templates for unsafe unescaped inputs (e.g. dangerouslySetInnerHTML).
  2. Configure hardened HTTP headers (CSP, HSTS, X-Content-Type-Options, X-Frame-Options).
  3. Validate CSRF token verification on state-changing endpoints.
  4. Run automated web vulnerability scanners against staging instances.
- **Expected Deliverables**: Hardened web application configuration and passing automated web security tests.
- **Critical Restrictions**: Never disable browser security controls (CORS/CSP) to fix integration bugs.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides comprehensive engineering instructions for identifying, defending against, and remediating classic and modern web application vulnerabilities across client and server layers.

---

### Scope
- **In-Scope**:
  - Stored, reflected, and DOM-based Cross-Site Scripting (XSS) defense\n  - Cross-Site Request Forgery (CSRF) protection using anti-CSRF tokens and SameSite cookies\n  - Server-Side Request Forgery (SSRF) defense via strict IP allowlists and URL parsing\n  - Path traversal and unrestricted file upload remediation\n  - HTTP security header configuration (CSP, HSTS, X-Content-Type-Options)
- **Out-of-Scope**:
  - API-specific object-level authorization (delegate to `skills/02-security-engineering/api-security-testing/SKILL.md`)\n  - Low-level network firewall architecture

---

### When to Use
- Developing or reviewing web frontend and server-rendered templates\n- Implementing file upload handlers, redirect logic, or external fetchers\n- Configuring production web servers or reverse proxies

---

### When Not to Use
- For pure command-line tools without web or HTTP interfaces

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
### 8.1 Primary Web Vulnerability Defenses
1. **XSS Defense**:
   - Context-aware output encoding (HTML, JavaScript, CSS, URL contexts).
   - Use safe templating frameworks that auto-escape by default (React, Vue, Jinja2 autoescape).
   - Enforce Content Security Policy (CSP): `default-src 'self'; script-src 'self'; object-src 'none';`.
2. **CSRF Defense**:
   - Set all session cookies with `SameSite=Lax` or `SameSite=Strict`.
   - Implement cryptographically random anti-CSRF tokens on state-changing requests (POST, PUT, DELETE, PATCH).
3. **SSRF Defense**:
   - Parse and validate destination URLs against an allowlist of allowed domains.
   - Resolve DNS and reject private/loopback IP ranges (`127.0.0.0/8`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `169.254.169.254`).
   - Disable HTTP redirects in the HTTP client library when fetching untrusted URLs.
4. **File Upload Security**:
   - Validate file extension against a strict allowlist; do not trust `Content-Type` headers alone.
   - Re-encode uploaded images or store files in an isolated object bucket outside the application execution root.
   - Generate random unique filenames on storage (e.g. UUIDv4).

---

### Step-by-Step Workflow
1. **Step 1: Input and Output Vector Audit**
   - Identify all points where user-supplied data enters the web layer and where it is rendered.
2. **Step 2: Security Header Verification**
   - Check response headers for CSP, HSTS (`Strict-Transport-Security: max-age=31536000; includeSubDomains`), `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`.
3. **Step 3: Contextual Encoding & Sanitization**
   - Verify that all dynamic variables in HTML templates use proper escaping.
4. **Step 4: SSRF & Upload Gate Audit**
   - Test external fetch utilities with internal IP addresses; verify rejection.
5. **Step 5: Regression Test Authoring**
   - Add automated web tests asserting security headers and input rejection.

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
