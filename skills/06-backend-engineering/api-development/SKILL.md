---
name: api-development
description: Contract design, versioning, serialization, status codes, and security standards for REST, GraphQL, and gRPC APIs.
version: 1.7.0
category: development
tags: [api, rest, graphql, grpc, openapi, contracts, json, serialization]
---

# Skill: API Design & Contract Development

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 06 — Backend Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `api-development`
- **Category**: Backend Engineering (Domain 06)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Design, implement, and document deterministic RESTful, GraphQL, and RPC APIs with strict schema contracts.
- **When to Use**: Building new API endpoints, evolving existing web services, or authoring OpenAPI/Swagger specifications.
- **Essential Invariants**:
  1. API responses must adhere strictly to documented schema contracts (OpenAPI/JSON Schema/Zod).
  2. Use standard HTTP status codes correctly (200, 201, 204, 400, 401, 403, 404, 409, 422, 500).
  3. Implement backward compatibility; never introduce breaking schema changes without versioning.
- **Minimal Workflow**:
  1. Define explicit request and response schemas with strict field types.
  2. Implement endpoint route handlers and middleware (validation, auth, rate limiting).
  3. Author contract and integration tests verifying request validation and response formats.
  4. Verify API test suite execution with exit code 0.
- **Expected Deliverables**: Documented, schema-validated API endpoints with passing automated contract test suites.
- **Critical Restrictions**: Never return unstructured 500 error strings to clients; never expose database column names directly.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes strict engineering standards for designing, documenting, versioning, and implementing client-server API interfaces across REST, GraphQL, and gRPC paradigms. It guarantees predictable contracts, standard HTTP semantics, and robust error formats.

---

### Scope
- **In-Scope**:
  - Designing API resource endpoints and URI hierarchies.
  - Formulating OpenAPI / Swagger or GraphQL schema contracts.
  - Applying standard HTTP methods, headers, status codes, and idempotency keys.
  - Structuring predictable, RFC 7807-compliant error payloads.
  - Versioning strategies (URI path versioning vs. header versioning).
- **Out-of-Scope**:
  - Low-level database queries and indexing (delegate to [`skills/database-design/SKILL.md`](../../database-design/SKILL.md)).
  - Frontend component presentation (delegate to [`skills/ui-ux-pro-max/SKILL.md`](../../ui-ux-pro-max/SKILL.md)).

---

### When to Use
- When introducing a new external or internal API endpoint.
- When drafting OpenAPI specifications or updating schema definitions.
- When resolving breaking API changes or authoring API migration strategies.

---

### When Not to Use
- For internal module-to-module in-memory function calls.
- When altering backend domain calculations without changing external contracts.

---

### Prerequisites
- Target consumer requirements understood.
- Authentication/authorization mechanism verified.

---

### Required Context
- Security rules in [`RULES.md`](../../../RULES.md).
- Existing endpoints documented in [`CONTEXT.md`](../../../CONTEXT.md).

---

### Core Instructions
1. **RESTful Semantics**:
   - Use nouns for resource paths: `GET /api/v1/orders`, `POST /api/v1/orders`. Never use verbs in paths (`POST /api/v1/createOrder` is prohibited).
   - Use correct HTTP verbs: `GET` (idempotent read), `POST` (create), `PUT` (complete replacement), `PATCH` (partial update), `DELETE` (removal).
2. **Standard HTTP Status Codes**:
   - `200 OK`: Successful read or update.
   - `201 Created`: Resource successfully created (with `Location` header).
   - `204 No Content`: Successful action with empty response body.
   - `400 Bad Request`: Validation failure.
   - `401 Unauthorized`: Missing or invalid authentication token.
   - `403 Forbidden`: Authenticated user lacks permission.
   - `404 Not Found`: Resource does not exist.
   - `409 Conflict`: Unique constraint violation or state conflict.
   - `500 Internal Server Error`: Unhandled server exception (never return 200 with error payload).
3. **Structured Error Schema (RFC 7807)**:
   - Error payloads must follow predictable structure:
     ```json
     {
       "type": "https://api.example.com/errors/invalid-input",
       "title": "Invalid Request Parameters",
       "status": 400,
       "detail": "Field 'email' is formatted incorrectly.",
       "instance": "/api/v1/users",
       "errors": [{ "field": "email", "message": "Must be a valid email address" }]
     }
     ```
4. **Pagination & Filtering**:
   - List endpoints must support cursor or offset-based pagination (`limit`, `cursor`/`offset`) and return total count or `next_cursor`. Never return unbounded lists.

---

### Step-by-Step Workflow
1. **Step 1: Draft Contract Specification**
   - Author OpenAPI spec or schema definition defining paths, request schemas, and response types.
2. **Step 2: Validate Contract Against Standards**
   - Verify noun URIs, status codes, and error payloads.
3. **Step 3: Implement Endpoint Route & Controller**
   - Bind contract to endpoint handler with strict input validation middleware.
4. **Step 4: Author Integration & Contract Tests**
   - Write automated tests verifying request parsing, status codes, headers, and validation errors.
5. **Step 5: Publish API Documentation**
   - Update contract documentation.

---

### Quality Standards
- **Backward Compatibility**: Non-breaking changes only within minor versions. Breaking changes require version increments (`/v1` to `/v2`).
- **Contract Fidelity**: 100% agreement between OpenAPI schema and actual runtime payload.
- **Security**: Strict input schema validation on every request payload.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Contract Schema Test | Schema validator runner | API response matches OpenAPI JSON schema |
| Error Status Check | Negative test cases | Returns correct 4xx status with RFC 7807 error body |
| Unbounded List Prevention | Large dataset query | Responses capped at maximum page limit |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| HTTP 200 with `{ "error": true }` | Breaks standard HTTP client error handling and caching | Return proper 4xx/5xx HTTP status codes |
| Unbounded Collection Returns | Triggers memory exhaustion and database denial of service | Enforce default and maximum pagination limits |

---

### Restrictions
- Do NOT expose internal database IDs or stack traces in public error payloads.
- Do NOT introduce breaking contract modifications without version bumps.

---

### Expected Deliverables
- OpenAPI contract or GraphQL schema file.
- Endpoint controller implementations.
- API contract integration tests.

---

### Documentation Requirements
- Update API endpoint listings in [`CONTEXT.md`](../../../CONTEXT.md).
- Record API breaking decisions in [`DECISIONS.md`](../../../DECISIONS.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
