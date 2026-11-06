---
name: system-testing
description: "Holistic verification of the fully assembled application system, verifying end-to-end business workflows, configuration integrity, and environment parity."
version: 1.7.0
category: quality
tags: ['testing', 'system-testing', 'e2e', 'configuration', 'environment-parity']
---

# Skill: System Testing & End-to-End Environment Validation

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 09 — Quality Assurance & Testing  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `system-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Validate the completely integrated software system against original functional and non-functional specifications.
- **When to Use**: Pre-release validation, staging environment qualification, or major system integration milestones.
- **Essential Invariants**:
  1. System tests must execute against a fully assembled, production-like build artifact.
  2. Verify complete end-to-end workflows from client input to background persistence.
  3. All system test environments must have synchronized schema and dependency versions.
- **Minimal Workflow**:
  1. Deploy candidate release artifact to isolated staging environment.
  2. Execute end-to-end system test scenarios covering primary business user flows.
  3. Inspect system telemetry (logs, metrics, error rates) during test execution.
  4. Verify all system acceptance gates pass with exit code 0.
- **Expected Deliverables**: System test verification report confirming complete end-to-end functionality.
- **Critical Restrictions**: Never declare system testing complete if downstream integrations were mocked or bypassed.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Evaluates the complete, integrated software product against high-level business specifications and operational requirements in an environment closely mirroring production.

---

### Scope
- **In-Scope**:
  - Testing multi-step business workflows spanning multiple subsystems\n  - Verifying environment variable configuration and startup readiness\n  - Testing database migrations, seeders, and health-check probes\n  - Validating logging, error handling, and recovery under subsystem outages
- **Out-of-Scope**:
  - Fine-grained unit testing of single methods

---

### When to Use
- Validating pre-release candidate builds in staging environments\n- Conducting smoke tests after major infrastructure or deployment changes\n- Verifying end-to-end transaction lifecycles

---

### When Not to Use
- During initial rapid TDD micro-cycles (use unit and integration tests)

---

### Prerequisites
- Target code components, interfaces, and architecture verified.
- Project testing frameworks and dependencies inspected from repository.
- Task registered and tracked in [`TASKS.md`](../../../TASKS.md).

---

### Required Context
Before executing this skill, verify:
- Mandatory constraints in [`RULES.md`](../../../RULES.md) (TDD invariants & Release Gates).
- Testing environment in [`CONTEXT.md`](../../../CONTEXT.md).
- Active test strategies in [`docs_agent/testing/TEST_STRATEGY.md`](../../../templates/TEST_STRATEGY.template.md) (if present).

---

### Core Instructions
### 8.1 System Test Principles
- **Black-Box Perspective**: Test the system through its public entry points (UI, REST APIs, CLI commands) without inspecting internal object states.
- **Environment Parity**: Run against identical operating systems, database engines, and runtime configurations as production.
- **Configuration Verification**: Ensure the application validates required environment variables at boot and fails fast if credentials or connection strings are missing.
- **Resilience Testing**: Test how the system behaves when dependent services (cache, email service) are unavailable—verify graceful error responses, not unhandled crashes.

---

### Step-by-Step Workflow
1. **Step 1: System Boot & Health Check Verification**
   - Deploy or boot application in staging. Query `/health` or readiness probe.
2. **Step 2: Execute Core Business Journey**
   - Execute user registration -> email confirmation -> product checkout -> receipt generation.
3. **Step 3: Inspect Logs & Telemetry**
   - Confirm structured logs are produced with zero unhandled exceptions.
4. **Step 4: Verify Asynchronous Jobs**
   - Confirm background workers process queued jobs and deliver expected outputs.
5. **Step 5: Signoff System Readiness**
   - Record pass/fail status in `docs_agent/testing/TEST_RESULTS.md`.

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
- Record testing conventions and discovered edge cases in [`MEMORY.md`](../../../MEMORY.md).
- Record testing architectural trade-offs in [`DECISIONS.md`](../../../DECISIONS.md).
- Update task tracking in [`TASKS.md`](../../../TASKS.md) and session log in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
