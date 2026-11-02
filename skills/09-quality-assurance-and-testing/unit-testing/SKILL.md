---
name: unit-testing
description: "Isolation testing of individual functions, methods, and classes using deterministic mocks, clear boundary isolation, and the AAA pattern."
version: 1.0.0
category: quality
tags: ['testing', 'unit-testing', 'mocks', 'stubs', 'isolation', 'aaa-pattern']
---

# Skill: Unit Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `unit-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Provides principles and patterns for writing fast, deterministic, isolated unit tests that verify business domain logic without external environmental dependencies.

---

## 3. Scope
- **In-Scope**:
  - Applying the Arrange-Act-Assert (AAA) pattern\n  - Isolating units under test from databases, networks, and file systems\n  - Designing deterministic test doubles (mocks, stubs, fakes, spies)\n  - Testing pure functions, state transitions, and boundary values
- **Out-of-Scope**:
  - Multi-component integration testing with live databases (delegate to `skills/09-quality-assurance-and-testing/integration-testing/SKILL.md`)

---

## 4. When to Use
- Writing unit tests for domain services, utility functions, or calculation engines\n- Testing class methods, state machines, and data validation logic

---

## 5. When Not to Use
- For end-to-end browser journeys or database query verification

---

## 6. Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in [`TASKS.md`](../../../TASKS.md).

---

## 7. Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (TDD invariants & Release Gates).
- Testing environment in [`CONTEXT.md`](../../../CONTEXT.md).
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

## 8. Core Instructions
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

## 9. Step-by-Step Workflow
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

## 10. Quality Standards
- **Standard 1**: 100% adherence to the mandatory TDD Red-Green-Refactor protocol.
- **Standard 2**: All tests must run deterministically with zero flakiness.
- **Standard 3**: Absolute prohibition on claiming tests passed without verifying execution exit code 0.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Test Execution | Automated test runner execution | 100% passing tests; exit code 0 |
| Regression Safety | Full regression suite execution | Zero regressions in existing capabilities |
| Coverage Integrity | Coverage instrumentation | Branch coverage meets agreed project threshold |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Writing Tests After Implementation | High susceptibility to confirmation bias | Follow TDD: write failing test first (RED phase) |
| Hardcoded Sleeps | Causes flaky, brittle, and slow test runs | Wait explicitly for state or DOM conditions |
| Shared Mutable Test Data | Tests fail unpredictably when run in parallel | Use isolated data factories and per-test cleanups |

---

## 13. Restrictions
- Do NOT modify tests merely to force incorrect implementation code to pass.
- Do NOT delete failing tests without documented architectural authorization.
- Do NOT bypass Functional or Regression Release Gates.

---

## 14. Expected Deliverables
- Automated test suites (unit, integration, or E2E).
- Updated testing logs in `docs_agent/testing/TDD_LOG.md` or `TEST_RESULTS.md`.
- Regression verification report.

---

## 15. Documentation Requirements
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Record testing architectural trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).
