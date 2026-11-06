---
name: unit-testing
description: "Isolation testing of individual functions, methods, and classes using deterministic mocks, clear boundary isolation, and the AAA pattern."
version: 1.7.0
category: quality
tags: ['testing', 'unit-testing', 'mocks', 'stubs', 'isolation', 'aaa-pattern']
---

# Skill: Unit Testing & Component Verification

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `unit-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Author fast, isolated unit tests verifying individual functions, classes, and components in isolation from external systems.
- **When to Use**: Verifying pure business logic, utility functions, algorithms, and isolated UI components.
- **Essential Invariants**:
  1. Unit tests must execute in memory without filesystem, network, or external database calls.
  2. Each unit test must verify a single behavior or invariant.
  3. Unit test execution time must remain under a few milliseconds per test.
- **Minimal Workflow**:
  1. Identify boundaries and dependencies of unit under test.
  2. Mock or stub external I/O dependencies using test doubles.
  3. Assert expected return values and side effects across valid and boundary inputs.
  4. Execute unit test suite and verify 100% pass rate.
- **Expected Deliverables**: Comprehensive unit test suite executing with exit code 0.
- **Critical Restrictions**: Never introduce external network or database dependencies into pure unit tests.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Provides principles and patterns for writing fast, deterministic, isolated unit tests that verify business domain logic without external environmental dependencies.

---

### Scope
- **In-Scope**:
  - Applying the Arrange-Act-Assert (AAA) pattern\n  - Isolating units under test from databases, networks, and file systems\n  - Designing deterministic test doubles (mocks, stubs, fakes, spies)\n  - Testing pure functions, state transitions, and boundary values
- **Out-of-Scope**:
  - Multi-component integration testing with live databases (delegate to `skills/09-quality-assurance-and-testing/integration-testing/SKILL.md`)

---

### When to Use
- Writing unit tests for domain services, utility functions, or calculation engines\n- Testing class methods, state machines, and data validation logic

---

### When Not to Use
- For end-to-end browser journeys or database query verification

---

### Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in `TASKS.md`.

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in `RULES.md` (TDD invariants & Release Gates).
- Testing environment in `CONTEXT.md`.
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

### Core Instructions
### 8.1 The Arrange-Act-Assert (AAA) Standard
Every unit test must be structured into three distinct blocks:
```typescript
it('calculates discount correctly for premium subscribers', () => {
  // 1. Arrange: Setup inputs and dependencies
  const user = createTestUser({ tier: 'premium' });
  const cart = createTestCart({ total: 100 });
  const service = new PricingService();

  // 2. Act: Execute single behavior under test
  const finalPrice = service.calculateTotal(user, cart);

  // 3. Assert: Verify outcome unambiguously
  expect(finalPrice).toBe(80);
});
```

### 8.2 Test Double Guidelines
- **Use Stubs** for indirect inputs (providing predetermined return values).
- **Use Mocks** sparingly for indirect outputs (verifying an email dispatcher or payment gateway was called with exact parameters).
- **Never mock what you do not own**: Wrap third-party libraries in thin domain adapters and mock the adapter.

---

### Step-by-Step Workflow
1. **Step 1: Identify Unit Boundary & Collaborators**
   - Isolate the class or function under test. Identify external collaborator interfaces.
2. **Step 2: Setup Test Doubles & Fixtures**
   - Provide minimal mock objects for network/DB dependencies.
3. **Step 3: Author AAA Test Cases**
   - Implement test cases covering standard operation, null inputs, and error throws.
4. **Step 4: Execute & Verify Fast Feedback**
   - Run tests; ensure execution completes in under 50ms per test.
5. **Step 5: Review Coverage**
   - Verify branch and statement coverage for the unit.

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
- Record testing conventions and discovered edge cases in `MEMORY.md`.
- Record testing architectural trade-offs in `DECISIONS.md`.
- Update task tracking in `TASKS.md` and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
