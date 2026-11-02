# SECURITY_TEST_PLAN.md — Application Security Testing Plan
# [Project Name]

> Security Testing Scope, Boundaries, and Authorization Specification  
> Authority: Independent Security Agent (Agent C)  

---

## 1. Testing Scope & Explicit Authorization Boundary
- **Target Application**: [Application Name / Version]
- **Target Environment**: [Local Development / Dedicated Staging Instance]
- **Ownership & Authorization**: [Verified User Ownership / Written Authorization]
- **Permitted Endpoints**:
  - `http://localhost:[PORT]/api/*`
  - `[Allowed test domain / staging URL]`
- **Prohibited Targets & Actions (STRICT)**:
  - Third-party payment gateways, external webhooks, or external OAuth providers.
  - Destructive queries (`DROP`, `DELETE`, `TRUNCATE` without test sandbox).
  - Uncontrolled Denial-of-Service (DoS) or brute-force floods.
  - Exfiltration of real user data or secrets.

---

## 2. Security Test Matrix

| Security Domain | Specific Probes | Methodology | Tools / Techniques |
|---|---|---|---|
| **Authentication** | Brute force, session hijacking, JWT tampering | Non-destructive PoC | Controlled test requests |
| **Authorization** | BOLA / IDOR, BFLA, tenant isolation | Matrix cross-account tests | 2 distinct test accounts |
| **Injection** | SQLi, Command Injection, Template Injection | Boolean / inert syntax probes | Passive review & inert payloads |
| **Web Security** | Stored/Reflected XSS, CSRF, SSRF, headers | DOM markers, header audits | Curl, browser inspect |
| **Supply Chain** | Known CVEs in dependencies, lockfile audit | Static composition analysis | Native package audit CLI |

---

## 3. Backup & Recovery Prerequisites
- [ ] Clean database snapshot available before active testing.
- [ ] Automated reset script verified to restore environment to baseline.
