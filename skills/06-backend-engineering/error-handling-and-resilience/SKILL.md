---
name: error-handling-and-resilience
description: Design robust error taxonomies, graceful degradation, circuit breakers, retry strategies, and fault tolerance across backend services.
version: 2.0.0
category: backend-engineering
tags: [error-handling, resilience, circuit-breaker, retries, fault-tolerance, backend]
---

# Skill: Backend Error Handling & System Resilience

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 06-backend-engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `error-handling-and-resilience`
- **Category**: 06-backend-engineering
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Design robust error taxonomies, graceful degradation, circuit breakers, retry strategies, and fault tolerance across backend services.
- **When to Use**: Designing error responses, implementing distributed client calls, handling external API failures, or configuring timeouts.
- **Essential Invariants**:
  1. Distinguish operational errors (transient network, 4xx/5xx) from programmer errors (bugs, panics) with structured error types.
  2. Outbound network requests must always have explicit timeout, retry with jitter, and circuit breaker policies.
  3. Never leak internal implementation details, database queries, or raw stack traces to external API consumers.
- **Minimal Workflow**:
  1. Define centralized application error hierarchy with machine-readable codes and HTTP status mappings.
  2. Wrap external network integrations with exponential backoff retries and circuit breakers.
  3. Implement global error middleware to log diagnostics internally while returning safe client errors.
  4. Test failure modes using fault injection, timeout simulations, and boundary test cases.
- **Expected Deliverables**: Structured error taxonomy, fault-tolerant network clients, and resilience verification tests.
- **Critical Restrictions**: Prohibit bare empty catch blocks that swallow errors; never make unbounded network calls without timeouts.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Design robust error taxonomies, graceful degradation, circuit breakers, retry strategies, and fault tolerance across backend services.

### Execution Procedures
1. **Preparation**: Review task scope, prerequisites, and verify project state. If governance files (TASKS.md, CONTEXT.md) are absent, create them from the bootstrap template or record the evidence inline.
2. **Implementation**: Execute the procedures according to the Level 1 Minimal Workflow while upholding all Essential Invariants.
3. **Verification**: Verify outputs empirically with exit codes, static linters, and regression checks.

### Edge Cases & Failure Recovery
- **Ambiguous Constraints**: Halt and trigger human-in-the-loop escalation rather than making unverified assumptions.
- **Execution Failures**: Record failure evidence, isolate root cause, and formulate targeted remediation within bounded iterations.

---

## Level 3 — Optional References & Supplementary Assets

### Level 3 Index
- None (all core procedures codified in Level 1 & Level 2).
