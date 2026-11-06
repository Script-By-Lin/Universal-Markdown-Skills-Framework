---
name: performance
description: Profiling methodologies, latency optimization, memory leak mitigation, algorithmic efficiency, and frontend bundle budgets.
version: 1.7.0
category: quality
tags: [performance, profiling, latency, memory, optimization, bundle-size, caching]
---

# Skill: Application Performance Optimization

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 13 — Performance Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `performance`
- **Category**: Performance Engineering (Domain 13)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Profile, analyze, and optimize application CPU usage, memory allocation, database queries, and I/O bottlenecks.
- **When to Use**: Investigating slow endpoints, reducing memory footprint, eliminating N+1 queries, or tuning event loops.
- **Essential Invariants**:
  1. Measure before and after; never optimize based on assumptions without profiling data.
  2. Optimizations must NOT break code correctness or readability without documented justification.
  3. Verify zero behavioral regressions with comprehensive test suite runs.
- **Minimal Workflow**:
  1. Profile application under realistic workload to identify hot paths (CPU, memory, I/O).
  2. Formulate optimization hypothesis and implement targeted code/query refactoring.
  3. Re-profile to measure latency and throughput improvements against baseline.
  4. Re-run test suite to confirm 100% test pass rate and zero functional regressions.
- **Expected Deliverables**: Profiling benchmark report demonstrating quantified latency or resource reductions.
- **Critical Restrictions**: Never apply premature optimizations that sacrifice code maintainability without empirical profiling data.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes empirical, measurement-driven methodologies for diagnosing latency bottlenecks, reducing computational complexity, preventing memory leaks, optimizing database access, and enforcing frontend bundle size budgets.

---

### Scope
- **In-Scope**:
  - Profiling execution bottlenecks (CPU, memory, I/O, network).
  - Algorithmic optimization (reducing $O(n^2)$ loops to $O(n \log n)$ or $O(n)$).
  - Database query latency tuning (indexing, batching, caching).
  - Frontend performance (lazy loading, Cumulative Layout Shift &lt; 0.1, bundle minimization).
- **Out-of-Scope**:
  - Initial feature functional implementation (delegate to [`skills/backend-development/SKILL.md`](../../backend-development/SKILL.md)).
  - Routine bug troubleshooting without performance symptoms (delegate to [`skills/debugging/SKILL.md`](../../debugging/SKILL.md)).

---

### When to Use
- When response latency exceeds acceptable thresholds (e.g. API endpoint P95 &gt; 200ms).
- When frontend pages exhibit sluggish frame rates or low Core Web Vitals scores.
- When memory usage scales unsustainably with load.

---

### When Not to Use
- Premature optimization before code correctness and test coverage are established.
- For micro-optimizations that sacrifice code readability without measurable gains.

---

### Prerequisites
- Measurable performance baseline established through profiling or benchmarking.
- Reproducible benchmark environment available.

---

### Required Context
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- Performance history recorded in [`MEMORY.md`](../../../MEMORY.md).

---

### Core Instructions
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

### Step-by-Step Workflow
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

### Quality Standards
- **Measurable Improvement**: Optimization yields at least a 20% measurable reduction in execution time or memory footprint.
- **Readability Preservation**: Code remains maintainable, well-commented, and standard-compliant.
- **Zero Regression**: 100% of functional tests continue to pass.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Latency Benchmark | Automated benchmark runner | P95 latency reduced compared to baseline |
| Memory Profile | Heap allocation trace | Zero unbounded memory accumulation over iterations |
| Test Suite | Full test runner execution | 100% test pass rate with zero behavioral changes |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Premature Optimization | Complicates code before identifying actual bottlenecks | Establish working baseline first; profile before optimizing |
| Breaking Tests for Speed | Renders software fast but broken | Performance optimizations must maintain 100% functional equivalence |

---

### Restrictions
- Do NOT commit optimizations that have not been validated against a measurable baseline.
- Do NOT sacrifice security protections (input validation, rate limiting) for performance.

---

### Expected Deliverables
- Optimized source code files.
- Benchmark comparison report (Baseline vs. Optimized metrics).

---

### Documentation Requirements
- Record performance benchmarks and caching conventions in [`MEMORY.md`](../../../MEMORY.md).
- Update [`TASKS.md`](../../../TASKS.md) with optimization results.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
