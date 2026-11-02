---
name: system-testing
description: "Holistic verification of the fully assembled application system, verifying end-to-end business workflows, configuration integrity, and environment parity."
version: 1.0.0
category: quality
tags: ['testing', 'system-testing', 'e2e', 'configuration', 'environment-parity']
---

# Skill: System Testing

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.
> Category: Domain 09 — Quality Assurance & Testing

---

## 1. Metadata
- **Identifier**: `system-testing`
- **Category**: Quality Assurance & Testing (Domain 09)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
Evaluates the complete, integrated software product against high-level business specifications and operational requirements in an environment closely mirroring production.

---

## 3. Scope
- **In-Scope**:
  - Testing multi-step business workflows spanning multiple subsystems\n  - Verifying environment variable configuration and startup readiness\n  - Testing database migrations, seeders, and health-check probes\n  - Validating logging, error handling, and recovery under subsystem outages
- **Out-of-Scope**:
  - Fine-grained unit testing of single methods

---

## 4. When to Use
- Validating pre-release candidate builds in staging environments\n- Conducting smoke tests after major infrastructure or deployment changes\n- Verifying end-to-end transaction lifecycles

---

## 5. When Not to Use
- During initial rapid TDD micro-cycles (use unit and integration tests)

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
### 8.1 System Test Principles
- **Black-Box Perspective**: Test the system through its public entry points (UI, REST APIs, CLI commands) without inspecting internal object states.
- **Environment Parity**: Run against identical operating systems, database engines, and runtime configurations as production.
- **Configuration Verification**: Ensure the application validates required environment variables at boot and fails fast if credentials or connection strings are missing.
- **Resilience Testing**: Test how the system behaves when dependent services (cache, email service) are unavailable—verify graceful error responses, not unhandled crashes.

---

## 9. Step-by-Step Workflow
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
