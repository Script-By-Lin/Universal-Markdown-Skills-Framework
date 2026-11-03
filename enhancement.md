# UMSF Enhancement — Independent Verification Subagent Architecture

Repository:
https://github.com/Script-By-Lin/Universal-Markdown-Skills-Framework

## Objective

Enhance the existing Universal Markdown Skills Framework (UMSF) by implementing an Independent Verification Subagent architecture.

The primary development agent must not be the only agent responsible for determining whether its implementation is correct.

After the primary development agent completes a meaningful development task, a separate verification subagent must independently inspect, analyse, test, and evaluate the complete implementation.

Preserve the existing UMSF architecture, 16 engineering domains, Markdown-only philosophy, provider independence, and existing skills.

Do not rebuild the framework from scratch.

## Phase 1 — Inspect Existing Architecture

Inspect:

- AGENTS.md
- RULES.md
- SKILLS.md
- WORKFLOW.md
- CONTEXT.md
- DECISIONS.md
- Existing multi-agent skills.
- Existing agent role separation.
- Existing independent QA skills.
- Existing security verification skills.
- Existing evidence-based validation skills.
- Existing post-task verification capabilities.

Identify existing functionality that can be reused.

Do not create duplicate skills or conflicting role definitions.

## Phase 2 — Create Independent Verification Subagent Skill

Create:

skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md

Use the established UMSF 15-section skill structure.

Define the subagent's purpose, activation conditions, inputs, workflow, responsibilities, restrictions, deliverables, and validation criteria.

## Phase 3 — Define Agent Responsibilities

### Agent A — Primary Development Agent

Responsible for:

1. Understanding the original user request.
2. Extracting requirements and acceptance criteria.
3. Planning implementation.
4. Selecting relevant skills.
5. Following TDD where applicable.
6. Implementing the requested changes.
7. Running initial tests.
8. Recording files changed.
9. Preparing a structured handoff for Agent B.

Agent A must not claim independent verification.

### Agent B — Independent Verification Subagent

Agent B must independently evaluate everything Agent A implemented.

Required inputs:

- Original user prompt.
- Acceptance criteria.
- Initial project context.
- Actual repository state.
- Git diff or equivalent change inventory.
- Agent A implementation report.
- Relevant test instructions.

Agent B must perform:

#### A. Requirements Audit
- Re-read the original prompt.
- Extract all explicit requirements.
- Compare each requirement against actual implementation.
- Identify missing, incomplete, incorrect, or unnecessary functionality.

#### B. Complete Change Inspection
- Inspect every created file.
- Inspect every modified file.
- Inspect every deleted file.
- Inspect renamed and moved files.
- Check unintended changes.
- Check secrets and sensitive data exposure.

#### C. Architecture Audit
- Check architectural consistency.
- Inspect dependency boundaries.
- Check interfaces and data flow.
- Inspect error handling.
- Identify unnecessary complexity and coupling.
- Check existing decisions and framework rules.

#### D. Code Quality Audit
- Inspect maintainability.
- Identify duplicated code.
- Identify incorrect patterns.
- Inspect edge cases.
- Review type safety and validation.
- Examine performance where relevant.

#### E. Independent Testing
- Independently determine which tests are necessary.
- Execute relevant available tests.
- Inspect actual command output and exit status.
- Verify expected and actual results.
- Identify missing tests.
- Check regressions.
- Do not simply trust Agent A's test report.

#### F. Security Review
- Inspect security-sensitive changes.
- Identify relevant vulnerabilities and weaknesses.
- Coordinate with the existing Security Agent when appropriate.
- Do not perform unauthorized active penetration testing.

#### G. Documentation Audit
- Verify documentation against actual implementation.
- Identify outdated instructions.
- Verify internal paths and references.
- Check that reported completion matches actual work.

## Phase 4 — Finding and Defect Management

Every finding must include:

- Finding ID.
- Title.
- Severity.
- Affected file or component.
- Description.
- Evidence.
- Reproduction steps where applicable.
- Expected behavior.
- Actual behavior.
- Recommended remediation.
- Verification status.

Use these finding categories:

- Critical
- High
- Medium
- Low
- Informational
- False Positive
- Not Tested

Distinguish confirmed defects from potential concerns.

## Phase 5 — Remediation and Retesting

After Agent B identifies findings:

1. Return actionable findings to Agent A.
2. Agent A corrects valid findings within the original authorization.
3. Agent A reports additional changes.
4. Agent B independently inspects the corrections.
5. Agent B reruns affected tests.
6. Agent B checks for new regressions.
7. Repeat as necessary within reasonable task scope.

Set a configurable verification iteration limit to prevent endless agent loops.

If findings remain unresolved after the permitted iterations, report them honestly. Never silently approve incomplete work.

## Phase 6 — Integration With Security Agent

Reuse the existing independent-security-review-agent.

Agent C should be involved when the change has meaningful security implications.

Define clear boundaries:

- Agent B: General implementation, requirements, quality, testing, and regression verification.
- Agent C: Security-specific analysis and authorized security testing.

Agent B must not claim a penetration test was performed merely because it reviewed the code.

## Phase 7 — Multi-Agent and Fallback Modes

Support:

### Mode A — Independent Subagents

When the environment supports real independent subagents:

- Agent A implements.
- Agent B independently verifies.
- Agent C reviews relevant security concerns.
- Findings are returned to Agent A.
- Verification agents retest corrections.

Use actual separate agent execution and handoff mechanisms.

### Mode B — Sequential Verification

When real subagents are unavailable:

- Complete Agent A's implementation first.
- Switch to a separate verification role.
- Re-read the original request.
- Use fresh verification checklists.
- Inspect actual files and execute tests independently.
- Record that verification was sequential self-review, not independent subagent execution.

Never pretend that separate roles in one agent are separate agents.

## Phase 8 — Final Acceptance Decision

Define three possible outcomes:

### VERIFIED

Applicable acceptance criteria passed, relevant independent checks were completed, and no unresolved blocking findings remain.

### NEEDS REMEDIATION

Valid findings remain and require further work.

### BLOCKED / NOT VERIFIED

Required tools, environment, permissions, or test evidence are unavailable, or unresolved critical issues prevent acceptance.

A successful compilation alone is not sufficient for VERIFIED status.

Agent B provides a verification assessment. Final user-facing completion reporting must accurately distinguish development completion from independent verification approval.

## Phase 9 — Mandatory Framework Integration

Update where appropriate:

- AGENTS.md
- RULES.md
- WORKFLOW.md
- SKILLS.md
- Existing multi-agent verification skills.
- Existing independent QA skills.
- Existing post-task verification skill.

Make the verification handoff mandatory for meaningful development tasks.

Keep detailed procedures inside the dedicated skill.

Avoid duplicating large blocks of instructions across framework files.

## Phase 10 — Documentation

Create or update actual development records under UMSF's own docs_agent/ directory.

For consuming projects, preserve the existing rule that their docs_agent/ directory starts empty and grows only as meaningful work happens.

Record:

- Agent A implementation handoff.
- Agent B findings.
- Agent C security findings when applicable.
- Remediation history.
- Retest evidence.
- Final verification decision.

Do not create fake reports or claim unperformed tests.

Never include credentials or secrets in reports.

## Phase 11 — Validation

Before completing this enhancement:

1. Verify the new skill exists.
2. Verify SKILLS.md registration.
3. Verify all referenced paths.
4. Check for duplicate responsibilities.
5. Check role separation.
6. Verify the subagent workflow and sequential fallback.
7. Verify finding and remediation lifecycle.
8. Verify iteration limits.
9. Check instruction precedence consistency.
10. Inspect the complete Git diff.
11. Validate Markdown and internal links.
12. Confirm no external runtime, application, CLI, database, API, or mandatory dependency has been introduced.

## Final Report

Report:

- New files.
- Modified files.
- Agent architecture.
- Subagent handoff design.
- Independent testing capabilities.
- Security coordination.
- Fallback behavior.
- Actual validation results.
- Remaining limitations.
- Final acceptance status.

Stop after this enhancement. Do not automatically begin another development phase.