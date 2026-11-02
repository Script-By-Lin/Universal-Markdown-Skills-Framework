---
name: backend-development
description: Guidelines for maintainable, secure, and performant backend services, domain business logic, and data access.
version: 1.0.0
category: development
tags: [backend, api, business-logic, domain-model, data-access, services]
---

# Skill: Backend Development

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `backend-development`
- **Category**: Engineering & Development
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill provides comprehensive standards for authoring production-grade backend systems, including domain service logic, data persistence adapters, input validation, robust error handling, and transactional integrity.

---

## 3. Scope
- **In-Scope**:
  - Implementation of core domain services and business rules.
  - Integration with data access layers (repositories, ORMs, query builders).
  - Robust exception handling, validation pipelines, and logging.
  - Ensuring transactional atomicity and data consistency.
- **Out-of-Scope**:
  - Frontend components and client state (delegate to [`skills/frontend-development/SKILL.md`](../frontend-development/SKILL.md)).
  - Low-level database schema design and migrations (delegate to [`skills/database-design/SKILL.md`](../database-design/SKILL.md)).

---

## 4. When to Use
- Implementing business logic, computational routines, or data processing pipelines.
- Building backend controllers, handlers, services, and repository classes.
- Refactoring backend business rules for testability and performance.

---

## 5. When Not to Use
- When defining external API wire contracts only (use [`skills/api-development/SKILL.md`](../api-development/SKILL.md)).
- For frontend UI state or component rendering.

---

## 6. Prerequisites
- Functional requirements understood and verified.
- Target data models and storage mechanisms verified in [`CONTEXT.md`](../../CONTEXT.md).

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- Architectural boundaries defined in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).

---

## 8. Core Instructions
1. **Layer Separation**:
   - Keep HTTP/Transport controllers thin: parse request -> invoke domain service -> return response.
   - Domain services must contain business rules and be free of transport-specific classes (`HttpRequest`, `Response`).
2. **Fail Fast & Validate Input**:
   - Validate all input parameters using strong typing or schema validators before executing business operations.
3. **Deterministic Error Handling**:
   - Throw typed, domain-specific exceptions (e.g. `UserNotFoundException`, `InsufficientBalanceException`) rather than generic errors.
   - Never write empty catch blocks (`catch (e) {}`).
4. **Idempotency & Transactions**:
   - Operations that mutate multiple entities must execute within a transactional boundary or adhere to idempotent design.

---

## 9. Step-by-Step Workflow
1. **Step 1: Define Domain Interfaces & Types**
   - Author domain models, value objects, and repository interfaces.
2. **Step 2: Implement Business Logic (TDD Preferred)**
   - Author service methods fulfilling business rules, accompanying them with unit tests.
3. **Step 3: Implement Persistence Adapters**
   - Bind repository interfaces to real database or storage adapters using parameterized queries.
4. **Step 4: Wire Transport / Handlers**
   - Connect transport endpoints to domain services, validating inputs and mapping domain exceptions to HTTP status codes.
5. **Step 5: Execute Automated Verification**
   - Run unit and integration tests.

---

## 10. Quality Standards
- **Test Coverage**: 100% of domain business logic paths covered by automated unit tests.
- **Security**: Zero SQL injection vulnerabilities (parameterized queries strictly required); zero hardcoded credentials.
- **Type Safety**: Full type annotations on all public methods and functions.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Unit Test Suite | Test runner execution | All domain service tests pass |
| Security Inspection | Code audit | Zero raw SQL string interpolations; zero plain-text secrets |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Fat Controllers | Embedding SQL queries directly into route handlers prevents reuse and unit testing | Move data access to repositories and logic to services |
| Swallowing Exceptions | Hides catastrophic errors and corrupts data | Catch specifically, log with context, and rethrow or return typed error |

---

## 13. Restrictions
- Do NOT commit database passwords, API tokens, or secrets to repository files.
- Do NOT perform non-parameterized SQL queries.

---

## 14. Expected Deliverables
- Clean domain service and repository source files.
- Unit and integration tests verifying behavior.

---

## 15. Documentation Requirements
- Record reusable backend patterns in [`MEMORY.md`](../../MEMORY.md).
- Update [`TASKS.md`](../../TASKS.md) with task completion.

