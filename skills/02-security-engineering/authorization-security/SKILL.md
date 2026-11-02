---
name: authorization-security
description: "Design, implementation, and testing of robust access control, RBAC/ABAC models, IDOR prevention, and multi-tenant isolation."
version: 1.0.0
category: security
tags: ['security', 'authorization', 'access-control', 'rbac', 'abac', 'idor', 'multi-tenant']
---

# Skill: Authorization Security

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 02 — Security Engineering

---

## 1. Metadata
- **Identifier**: `authorization-security`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Guarantees that authenticated users and services can only access and manipulate resources they explicitly own or are authorized to manage, preventing horizontal and vertical privilege escalation.

---

## 3. Scope
- **In-Scope**:
  - Insecure Direct Object Reference (IDOR / BOLA) elimination\n  - Role-Based Access Control (RBAC) and Attribute-Based Access Control (ABAC)\n  - Vertical privilege escalation prevention (user gaining admin privileges)\n  - Horizontal privilege escalation prevention (tenant A accessing tenant B records)\n  - Row-level security and multi-tenant data partitioning
- **Out-of-Scope**:
  - Identity verification (delegate to `skills/02-security-engineering/authentication-security/SKILL.md`)

---

## 4. When to Use
- Authoring endpoints that access, modify, or delete database resources by ID\n- Implementing multi-tenant architectures or organization hierarchies\n- Designing administrative dashboards or privileged control panels

---

## 5. When Not to Use
- For purely unauthenticated public content

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
### 8.1 The Golden Rule of Authorization
**Never trust client-supplied resource identifiers alone.**
Every data query fetching user or tenant data must bind ownership constraints into the database query:
```sql
-- VULNERABLE: IDOR / BOLA
SELECT * FROM orders WHERE id = $1;

-- SECURE: Ownership constraint enforced
SELECT * FROM orders WHERE id = $1 AND user_id = $current_user_id;
```

### 8.2 Authorization Architecture Invariants
1. **Server-Side Enforcement**: Authorization decisions must occur on the server or API layer. Hiding buttons in the UI is not security.
2. **Default Deny**: Access control policies must default to denying access unless an explicit permission or role grant matches.
3. **Tenant Context**: In multi-tenant systems, every request must resolve the tenant context from the validated session/token, not from query strings or request headers.
4. **Hierarchical RBAC**: Ensure admin routes (`/admin/*`) verify administrative roles via server-side middleware before controller execution.

---

## 9. Step-by-Step Workflow
1. **Step 1: Role & Permission Matrix Definition**
   - Map all roles (e.g. Guest, Member, Manager, Admin) to actions (Create, Read, Update, Delete) on each resource.
2. **Step 2: Middleware & Controller Enforcement**
   - Apply centralized authorization guards or policies to every controller route.
3. **Step 3: Database Query Scoping**
   - Enforce row-level security or user-scoping in all repository queries.
4. **Step 4: Matrix Testing Across User Contexts**
   - Execute integration tests with multiple distinct user accounts verifying HTTP 403 Forbidden on cross-account access.
5. **Step 5: Signoff in Security Gate**
   - Verify zero IDOR findings before approving production releases.

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
