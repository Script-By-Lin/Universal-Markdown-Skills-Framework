---
name: performance-testing
description: "Benchmarking, latency profiling, throughput measurement, and bottleneck identification across API endpoints and UI render pipelines."
version: 1.0.0
category: quality
tags: ['testing', 'performance', 'latency', 'benchmarks', 'throughput', 'cls']
---

# Skill: Performance Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `performance-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Measures, benchmarks, and optimizes the speed, latency, and resource efficiency of software components to ensure they meet agreed performance budgets.

---

## 3. Scope
- **In-Scope**:
  - Measuring response time percentiles (p50, p95, p99)\n  - Benchmarking database query execution times and identifying unindexed scans\n  - Measuring frontend Core Web Vitals (LCP < 2.5s, CLS < 0.1, INP < 200ms)\n  - Profiling memory allocations and algorithmic time complexity
- **Out-of-Scope**:
  - Massive distributed load testing with thousands of simulated nodes

---

## 4. When to Use
- Validating performance SLAs for new API endpoints or database queries\n- Conducting UI responsiveness audits on complex views\n- Tuning algorithmic bottlenecks and caching layers

---

## 5. When Not to Use
- For non-performance-critical internal background cleanup scripts

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
### 8.1 Performance Budget Thresholds
Enforce strict performance budgets across the stack:
- **API Response Latency**:
  - Read endpoints (p95): **< 200ms**
  - Write endpoints (p95): **< 500ms**
- **Database Query Time**:
  - Any single query (p95): **< 20ms** (zero unindexed sequential table scans on tables > 1,000 rows).
- **Frontend Core Web Vitals**:
  - **LCP** (Largest Contentful Paint): **< 2.5s**
  - **CLS** (Cumulative Layout Shift): **< 0.1** (reserve image/widget dimensions)
  - **INP** (Interaction to Next Paint): **< 200ms**

---

## 9. Step-by-Step Workflow
1. **Step 1: Establish Performance Baseline & SLA**
   - Define expected request volume, concurrency, and maximum acceptable latency.
2. **Step 2: Profile Local & Staging Endpoints**
   - Execute benchmark script measuring response time distribution over 100+ requests.
3. **Step 3: Identify Bottlenecks via Tracing**
   - Isolate time spent in database, network serialization, and CPU processing.
4. **Step 4: Optimize & Re-benchmark**
   - Add database index, introduce caching, or optimize algorithm. Re-run benchmark.
5. **Step 5: Document Results**
   - Record before/after latency comparisons in `docs_agent/testing/TEST_RESULTS.md`.

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
