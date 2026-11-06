---
name: integration-testing
description: "Verification of interactions across service boundaries, database transactions, API contracts, inter-process messaging, and external adapters."
version: 1.7.0
category: quality
tags: ['testing', 'integration-testing', 'database', 'api-contracts', 'transactions']
---

# Skill: Integration Testing & Subsystem Verification

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `integration-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Verify communication, data contracts, and error handling across integrated modules, databases, and external APIs.
- **When to Use**: Testing database repositories, HTTP service clients, middleware stacks, or multi-module workflows.
- **Essential Invariants**:
  1. Integration tests must use realistic, ephemeral test environments (e.g. Testcontainers, local test DB).
  2. Clean up and reset test state between test cases to prevent test crosstalk.
  3. Assert on actual database records and external protocol exchanges.
- **Minimal Workflow**:
  1. Spin up ephemeral test resources (database, cache, mock server).
  2. Seed baseline test data and configure service connection strings.
  3. Execute multi-component operations asserting state changes and returned payloads.
  4. Tear down ephemeral test fixtures and verify exit code 0.
- **Expected Deliverables**: Passing integration test suite proving seamless multi-component interaction.
- **Critical Restrictions**: Never run integration tests against production databases or live third-party billing APIs.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Validates that independently developed software components correctly communicate, persist data, and handle transactions across real or simulated subsystem boundaries.

---

### Scope
- **In-Scope**:
  - Testing repository layers against real or containerized databases\n  - Validating API endpoint serialization, routing, and middleware pipelines\n  - Testing transactional rollbacks and data integrity constraints\n  - Testing message queue publishers and consumer handlers
- **Out-of-Scope**:
  - Isolated unit testing of pure functions without collaborators\n  - Full end-to-end multi-service browser simulation

---

### When to Use
- Verifying database migrations, queries, and ORM entity mapping\n- Testing API routes with authentication, authorization, and validation middleware\n- Testing external service client adapters

---

### When Not to Use
- For isolated business calculations testable via fast unit tests

---

### Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in [`TASKS.md`](../../../TASKS.md).

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (TDD invariants & Release Gates).
- Testing environment in [`CONTEXT.md`](../../../CONTEXT.md).
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

### Core Instructions
### 8.1 Integration Test Boundaries
Focus integration tests on actual points of interaction:
1. **Database Integration**:
   - Execute against an isolated test database (e.g. SQLite in-memory, Dockerized Postgres).
   - Use transactional rollbacks or database cleanups (`TRUNCATE`) between tests to prevent test pollution.
   - Verify that constraints (foreign keys, unique indexes, not-null) trigger expected errors.
2. **HTTP API Integration**:
   - Send actual HTTP requests through the full middleware stack (using test clients like Supertest or WebTestClient).
   - Verify status codes (200, 201, 400, 401, 403, 404, 422, 500) and response JSON payload schemas.

---

### Step-by-Step Workflow
1. **Step 1: Environment Setup & Isolation**
   - Ensure clean test database or service mocks are initialized.
2. **Step 2: Seed Test Data**
   - Use deterministic data factories to insert prerequisite parent records.
3. **Step 3: Execute Cross-Component Interaction**
   - Invoke endpoint or repository method across the boundary.
4. **Step 4: Verify Persistence & State Changes**
   - Query database directly to confirm state was persisted correctly.
5. **Step 5: Teardown & State Cleanup**
   - Clean up created records; confirm zero residual test data.

---

### Quality Standards
- **Standard 1**: 100% adherence to the mandatory TDD Red-Green-Refactor protocol.
- **Standard 2**: All tests must run deterministically with zero flakiness.
- **Standard 3**: Absolute prohibition on claiming tests passed without verifying execution exit code 0.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Test Execution | Automated test runner execution | 100% passing tests; exit code 0 |
| Regression Safety | Full regression suite execution | Zero regressions in existing capabilities |
| Coverage Integrity | Coverage instrumentation | Branch coverage meets agreed project threshold |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Writing Tests After Implementation | High susceptibility to confirmation bias | Follow TDD: write failing test first (RED phase) |
| Hardcoded Sleeps | Causes flaky, brittle, and slow test runs | Wait explicitly for state or DOM conditions |
| Shared Mutable Test Data | Tests fail unpredictably when run in parallel | Use isolated data factories and per-test cleanups |

---

### Restrictions
- Do NOT modify tests merely to force incorrect implementation code to pass.
- Do NOT delete failing tests without documented architectural authorization.
- Do NOT bypass Functional or Regression Release Gates.

---

### Expected Deliverables
- Automated test suites (unit, integration, or E2E).
- Updated testing logs in `docs_agent/testing/TDD_LOG.md` or `TEST_RESULTS.md`.
- Regression verification report.

---

### Documentation Requirements
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Record testing architectural trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
