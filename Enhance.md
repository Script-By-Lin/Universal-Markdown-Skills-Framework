## EXPANDED UNIVERSAL SOFTWARE ENGINEERING SKILLS LIBRARY

The framework must deliver a comprehensive Software Engineering Skills Library covering the entire Software Development Lifecycle (SDLC).

Create and organize skills across these 16 engineering domains:

1. Software Development Lifecycle.
2. Security Engineering.
3. Software Architecture and Design.
4. Requirements and Business Analysis.
5. Programming and Implementation.
6. Backend Engineering.
7. Frontend Engineering.
8. Database Engineering.
9. Quality Assurance and Testing.
10. DevOps and Infrastructure.
11. Reliability and Operations.
12. Code Quality and Maintenance.
13. Performance Engineering.
14. Project and Team Management.
15. Documentation and Technical Communication.
16. AI Agent Engineering.

Each domain must contain individually reusable SKILL.md documents.

Requirements:

- Cover the full SDLC, from requirements to maintenance.
- Include secure software development practices throughout the lifecycle.
- Include OWASP-oriented security engineering and threat modeling.
- Include architecture, design, implementation, testing, deployment and operations.
- Include functional and non-functional quality requirements.
- Include practical workflows, checklists, validation criteria and expected deliverables.
- Make skills language-independent wherever possible.
- Avoid duplicate or overlapping responsibilities.
- Maintain a central SKILLS.md registry.
- Load skills based on task relevance rather than loading every skill automatically.
- Use supporting Markdown reference files only when necessary.
- Keep all skills provider-independent and locally reusable.

Do not create superficial placeholder skills. Every published skill must provide actionable instructions, a clear scope, a practical workflow and measurable validation criteria.

Treat security, quality, documentation and maintainability as cross-cutting engineering requirements.

Organize the skills into numbered domain directories under skills/ and maintain their inventory in SKILLS.md.

# UMSF — Master Enhancement Prompt
## Advanced Testing, Test-Driven Development & AI Security Engineering

### Role

Act as a Principal Software Architect, Senior QA Engineer, Security Architect, Penetration Tester, AI Agent Systems Architect, and Technical Documentation Engineer.

You are enhancing the existing Universal Markdown Skills Framework (UMSF).

Your responsibility is to integrate a comprehensive software testing and security engineering system into the existing framework without compromising its universal, local-first, Markdown-only architecture.

---

# 1. Project Context

UMSF is a universal, reusable Markdown-based instruction and skills framework for AI coding agents.

Supported agents include:

- OpenAI Codex
- Claude Code
- Cursor
- Windsurf
- Gemini CLI
- Antigravity
- GitHub Copilot
- Other compatible AI coding agents

Architectural decisions:

- Project scope: Universal platform.
- Execution model: Hybrid.
- Distribution: Both reusable framework repository and copied project-level framework.
- Canonical instruction format: Markdown.
- Local-first operation.
- Zero external dependencies.
- No framework CLI, application, runtime, database, or service.
- AI agents themselves execute the workflows by reading and following Markdown instructions.
- Skills are discovered and selectively loaded according to the task.
- All actual user-project development records belong inside the user's project-level `/docs_agent/` directory.

Do not introduce dependencies, programming runtimes, external services, or mandatory third-party tools.

External security standards may be referenced as guidance, but the framework itself must remain dependency-free.

# 2. Enhancement Objectives

Integrate the following capabilities:

1. Test-Driven Development (TDD).
2. Comprehensive Software Testing Lifecycle.
3. Independent AI Quality Assurance Agent.
4. Independent AI Security Testing Agent.
5. AI-driven penetration testing.
6. Vulnerability assessment and management.
7. Adversarial testing.
8. Automated regression verification.
9. Security remediation and retesting.
10. Release quality and security gates.
11. Testing context and knowledge preservation.
12. Comprehensive testing and security documentation.

These capabilities must become part of the existing UMSF operating instructions, workflows, and skills library.

Do not simply create superficial skill descriptions. Every skill must contain actionable instructions.

# 3. Test-Driven Development Architecture

Implement TDD as the preferred development approach for testable application features.

Use the following mandatory Red-Green-Refactor cycle.

## RED — Write Tests First

Before implementing a feature:

1. Understand the requirements.
2. Identify expected behavior.
3. Define acceptance criteria.
4. Identify positive, negative, boundary, and edge cases.
5. Write automated tests.
6. Execute the tests.
7. Confirm that the new tests fail for the expected reason.

The agent must distinguish an expected test failure from a broken test environment or unrelated failure.

## GREEN — Implement the Feature

1. Implement the minimum code necessary.
2. Execute the relevant tests.
3. Confirm the expected tests pass.
4. Avoid unrelated implementation changes.
5. Preserve existing functionality.

## REFACTOR — Improve the Implementation

1. Improve code structure.
2. Remove unnecessary duplication.
3. Improve maintainability.
4. Review architecture and security implications.
5. Run the complete relevant test suite.
6. Confirm no regression.

Repeat the cycle for subsequent requirements.

### TDD Rules

- Do not write tests merely to match an existing implementation.
- Do not modify tests just to make incorrect implementation pass.
- Do not delete failing tests without justified approval.
- Do not claim tests passed without actually executing them.
- Record exceptions when TDD is impractical, such as exploratory prototypes, legacy characterization, or infrastructure constraints.
- Existing test suites must be preserved.

# 4. Complete Software Testing Lifecycle

Create a comprehensive testing methodology.

Include:

### Functional Testing
- Requirement verification.
- Business logic verification.
- Input and output validation.
- Positive and negative scenarios.
- Boundary testing.

### Unit Testing
- Individual function testing.
- Method testing.
- Component isolation.
- Mocking and stubbing where appropriate.

### Integration Testing
- Database integration.
- API integration.
- External service boundaries.
- Authentication integration.
- Cross-module communication.

### System Testing
- Complete application behavior.
- End-to-end business workflows.
- Configuration verification.

### Regression Testing
- Existing functionality.
- Previously fixed bugs.
- Critical business workflows.
- Regression suites.

### Additional Testing
- Acceptance testing.
- Exploratory testing.
- Smoke testing.
- Compatibility testing.
- Usability testing.
- Accessibility testing.
- Performance testing.
- Load testing.
- Stress testing.
- Reliability testing.
- Recovery testing.
- Mutation testing where supported.

The agent must select relevant testing techniques according to the project, risk, architecture, and available environment.

Do not require every testing type for every project.

# 5. Independent AI Agent Testing Architecture

Introduce a multi-agent quality and security workflow.

Define three logical agent roles.

## Agent A — Development Agent

Responsibilities:

- Analyze requirements.
- Design architecture.
- Implement features.
- Follow TDD.
- Maintain code quality.
- Run developer tests.
- Fix implementation defects.
- Update project documentation.

The development agent must not declare its own work independently security-approved.

## Agent B — Independent QA Agent

Responsibilities:

- Review requirements and acceptance criteria.
- Inspect implementation and test coverage.
- Identify missing test cases.
- Execute relevant tests independently.
- Test functional behavior.
- Identify regressions.
- Challenge incorrect assumptions.
- Verify bug fixes.
- Report test results.

The QA agent must not automatically trust the development agent's claims.

It must independently inspect available evidence.

## Agent C — Independent Security Agent

Responsibilities:

- Review application architecture.
- Perform threat modeling.
- Inspect authentication and authorization.
- Examine application and API security.
- Identify vulnerabilities.
- Perform authorized security testing.
- Attempt controlled exploitation where appropriate.
- Verify security fixes.
- Conduct regression security testing.
- Produce security assessment reports.

The security agent must approach the application from an adversarial perspective.

### Multi-Agent Execution

Support two execution modes:

**Mode 1 — Multi-Agent**

When the coding environment supports multiple agents, assign independent QA and security roles.

**Mode 2 — Single-Agent**

When multiple agents are unavailable, the same AI agent must switch into separate QA and security-review roles after completing development.

It must use fresh review passes, separate checklists, and independently verify evidence rather than simply repeating its implementation reasoning.

Never assume that all AI coding agents support native multi-agent execution.

# 6. Security Engineering & Penetration Testing

Establish security testing as a mandatory risk-based engineering activity.

Include the following coverage.

## Authentication Security

- Authentication bypass.
- Password handling.
- Session management.
- Token security.
- JWT validation.
- Session expiration.
- Account enumeration.
- Brute-force protection.
- Multi-factor authentication where applicable.

## Authorization Security

- Broken access control.
- IDOR.
- RBAC bypass.
- Privilege escalation.
- Horizontal privilege escalation.
- Vertical privilege escalation.
- Tenant isolation.
- Resource ownership verification.

## Injection Security

- SQL injection.
- NoSQL injection.
- Command injection.
- Template injection.
- LDAP injection where applicable.
- Unsafe deserialization.

## Web Application Security

- Stored XSS.
- Reflected XSS.
- DOM-based XSS.
- CSRF.
- SSRF.
- Path traversal.
- File upload vulnerabilities.
- Open redirects.
- Security misconfiguration.

## API Security

- Broken object-level authorization.
- Broken function-level authorization.
- Excessive data exposure.
- Improper input validation.
- Rate-limit weaknesses.
- Authentication weaknesses.
- API inventory and version exposure.
- Insecure error handling.

## Database Security

- Unauthorized access.
- Privilege misconfiguration.
- SQL injection.
- Sensitive data exposure.
- Weak backup protection.
- Insecure database configuration.

## Infrastructure Security

- Exposed secrets.
- Insecure environment variables.
- Weak deployment configuration.
- Network exposure.
- Insecure container configuration.
- TLS configuration weaknesses.
- File permission weaknesses.

## Cryptographic Security

- Weak password hashing.
- Insecure encryption.
- Hardcoded cryptographic keys.
- Weak random number generation.
- Improper secret management.
- Incorrect cryptographic implementation.

## Dependency Security

- Known vulnerable dependencies.
- Unmaintained dependencies.
- Dependency confusion risks.
- Supply-chain risks.
- Unnecessary dependencies.

Use relevant and current security guidance such as:

- OWASP Top 10.
- OWASP ASVS.
- OWASP API Security Top 10.
- CWE.
- NIST Secure Software Development Framework.
- Relevant security testing standards.

Record the version or publication date of references when practical. Do not assume an older checklist remains current.

# 7. Authorized Penetration Testing Rules

The security agent must operate within an explicit authorization boundary.

Before active security testing:

1. Identify the target application and environment.
2. Establish that the user owns the system or has authorized testing.
3. Identify permitted endpoints and resources.
4. Define prohibited targets and actions.
5. Determine whether test data and backups are available.
6. Establish the permitted testing intensity.

Default to local development, staging, or dedicated test environments.

The security agent must:

- Prefer non-destructive testing.
- Use controlled proof-of-concept demonstrations.
- Avoid unnecessary data access.
- Never exfiltrate sensitive information.
- Never destroy or modify production data.
- Never perform uncontrolled denial-of-service testing.
- Never attack unrelated third-party systems.
- Stop when testing exceeds authorization boundaries.
- Request explicit authorization before intrusive or potentially disruptive tests.

If authorization is missing, perform passive review and code/configuration analysis only.

The security agent must distinguish between:

- Confirmed vulnerability.
- Reproducible security weakness.
- Potential vulnerability.
- Informational observation.
- False positive.
- Not tested.

Do not invent successful exploitation.

# 8. Vulnerability Management Lifecycle

Implement this lifecycle:

Discovery
    ↓
Classification
    ↓
Risk Assessment
    ↓
Evidence Collection
    ↓
Reproduction
    ↓
Remediation Recommendation
    ↓
Development Agent Fix
    ↓
Independent Retest
    ↓
Regression Security Testing
    ↓
Closure or Documented Risk Acceptance

Use a risk classification system:

- Critical
- High
- Medium
- Low
- Informational

Consider exploitability, impact, exposure, affected assets, and business context.

CVSS may be used as supporting evidence where appropriate, but must not replace contextual risk assessment.

Every confirmed vulnerability must contain:

- Unique vulnerability ID.
- Title.
- Affected component.
- Description.
- Severity.
- Evidence.
- Reproduction steps.
- Impact.
- Recommended remediation.
- Status.
- Assigned responsibility.
- Retest result.
- Closure date where applicable.

# 9. Quality and Security Release Gates

Define quality gates before production release.

A release must satisfy applicable requirements:

### Functional Gate
- Acceptance criteria verified.
- Required tests passed.
- Critical business workflows validated.

### Regression Gate
- Relevant existing tests passed.
- Previously fixed defects remain fixed.

### Security Gate
- Security review completed according to risk.
- Critical and high-risk confirmed vulnerabilities resolved or formally accepted through an authorized, documented exception.
- Security retests completed.
- No unreviewed security findings hidden or ignored.

### Documentation Gate
- Implementation status updated.
- Test results documented.
- Vulnerability register updated.
- Release decisions documented.

The agent must not falsely mark a release as approved when a mandatory gate remains incomplete.

# 10. Universal Skills Library Enhancement

Preserve the existing 16 UMSF skill categories.

Enhance the following categories.

## Category 02 — Security Engineering

Add:

- security-testing
- penetration-testing
- web-application-security
- api-security-testing
- vulnerability-assessment
- security-code-review
- threat-modeling
- dependency-security-audit
- authentication-security
- authorization-security
- vulnerability-management
- security-remediation-and-retesting

## Category 09 — Quality Assurance & Testing

Add:

- test-driven-development
- unit-testing
- integration-testing
- system-testing
- end-to-end-testing
- regression-testing
- acceptance-testing
- exploratory-testing
- test-automation
- test-coverage-analysis
- mutation-testing
- performance-testing
- load-and-stress-testing
- test-strategy-and-planning
- test-data-management
- defect-management

## Category 16 — AI Agent Engineering

Add:

- independent-qa-agent
- independent-security-review-agent
- multi-agent-verification
- adversarial-testing
- agent-handoff-and-review
- evidence-based-validation
- agent-role-separation

Each skill must have a dedicated SKILL.md and actionable instructions.

Avoid duplicating the same full instructions across skills. Use cross-references and selective loading.

# 11. Skill Discovery and Loading

Update SKILLS.md and AGENTS.md.

The agent must:

1. Read the skill registry.
2. Identify skills relevant to the current task.
3. Load required skills before implementation or testing.
4. Load dependent skills when necessary.
5. Apply cross-cutting security and quality rules.
6. Avoid loading unrelated skills.
7. Record important missing capabilities.
8. Never pretend a skill was loaded when it was not.

Support explicit user requests to load a particular skill.

Implement progressive discovery and selective skill loading.

# 12. Project Documentation

All actual project development and verification records must be stored in the user's project root:

`/docs_agent/`

Important:

The `/docs_agent/` folder must initially be empty.

UMSF must not populate it with fictional reports, sample test results, fake development history, or pre-created project-specific reports.

The coding agent creates documentation files only when corresponding activities actually happen.

Suggested structure as the project evolves:

docs_agent/
├── testing/
│   ├── TEST_STRATEGY.md
│   ├── TDD_LOG.md
│   ├── TEST_RESULTS.md
│   ├── REGRESSION_REPORT.md
│   ├── COVERAGE_REPORT.md
│   └── QA_ASSESSMENT.md
│
├── security/
│   ├── SECURITY_TEST_PLAN.md
│   ├── THREAT_MODEL.md
│   ├── SECURITY_ASSESSMENT.md
│   ├── VULNERABILITY_REGISTER.md
│   ├── PENETRATION_TEST_REPORT.md
│   └── RETEST_REPORT.md
│
├── ARCHITECTURE.md
├── IMPLEMENTATION_STATUS.md
├── DEVELOPMENT_LOG.md
├── CHANGE_HISTORY.md
├── PHASE_HISTORY.md
└── SESSION_LOG.md

Create only the files needed by the actual project.

### Reporting Rules

Every meaningful testing activity must record:

- Objective.
- Scope.
- Environment.
- Test methodology.
- Actual tests executed.
- Expected result.
- Actual result.
- Pass/fail status.
- Evidence.
- Identified issues.
- Remediation.
- Remaining risks.
- Next actions.

Security reports must never include actual passwords, private keys, access tokens, or other secrets.

Do not expose sensitive vulnerability details unnecessarily in public project documentation.

Preserve historical records and update current status separately.

# 13. Context and Memory Integration

Integrate testing and security knowledge with existing UMSF context management.

CONTEXT.md must describe the current verified testing architecture, testing tools already available in the project, and security status.

MEMORY.md may preserve reusable discoveries, lessons, testing conventions, and security pitfalls.

TASKS.md must track:

- Missing tests.
- Failing tests.
- Unresolved defects.
- Open vulnerabilities.
- Security remediation.
- Pending retests.
- Deferred testing.

DECISIONS.md must record important testing architecture and security decisions.

Never treat historical test results as proof that the current code is safe.

# 14. Existing Project Integration

When UMSF is copied into an existing or empty user project:

- Inspect the actual project before making assumptions.
- Detect the existing programming language and framework.
- Discover the current test infrastructure.
- Preserve existing testing configurations.
- Do not replace working test frameworks without justification.
- Use tools already installed whenever possible.
- Do not introduce dependencies without user authorization.
- If a suitable testing capability is unavailable, explain the limitation and provide a manual verification alternative.
- Do not invent test commands or successful results.

The framework must also support empty projects where the testing architecture is established as development begins.

# 15. Implementation Requirements

Enhance the existing UMSF files rather than rebuilding the framework.

Inspect first:

- AGENTS.md
- SKILLS.md
- RULES.md
- WORKFLOW.md
- Existing skill directories.
- Existing templates.
- Existing documentation.
- Existing phase implementation status.

Preserve existing architecture and decisions unless an actual conflict is identified.

Update all relevant cross-references.

Do not create duplicate skill files or duplicate rules.

Do not modify unrelated functionality.

Do not create fake test reports in the UMSF repository that imply an actual user's application was tested.

# 16. Validation and Acceptance Criteria

Before declaring the enhancement complete, verify:

1. TDD workflow is documented and actionable.
2. Red-Green-Refactor is clearly defined.
3. Testing lifecycle covers appropriate testing levels.
4. Independent QA role is defined.
5. Independent security role is defined.
6. Single-agent fallback is defined.
7. Penetration testing authorization rules exist.
8. Security testing covers relevant application and infrastructure risks.
9. Vulnerability classification and lifecycle exist.
10. Fix verification and security retesting are defined.
11. Release gates are documented.
12. Testing and security skills are registered.
13. Skill cross-references are valid.
14. Agent discovery instructions are updated.
15. Project documentation rules are updated.
16. Empty `/docs_agent/` initialization is preserved.
17. Zero-dependency architecture remains intact.
18. Existing UMSF functionality is preserved.

For every criterion, report PASS, FAIL, or NOT VERIFIED with evidence.

Do not claim real-world security validation unless an actual authorized assessment was performed.

# 17. Mandatory Development Documentation

After this enhancement, update the UMSF repository's own development records under its `/docs_agent/` folder, following its existing documentation policy.

Record:

- Enhancement objectives.
- Architectural changes.
- New and modified skills.
- Updated instruction files.
- Testing methodology.
- Security architecture.
- Validation evidence.
- Unresolved issues.
- Decisions.
- Next steps.

Do not confuse UMSF repository development records with the documentation generated later inside a user's own project.

# 18. Execution Instructions

Work incrementally.

1. Inspect the existing UMSF repository.
2. Identify current implementation and missing capabilities.
3. Prepare an enhancement plan.
4. Update architecture and instructions.
5. Implement TDD and QA skills.
6. Implement security and penetration-testing skills.
7. Integrate multi-agent and single-agent workflows.
8. Update skill registry and cross-references.
9. Update templates and documentation requirements.
10. Validate the complete enhancement.
11. Produce an accurate implementation report.

Do not stop after writing a plan. Implement the enhancement within the existing repository.

Do not automatically start unrelated future phases or rewrite the entire framework.

Do not fabricate tests, results, files, or completed work.

---

# FINAL EXPECTED RESULT

UMSF should become a universal AI-driven Software Engineering framework in which:

- Development follows disciplined engineering workflows.
- TDD is the preferred approach for testable features.
- QA independently verifies application functionality.
- Security agents challenge the implementation adversarially.
- Authorized penetration testing identifies real security weaknesses.
- Vulnerabilities are tracked, fixed, and independently retested.
- Regression testing protects existing functionality.
- Release decisions are based on verifiable evidence.
- Every meaningful project activity is documented in the user's `/docs_agent/`.
- Skills are reusable across compatible AI coding agents.
- The entire framework remains local-first, Markdown-only, provider-independent, and zero-dependency.

**Begin by inspecting the existing UMSF repository, then implement this enhancement without destroying or unnecessarily restructuring existing work.**