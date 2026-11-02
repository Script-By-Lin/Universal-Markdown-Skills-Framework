---
name: api-development
description: Contract design, versioning, serialization, status codes, and security standards for REST, GraphQL, and gRPC APIs.
version: 1.0.0
category: development
tags: [api, rest, graphql, grpc, openapi, contracts, json, serialization]
---

# Skill: API Contract Design & Development

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `api-development`
- **Category**: Engineering & Protocols
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes strict engineering standards for designing, documenting, versioning, and implementing client-server API interfaces across REST, GraphQL, and gRPC paradigms. It guarantees predictable contracts, standard HTTP semantics, and robust error formats.

---

## 3. Scope
- **In-Scope**:
  - Designing API resource endpoints and URI hierarchies.
  - Formulating OpenAPI / Swagger or GraphQL schema contracts.
  - Applying standard HTTP methods, headers, status codes, and idempotency keys.
  - Structuring predictable, RFC 7807-compliant error payloads.
  - Versioning strategies (URI path versioning vs. header versioning).
- **Out-of-Scope**:
  - Low-level database queries and indexing (delegate to [`skills/database-design/SKILL.md`](../database-design/SKILL.md)).
  - Frontend component presentation (delegate to [`skills/frontend-development/SKILL.md`](../frontend-development/SKILL.md)).

---

## 4. When to Use
- When introducing a new external or internal API endpoint.
- When drafting OpenAPI specifications or updating schema definitions.
- When resolving breaking API changes or authoring API migration strategies.

---

## 5. When Not to Use
- For internal module-to-module in-memory function calls.
- When altering backend domain calculations without changing external contracts.

---

## 6. Prerequisites
- Target consumer requirements understood.
- Authentication/authorization mechanism verified.

---

## 7. Required Context
- Security rules in [`RULES.md`](../../RULES.md).
- Existing endpoints documented in [`CONTEXT.md`](../../CONTEXT.md).

---

## 8. Core Instructions
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

## 9. Step-by-Step Workflow
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

## 10. Quality Standards
- **Backward Compatibility**: Non-breaking changes only within minor versions. Breaking changes require version increments (`/v1` to `/v2`).
- **Contract Fidelity**: 100% agreement between OpenAPI schema and actual runtime payload.
- **Security**: Strict input schema validation on every request payload.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Contract Schema Test | Schema validator runner | API response matches OpenAPI JSON schema |
| Error Status Check | Negative test cases | Returns correct 4xx status with RFC 7807 error body |
| Unbounded List Prevention | Large dataset query | Responses capped at maximum page limit |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| HTTP 200 with `{ "error": true }` | Breaks standard HTTP client error handling and caching | Return proper 4xx/5xx HTTP status codes |
| Unbounded Collection Returns | Triggers memory exhaustion and database denial of service | Enforce default and maximum pagination limits |

---

## 13. Restrictions
- Do NOT expose internal database IDs or stack traces in public error payloads.
- Do NOT introduce breaking contract modifications without version bumps.

---

## 14. Expected Deliverables
- OpenAPI contract or GraphQL schema file.
- Endpoint controller implementations.
- API contract integration tests.

---

## 15. Documentation Requirements
- Update API endpoint listings in [`CONTEXT.md`](../../CONTEXT.md).
- Record API breaking decisions in [`DECISIONS.md`](../../DECISIONS.md).

