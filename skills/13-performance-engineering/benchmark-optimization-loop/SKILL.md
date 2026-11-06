---
name: benchmark-optimization-loop
description: Convert 'make it faster' requests into a bounded measured optimization loop — baseline first, generate one-hypothesis variants, benchmark each against a correctness gate, and promote the fastest safe variant with reproducible commands. Use when asked to speed something up, try many variants, run recursive optimization, benchmark latency/throughput/cost, or pick the best implementation by repeated measured tests.
license: MIT
metadata:
  origin: ECC
tools: Read, Write, Edit, Bash, Grep, Glob
version: 1.7.0
---

# Skill: Benchmark Optimization Loop

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 13 — Performance Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `benchmark-optimization-loop`
- **Category**: Performance Engineering (Domain 13)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Execute bounded, measured optimization loops: establish baseline, generate variants, benchmark, and promote the fastest safe code.
- **When to Use**: Optimizing critical algorithmic routines, mathematical kernels, parsers, or serialization loops.
- **Essential Invariants**:
  1. Establish reproducible baseline benchmark with statistically significant sample sizes.
  2. Every variant must pass the exact same correctness test gate before performance evaluation.
  3. Promote only variants that demonstrate statistically significant speedup without regressions.
- **Minimal Workflow**:
  1. Author automated benchmark script measuring iterations/sec and memory allocations.
  2. Run baseline to establish current performance floor (mean, std dev).
  3. Generate one-hypothesis code variants targeting specific algorithmic bottlenecks.
  4. Run correctness test gate and benchmark across variants; promote the fastest safe variant.
- **Expected Deliverables**: Benchmark comparison table and promoted high-performance code implementation.
- **Critical Restrictions**: Never promote a faster variant that fails any correctness or edge-case test.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

Use this skill to convert "make it 20x faster" or "try 50 recursive
optimizations" into a bounded measured loop that can actually improve a system.

### Required Baseline

Do not optimize until these exist:

- the operation being optimized;
- the correctness gate that must stay green;
- the metric: wall time, p95 latency, rows/sec, cost/run, memory, error rate;
- the current baseline;
- the search budget: max variants, max time, max spend, max data impact.

If the user asks for an unrealistic target, keep the ambition but make the loop
bounded and measurable.

### Loop

1. Measure the baseline.
2. Identify bottlenecks from evidence.
3. Generate variants that test one hypothesis each.
4. Run variants with the same input shape.
5. Reject variants that fail correctness, safety, or reproducibility.
6. Promote the fastest safe variant.
7. Codify the winning path in a script, command, test, config, or doc.
8. Rerun the baseline and winner to confirm the delta.

### Variant Table

Track variants like this:

```text
Variant | Hypothesis | Command | Time | Correct? | Notes
baseline | current path | npm run job | 120s | yes | stable
batch-500 | fewer round trips | npm run job -- --batch 500 | 42s | yes | winner
parallel-8 | more workers | npm run job -- --workers 8 | 31s | no | rate limited
```

### Recursive Search

For recursive or hyperparameter work:

- persist every run to a ledger;
- compare against the prior accepted winner, not only the previous run;
- keep a holdout or replay check;
- stop when improvement is within noise, correctness fails, cost exceeds the
  budget, or the search starts changing more variables than it can explain.

Use phrases like "best measured safe variant" instead of "global optimum" unless
the search space was actually exhaustive.

### Promotion Gate

A variant cannot become the new default until:

- correctness tests pass;
- the performance delta is repeated or explained;
- rollback is obvious;
- the change is encoded in source control or a durable runbook;
- the final summary includes exact commands and measurements.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
