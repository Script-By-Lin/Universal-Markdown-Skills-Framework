---
name: performance
description: Profiling methodologies, latency optimization, memory leak mitigation, algorithmic efficiency, and frontend bundle budgets.
version: 1.0.0
category: quality
tags: [performance, profiling, latency, memory, optimization, bundle-size, caching]
---

# Skill: Performance Engineering & Optimization

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `performance`
- **Category**: Quality & Optimization
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes empirical, measurement-driven methodologies for diagnosing latency bottlenecks, reducing computational complexity, preventing memory leaks, optimizing database access, and enforcing frontend bundle size budgets.

---

## 3. Scope
- **In-Scope**:
  - Profiling execution bottlenecks (CPU, memory, I/O, network).
  - Algorithmic optimization (reducing $O(n^2)$ loops to $O(n \log n)$ or $O(n)$).
  - Database query latency tuning (indexing, batching, caching).
  - Frontend performance (lazy loading, Cumulative Layout Shift &lt; 0.1, bundle minimization).
- **Out-of-Scope**:
  - Initial feature functional implementation (delegate to [`skills/backend-development/SKILL.md`](../backend-development/SKILL.md)).
  - Routine bug troubleshooting without performance symptoms (delegate to [`skills/debugging/SKILL.md`](../debugging/SKILL.md)).

---

## 4. When to Use
- When response latency exceeds acceptable thresholds (e.g. API endpoint P95 &gt; 200ms).
- When frontend pages exhibit sluggish frame rates or low Core Web Vitals scores.
- When memory usage scales unsustainably with load.

---

## 5. When Not to Use
- Premature optimization before code correctness and test coverage are established.
- For micro-optimizations that sacrifice code readability without measurable gains.

---

## 6. Prerequisites
- Measurable performance baseline established through profiling or benchmarking.
- Reproducible benchmark environment available.

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- Performance history recorded in [`MEMORY.md`](../../MEMORY.md).

---

## 8. Core Instructions
1. **Measure First, Optimize Second (Mandatory Invariant)**:
   - Never optimize based on intuition alone. Always capture baseline measurements before changing code, and compare post-optimization benchmarks against that baseline.
2. **Algorithmic Efficiency over Micro-Tuning**:
   - Prefer changing data structures (e.g., using a Hash Set for $O(1)$ lookups instead of scanning an array in $O(n)$) over tweaking micro-syntax.
3. **Minimize I/O & Network Round-Trips**:
   - In-memory computation is orders of magnitude faster than disk or network access. Batch database reads/writes and cache expensive, idempotent queries.
4. **UI Performance Heuristics (UI/UX Pro Max)**:
   - Reserve container dimensions to keep Cumulative Layout Shift (CLS) under 0.1.
   - Use modern image formats (WebP, AVIF) with lazy-loading attributes (`loading="lazy"`).
   - Animate exclusively via GPU-composited properties (`transform`, `opacity`). Never animate `top`, `left`, `width`, or `height`.

---

## 9. Step-by-Step Workflow
1. **Step 1: Benchmark Baseline Capture**
   - Execute benchmark under controlled conditions. Record metrics: P50, P95, P99 latency, memory allocations, CPU utilization.
2. **Step 2: Profile to Identify Hotspots**
   - Use profilers (flame graphs, query analyzers, Lighthouse) to identify the specific lines or queries consuming &gt; 80% of resources.
3. **Step 3: Hypothesize & Apply Optimization**
   - Apply targeted structural or algorithmic optimization (e.g. index addition, caching, data structure replacement).
4. **Step 5: Post-Optimization Benchmark Verification**
   - Run benchmark under identical conditions. Verify that latency or memory improved significantly.
5. **Step 6: Verify Functional Correctness**
   - Run the automated test suite to ensure the optimization introduced zero regressions.

---

## 10. Quality Standards
- **Measurable Improvement**: Optimization yields at least a 20% measurable reduction in execution time or memory footprint.
- **Readability Preservation**: Code remains maintainable, well-commented, and standard-compliant.
- **Zero Regression**: 100% of functional tests continue to pass.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Latency Benchmark | Automated benchmark runner | P95 latency reduced compared to baseline |
| Memory Profile | Heap allocation trace | Zero unbounded memory accumulation over iterations |
| Test Suite | Full test runner execution | 100% test pass rate with zero behavioral changes |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Premature Optimization | Complicates code before identifying actual bottlenecks | Establish working baseline first; profile before optimizing |
| Breaking Tests for Speed | Renders software fast but broken | Performance optimizations must maintain 100% functional equivalence |

---

## 13. Restrictions
- Do NOT commit optimizations that have not been validated against a measurable baseline.
- Do NOT sacrifice security protections (input validation, rate limiting) for performance.

---

## 14. Expected Deliverables
- Optimized source code files.
- Benchmark comparison report (Baseline vs. Optimized metrics).

---

## 15. Documentation Requirements
- Record performance benchmarks and caching conventions in [`MEMORY.md`](../../MEMORY.md).
- Update [`TASKS.md`](../../TASKS.md) with optimization results.

