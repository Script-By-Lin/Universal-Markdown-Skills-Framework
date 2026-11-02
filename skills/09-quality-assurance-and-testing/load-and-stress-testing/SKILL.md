---
name: load-and-stress-testing
description: "Concurrency testing, load curves, stress thresholds, breaking-point determination, and graceful degradation verification."
version: 1.0.0
category: quality
tags: ['testing', 'load-testing', 'stress-testing', 'concurrency', 'capacity', 'scalability']
---

# Skill: Load And Stress Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `load-and-stress-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Evaluates how application systems perform under sustained high concurrent user load and determines breaking points and failure recovery behaviors.

---

## 3. Scope
- **In-Scope**:
  - Designing load profiles (baseline load, peak load, spike load, soak test)\n  - Measuring system throughput (requests per second) under concurrent threads\n  - Determining system breaking points and memory leak saturation\n  - Verifying graceful degradation (rate limiting, queue backpressure)
- **Out-of-Scope**:
  - Uncontrolled distributed DoS testing on production infrastructure

---

## 4. When to Use
- Preparing for high-traffic marketing events, product launches, or flash sales\n- Capacity planning and horizontal/vertical infrastructure scaling analysis\n- Verifying database connection pool limits under heavy concurrency

---

## 5. When Not to Use
- On unmonitored development instances sharing production databases

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
### 8.1 Load Test Profiles
- **Load Test**: Assess performance under expected normal and peak traffic over sustained periods.
- **Stress Test**: Incrementally increase concurrency beyond peak capacity until the system breaks; observe failure mode.
- **Spike Test**: Rapidly surge traffic from 0 to 5x peak within seconds; observe rate limiting and queue behavior.
- **Soak Test**: Run moderate traffic for 4-12 hours to detect slow memory leaks or unclosed connection handles.

### 8.2 Graceful Degradation Invariants
When stressed beyond maximum capacity, the system must:
1. Return HTTP 429 Too Many Requests or HTTP 503 Service Unavailable cleanly.
2. Never crash the host process or corrupt database records.
3. Recover automatically within 60 seconds once traffic returns to normal levels.

---

## 9. Step-by-Step Workflow
1. **Step 1: Test Plan & Authorization Boundary**
   - Verify isolated staging target; confirm zero impact on live customer traffic.
2. **Step 2: Script Concurrent User Scenarios**
   - Author load script simulating realistic user behaviors (e.g. k6, Locust, autocannon).
3. **Step 3: Execute Ramp-Up Load Curve**
   - Gradually ramp virtual users from 10 to 500 over 10 minutes.
4. **Step 4: Monitor System Vital Signs**
   - Track CPU, memory, database connection pool, and error rates.
5. **Step 5: Compile Capacity Report**
   - Record maximum sustainable RPS and bottleneck analysis in `docs_agent/testing/TEST_RESULTS.md`.

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
