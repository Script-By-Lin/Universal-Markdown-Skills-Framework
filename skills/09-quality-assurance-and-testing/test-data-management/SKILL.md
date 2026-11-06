---
name: test-data-management
description: "Deterministic test data synthesis, seeders, factory patterns, sensitive data masking, state cleanup, and test isolation."
version: 1.7.0
category: quality
tags: ['testing', 'test-data', 'factories', 'fixtures', 'seeding', 'masking', 'isolation']
---

# Skill: Test Data Management & Fixture Engineering

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `test-data-management`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Generate, isolate, sanitize, and manage realistic test data fixtures for deterministic automated testing.
- **When to Use**: Creating database seeds, managing complex test fixtures, or sanitizing production data for staging environments.
- **Essential Invariants**:
  1. Never use unmasked production PII, passwords, or payment data in test environments.
  2. Test data fixtures must be deterministic, reproducible, and version-controlled.
  3. Tests must be idempotent; test data setup and teardown must prevent test crosstalk.
- **Minimal Workflow**:
  1. Define synthetic data generation factories using Faker/FactoryBot patterns.
  2. Implement automated database seeding and transaction rollback fixtures.
  3. Mask and sanitize any sanitized production dumps before staging import.
  4. Verify tests execute idempotently with clean data isolation.
- **Expected Deliverables**: Deterministic test fixture factories and automated data sanitization scripts.
- **Critical Restrictions**: Strictly prohibit copying raw production customer data into test databases.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides principles and patterns for generating, maintaining, and cleaning up realistic, isolated test data without relying on fragile production database dumps.

---

### Scope
- **In-Scope**:
  - Designing deterministic data factories and fixture builders\n  - Ensuring complete test data isolation between parallel test workers\n  - Synthesizing realistic mock datasets (addresses, emails, phone numbers)\n  - Masking and anonymizing sensitive data (PII, tokens, financial details)
- **Out-of-Scope**:
  - Production database replication and live backup orchestration

---

### When to Use
- Creating test setups for integration, E2E, or performance test suites\n- Cleaning up brittle test fixtures that cause intermittent test failures\n- Sanitizing staging database environments

---

### When Not to Use
- For trivial unit tests that require only simple primitive values

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
### 8.1 The Factory Pattern for Test Data
- Avoid hardcoding shared JSON fixtures with fixed IDs (e.g. `user-1.json`). Shared fixtures create hidden dependencies between tests.
- Use **Dynamic Data Factories** that generate fresh, isolated entities with sensible defaults and unique identifiers (e.g. `user-${Date.now()}-${random()}@example.com`).
- Allow individual tests to override specific fields relevant to their test assertion:
```typescript
const admin = buildUser({ role: 'admin', isActive: true });
const suspended = buildUser({ isActive: false });
```

### 8.2 PII & Production Data Masking Rules
- **NEVER import unmasked production customer data into development or test environments.**
- All customer PII must be masked:
  - Names -> Synthetic randomized names (e.g. John Doe, Jane Smith).
  - Emails -> `user-xxxx@example.com` or `@test.internal`.
  - Passwords -> Pre-hashed standard test passwords.
  - Payment Cards -> Standard test card numbers (e.g. `4242 4242 4242 4242`).

---

### Step-by-Step Workflow
1. **Step 1: Identify Required Entities & Relationships**
   - Map dependencies (e.g. Order requires User and Product).
2. **Step 2: Implement Data Factories**
   - Author factory functions with deterministic defaults and random seeds.
3. **Step 3: Implement Lifecycle Hooks (Setup & Teardown)**
   - Setup transaction rollbacks or `beforeEach`/`afterEach` cleanup logic.
4. **Step 4: Verify Parallel Isolation**
   - Run tests concurrently across multiple workers; verify zero data collisions.
5. **Step 5: Document Fixtures**
   - Document factory usage patterns in `docs_agent/testing/TEST_STRATEGY.md`.

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
