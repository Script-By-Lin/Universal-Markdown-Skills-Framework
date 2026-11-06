---
name: observability-and-logging
description: Implement structured JSON logging, distributed tracing (OpenTelemetry), metrics instrumentation, and alerting thresholds.
version: 2.0.0
category: reliability-and-operations
tags: [observability, logging, opentelemetry, tracing, metrics, prometheus]
---

# Skill: Observability, Telemetry & Structured Logging

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 11-reliability-and-operations  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `observability-and-logging`
- **Category**: 11-reliability-and-operations
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Implement structured JSON logging, distributed tracing (OpenTelemetry), metrics instrumentation, and alerting thresholds.
- **When to Use**: Adding telemetry to microservices, diagnosing production errors, tracking service latencies, or defining SLO/SLA alerts.
- **Essential Invariants**:
  1. Production logs must be emitted in structured JSON format with consistent timestamps, levels, and correlation/trace IDs.
  2. Distributed requests must propagate correlation IDs across all service boundaries.
  3. High-cardinality telemetry must be managed to avoid memory bloat and metrics storage exhaustion.
- **Minimal Workflow**:
  1. Configure structured logger with context enrichment (service name, environment, git commit).
  2. Implement distributed tracing context middleware to inject and propagate traceparent headers.
  3. Expose standard RED (Rate, Errors, Duration) metrics endpoints for Prometheus scraping.
  4. Define actionable alert thresholds tied directly to user-impacting SLOs.
- **Expected Deliverables**: Structured logging setup, distributed trace context propagator, and instrumented metrics endpoints.
- **Critical Restrictions**: Never log plaintext credentials, session tokens, or sensitive PII; avoid unbounded unindexed log spam.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Implement structured JSON logging, distributed tracing (OpenTelemetry), metrics instrumentation, and alerting thresholds.

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
