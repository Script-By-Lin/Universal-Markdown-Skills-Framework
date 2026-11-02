---
name: dependency-security-audit
description: "Software composition analysis (SCA), auditing supply-chain vulnerabilities, lockfile integrity, dependency confusion, and license compliance."
version: 1.0.0
category: security
tags: ['security', 'dependencies', 'supply-chain', 'cve', 'sca', 'lockfiles']
---

# Skill: Dependency Security Audit

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `dependency-security-audit`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Ensures third-party open-source libraries, packages, and transitive dependencies do not introduce known vulnerabilities, malicious supply-chain payloads, or license violations.

---

## 3. Scope
- **In-Scope**:
  - Auditing dependency manifests and deterministic lockfiles\n  - Checking dependencies against public vulnerability databases (NVD, GitHub Advisory)\n  - Detecting dependency confusion and typo-squatting risks\n  - Verifying package license compatibility (e.g. permissive vs copyleft)
- **Out-of-Scope**:
  - Proprietary in-house business logic review (delegate to `skills/02-security-engineering/security-code-review/SKILL.md`)

---

## 4. When to Use
- Adding new libraries or upgrading packages in the project\n- Running scheduled automated security checks in CI\n- Preparing software release bills of materials (SBOM)

---

## 5. When Not to Use
- For framework-internal UMSF operations (UMSF has zero dependencies)

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
### 8.1 Supply Chain Security Invariants
1. **Deterministic Lockfiles**: Always commit lockfiles (`package-lock.json`, `poetry.lock`, `Cargo.lock`, `go.sum`). Never use floating version ranges in production.
2. **Minimal Dependency Footprint**: Scrutinize every new package addition. Prefer native standard library capabilities where feasible.
3. **Private Package Scoping**: For internal packages, use scoped namespaces (e.g. `@myorg/package`) and configure private registry precedence to prevent Dependency Confusion attacks.
4. **Automated Audit CLI Integration**:
   - Node.js: `npm audit --audit-level=high`
   - Python: `pip-audit` or `safety check`
   - Rust: `cargo audit`
   - Go: `govulncheck ./...`

---

## 9. Step-by-Step Workflow
1. **Step 1: Manifest & Lockfile Inspection**
   - Verify lockfile presence and ensure it is in sync with package manifest.
2. **Step 2: Vulnerability Database Query**
   - Execute package manager security audit commands or scan dependency trees.
3. **Step 3: Severity Triaging**
   - Evaluate flagged CVEs for actual exploitability in the application context.
4. **Step 4: Safe Upgrade / Patching**
   - Apply non-breaking minor/patch updates; re-run test suite to confirm zero regressions.
5. **Step 5: Document Audit Findings**
   - Record audited dependencies and resolutions in `docs_agent/security/SECURITY_ASSESSMENT.md`.

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
