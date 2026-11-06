# Advanced Regression Testing Techniques (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `regression-testing`  
> Domain: 09 — Quality Assurance & Testing  

---

## 1. Overview
Advanced techniques for enterprise and distributed systems regression testing: Mutation Testing as Regression Quality Gate, Property-Based Regression, and Differential Testing.

---

## 2. Property-Based Regression Testing
- Use hypothesis engines (e.g. `hypothesis` for Python, `fast-check` for TypeScript/JavaScript, `gopter` for Go).
- Define invariants that must hold true across tens of thousands of pseudorandomly generated inputs.
- Automatically shrinks failing inputs to minimal counterexamples for permanent regression test suites.

---

## 3. Differential Regression Testing
- Run identical input workloads against two distinct system versions:
  - Version N (current stable production baseline).
  - Version N+1 (candidate build with refactored internals).
- Intercept and compare output payloads, HTTP status codes, latency histograms, and database side effects.
- Flag any discrepancies for review before production traffic migration.

