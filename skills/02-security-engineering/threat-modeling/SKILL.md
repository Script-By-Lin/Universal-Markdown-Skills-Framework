---
name: threat-modeling
description: "Structured architectural threat modeling using STRIDE / PASTA methodologies, trust boundary mapping, asset identification, and mitigation planning."
version: 1.0.0
category: security
tags: ['security', 'threat-modeling', 'stride', 'pasta', 'architecture', 'trust-boundaries']
---

# Skill: Threat Modeling

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `threat-modeling`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Establishes a proactive security design practice to identify threats, attack surfaces, and risk mitigations before software implementation begins.

---

## 3. Scope
- **In-Scope**:
  - Decomposing application architecture into data flows, processes, and data stores\n  - Identifying trust boundaries between clients, servers, and external third parties\n  - Applying the STRIDE threat categorization model (Spoofing, Tampering, Repudiation, Info Disclosure, DoS, Elevation of Privilege)\n  - Formulating concrete, traceable security controls for identified threats
- **Out-of-Scope**:
  - Post-implementation penetration testing and active exploitation

---

## 4. When to Use
- Designing new services, architectures, or major feature capabilities\n- Conducting architectural reviews before major data migrations or integrations\n- Evaluating third-party integrations and webhook intake flows

---

## 5. When Not to Use
- For minor cosmetic or non-functional documentation updates

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
### 8.1 The STRIDE Threat Modeling Framework
Evaluate every trust boundary against the six STRIDE threat categories:

| Threat Category | Property Violated | Threat Description | Canonical Mitigation |
|---|---|---|---|
| **S**poofing | Authenticity | Pretending to be an authorized user or service | Strong authentication, mTLS, JWT signature verification |
| **T**ampering | Integrity | Modifying data in transit or at rest | TLS 1.3, HMAC signatures, checksums, DB write validation |
| **R**epudiation | Non-repudiability | Denying performing an action | Tamper-evident audit logs, append-only ledgers |
| **I**nformation Disclosure | Confidentiality | Exposing sensitive data to unauthorized actors | Encryption at rest/transit, field-level masking, least privilege |
| **D**enial of Service | Availability | Exhausting resources to degrade service | Rate limiting, timeouts, connection pooling, backpressure |
| **E**levation of Privilege | Authorization | Gaining unauthorized capabilities | Strict RBAC/ABAC, principle of least privilege, zero trust |

### 8.2 Trust Boundary Identification
Map all boundaries where data transitions between different trust levels:
- Internet Client <-> Reverse Proxy / CDN (Untrusted to Semi-Trusted)
- Application Server <-> Database (Trusted internal network)
- Application Server <-> External Payment / SMS Gateway (Trusted to External Third-Party)

---

## 9. Step-by-Step Workflow
1. **Step 1: Architectural Decomposition**
   - Draw or document data flow diagrams (DFD) showing actors, processes, data stores, and data flows.
2. **Step 2: Identify Trust Boundaries & Sensitive Assets**
   - Mark trust boundary crossings and catalog assets (PII, tokens, financial data).
3. **Step 3: STRIDE Threat Analysis**
   - Systematically walk through each element and apply the STRIDE taxonomy.
4. **Step 4: Define Mitigation Strategies**
   - Assign a concrete technical control to each identified threat.
5. **Step 5: Publish Threat Model Document**
   - Author `docs_agent/security/THREAT_MODEL.md` and link to related architectural ADRs.

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
