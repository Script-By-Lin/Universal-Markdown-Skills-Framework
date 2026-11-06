---
name: api-security-testing
description: "Audit, testing, and hardening of REST, GraphQL, and gRPC APIs against the OWASP API Security Top 10 including BOLA, BFLA, and mass assignment."
version: 1.7.0
category: security
tags: ['security', 'api-security', 'owasp-api', 'bola', 'bfla', 'graphql', 'grpc']
---

# Skill: API Security Testing

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 02 — Security Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `api-security-testing`
- **Category**: Security Engineering (Domain 02)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Validate API endpoints against BOLA/IDOR, broken authentication, excessive data exposure, and rate limiting bypasses.
- **When to Use**: Authoring or modifying REST, GraphQL, or gRPC endpoints, webhooks, or public API gateways.
- **Essential Invariants**:
  1. Object-level authorization checks must occur on every single resource access.
  2. Enforce strict request payload schema validation and size limits.
  3. Rate limiting and throttling must be active on all public and authentication routes.
- **Minimal Workflow**:
  1. Test object-level authorization across multiple user tenant IDs (BOLA/IDOR tests).
  2. Fuzz request schemas with oversized, malformed, and unexpected data types.
  3. Verify rate limiting response (HTTP 429) under burst traffic.
  4. Inspect JSON response payloads to ensure sensitive internal fields are stripped.
- **Expected Deliverables**: API security test suite passing with exit code 0 and IDOR regression tests in place.
- **Critical Restrictions**: Never expose internal database IDs or stack traces in API error responses.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Governs the security assessment and defensive engineering of web APIs, preventing unauthorized object access, function escalation, and excessive data exposure.

---

### Scope
- **In-Scope**:
  - Broken Object-Level Authorization (BOLA / IDOR) testing and prevention\n  - Broken Function-Level Authorization (BFLA) testing\n  - Mass assignment and excessive data exposure auditing\n  - Rate limiting, resource exhaustion, and throttling verification\n  - GraphQL query depth and complexity limits
- **Out-of-Scope**:
  - General web frontend XSS/CSRF testing (delegate to `skills/02-security-engineering/web-application-security/SKILL.md`)

---

### When to Use
- Designing, implementing, or reviewing REST, GraphQL, or gRPC endpoints\n- Auditing API contracts for sensitive data leakage in response models\n- Testing API gateway routing and authorization filters

---

### When Not to Use
- For offline batch scripts without network endpoints

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
### 8.1 OWASP API Security Top 10 Defense Principles
1. **BOLA (API1:2023)**: Never assume a user owns an object just because they provide its ID (`/api/orders/{id}`). Always validate that `order.user_id === current_user.id` or that the tenant owns the record.
2. **Broken Authentication (API2:2023)**: Validate token signatures, expiry (`exp`), and algorithm (`alg: HS256/RS256`). Reject `alg: none`.
3. **Broken Object Property Level Authorization (API3:2023)**:
   - Use explicit DTOs/Schemas for incoming requests; never bind raw request bodies directly to database entities (Mass Assignment defense).
   - Use dedicated response serializers; never return raw user or database models that might leak password hashes or internal keys.
4. **Unrestricted Resource Consumption (API4:2023)**: Enforce pagination caps (`limit <= 100`) and rate limits by client IP/token.
5. **BFLA (API5:2023)**: Verify administrative endpoints (`/api/admin/*`) enforce role checks server-side, not merely hidden in client navigation.

---

### Step-by-Step Workflow
1. **Step 1: API Endpoint & Schema Discovery**
   - Inspect OpenAPI/Swagger specs or route definitions to inventory all endpoints and parameters.
2. **Step 2: BOLA / IDOR Matrix Testing**
   - Create two test identities (User A and User B).
   - Attempt to access, update, and delete User A objects using User B tokens.
3. **Step 3: Mass Assignment & Response Filtering Check**
   - Submit unexpected fields (e.g. `{"is_admin": true}`) in update payloads; verify rejection.
   - Inspect responses for sensitive fields (hashes, internal IPs, stack traces).
4. **Step 4: Rate Limiting & Throttling Verification**
   - Send burst test requests to verify HTTP 429 Too Many Requests responses.
5. **Step 5: Document Findings in Security Register**
   - Log any authorization bypasses in `docs_agent/security/VULNERABILITY_REGISTER.md`.

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
