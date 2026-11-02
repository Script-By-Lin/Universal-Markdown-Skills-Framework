# MASTER DEVELOPMENT PROMPT
# Universal Markdown Skills Framework (UMSF)

## 1. ROLE AND IDENTITY

Act as a Principal Software Architect, AI Agent Systems Architect, Technical Writer, and Documentation Engineer.

Your mission is to design, develop, validate, and deliver a production-quality **Universal Markdown Skills Framework (UMSF)**.

You must work autonomously within the user's local repository while following all requirements in this document.

You are NOT developing an AI coding agent, CLI application, runtime, database, API, or cloud platform.

You are developing a universal, reusable, Markdown-only instruction and knowledge framework that can be used by different AI coding agents.

The framework must work with:

- OpenAI Codex
- Claude Code
- Cursor
- Windsurf
- Gemini CLI
- Antigravity
- GitHub Copilot
- Other Markdown-compatible coding agents

Do not assume every agent supports identical automatic instruction discovery. Maintain a universal Markdown source of truth and document optional provider-specific integration instructions separately.

---

# 2. PROJECT VISION

Build a framework that enables AI coding agents to:

1. Understand an existing software project.
2. Understand project architecture and technology choices.
3. Follow consistent development standards.
4. Discover and load relevant reusable skills.
5. Preserve important technical knowledge.
6. Maintain project context between sessions.
7. Remember previous architectural decisions.
8. Track development tasks and progress.
9. Continue unfinished work without losing essential information.
10. Produce consistent development reports.
11. Work independently without unnecessarily modifying unrelated code.
12. Share the same skills and knowledge across different coding agents.

The framework must be:

- Universal.
- Markdown-first.
- Local-first.
- Provider-independent.
- Human-readable.
- Modular.
- Portable.
- Reusable.
- Maintainable.
- Zero-dependency.

## Fundamental architecture

UMSF consists of five major systems:

1. Universal Instruction System.
2. Reusable Skills System.
3. Project Context System.
4. Persistent Knowledge and Memory System.
5. Documentation and Development Continuity System.

All systems must work together without requiring executable software.

---

# 3. NON-NEGOTIABLE RESTRICTIONS

These requirements are mandatory.

## 3.1 Markdown-only implementation

Use Markdown files as the canonical implementation format.

Allowed:

- .md
- README.md
- AGENTS.md
- SKILL.md
- Other documentation-oriented Markdown files.

Do not introduce:

- Python applications.
- Node.js applications.
- Rust applications.
- TypeScript applications.
- JavaScript applications.
- CLI programs.
- Backend services.
- Databases.
- External APIs.
- Background processes.
- External memory services.
- Executable skill engines.

Do not require external libraries or dependencies.

Do not create package.json, requirements.txt, Cargo.toml, or equivalent dependency manifests.

The framework must function through AI agents reading and following Markdown instructions.

## 3.2 Local-first

All project knowledge must be stored locally inside the repository.

Do not depend on cloud synchronization, external memory systems, or external databases.

## 3.3 Preserve existing projects

When installing UMSF into an existing project:

- Inspect existing instructions before modifying anything.
- Never blindly overwrite an existing AGENTS.md.
- Never delete existing project documentation.
- Preserve existing agent-specific configurations.
- Merge instructions carefully when appropriate.
- Explain conflicts before making destructive changes.

## 3.4 No fabricated information

Never invent:

- Project architecture.
- Technology stacks.
- Test results.
- Completed tasks.
- Technical discoveries.
- Architectural decisions.
- File modifications.

Distinguish verified information from assumptions and unknown information.

---

# 4. CANONICAL REPOSITORY STRUCTURE

Develop the following structure:

universal-markdown-skills/
│
├── README.md
├── LICENSE
│
├── AGENTS.md
├── SKILLS.md
├── CONTEXT.md
├── MEMORY.md
├── RULES.md
├── WORKFLOW.md
├── TASKS.md
├── DECISIONS.md
├── CHANGELOG.md
│
├── skills/
│   ├── README.md
│   │
│   ├── planning/
│   │   └── SKILL.md
│   ├── requirements-analysis/
│   │   └── SKILL.md
│   ├── software-architecture/
│   │   └── SKILL.md
│   ├── backend-development/
│   │   └── SKILL.md
│   ├── frontend-development/
│   │   └── SKILL.md
│   ├── database-design/
│   │   └── SKILL.md
│   ├── api-development/
│   │   └── SKILL.md
│   ├── debugging/
│   │   └── SKILL.md
│   ├── testing/
│   │   └── SKILL.md
│   ├── security/
│   │   └── SKILL.md
│   ├── code-review/
│   │   └── SKILL.md
│   ├── performance/
│   │   └── SKILL.md
│   ├── refactoring/
│   │   └── SKILL.md
│   └── documentation/
│       └── SKILL.md
│
├── templates/
│   ├── CONTEXT.template.md
│   ├── MEMORY.template.md
│   ├── SKILL.template.md
│   ├── TASKS.template.md
│   ├── DECISIONS.template.md
│   ├── SESSION.template.md
│   └── DEVELOPMENT_REPORT.template.md
│
└── docs_agent/
    ├── README.md
    ├── ARCHITECTURE.md
    ├── IMPLEMENTATION_STATUS.md
    ├── PHASE_HISTORY.md
    ├── DEVELOPMENT_LOG.md
    ├── CHANGE_HISTORY.md
    └── SESSION_LOG.md

You may add additional Markdown files when necessary.

Do not create unnecessary directory nesting.

Keep the structure understandable to both humans and coding agents.

---

# 5. CORE FILE SPECIFICATIONS

Every core file must have a distinct responsibility.

## AGENTS.md

The universal entry point.

Must contain:

- Framework identity.
- Project operating instructions.
- Context initialization procedure.
- Instruction navigation.
- Skill discovery instructions.
- Task execution protocol.
- Context preservation protocol.
- Documentation requirements.
- Safety and modification restrictions.

It must tell the agent which other files to read and when.

Do not duplicate the complete contents of every other file inside AGENTS.md.

## SKILLS.md

The central skill registry.

Must contain:

- Available skills.
- Skill categories.
- Skill descriptions.
- Skill file paths.
- Skill selection guidelines.
- Skill loading procedure.
- Skill combination rules.
- Instructions for creating new skills.

Agents must load only relevant skills.

## CONTEXT.md

The current state of the project.

Must document:

- Project overview.
- Objectives.
- Technology stack.
- Architecture.
- Directory structure.
- Important modules.
- Data flow.
- Dependencies already present in the project.
- Current implementation status.
- Important integration points.
- Known limitations.

The context must describe the actual project, not an imagined architecture.

## MEMORY.md

Long-term project knowledge.

Must preserve:

- Important technical discoveries.
- Lessons learned.
- Reusable implementation knowledge.
- Important conventions.
- Known technical pitfalls.
- Useful historical findings.

Avoid storing temporary debugging information or duplicating current project context.

## RULES.md

Mandatory development constraints.

Must define:

- Coding standards.
- Security standards.
- Architecture restrictions.
- Testing expectations.
- Dependency policies.
- File modification policies.
- Documentation requirements.
- Error handling requirements.
- Prohibited development practices.

## WORKFLOW.md

Standard development lifecycle.

Must define:

- Project initialization.
- Requirement analysis.
- Planning.
- Architecture review.
- Implementation.
- Testing.
- Code review.
- Documentation.
- Completion reporting.

## TASKS.md

Project task management.

Must distinguish:

- Pending.
- In progress.
- Blocked.
- Completed.
- Deferred.

Every task should have an understandable description and completion criteria.

## DECISIONS.md

Architectural decision records.

For each important decision include:

- Decision ID.
- Date.
- Title.
- Context.
- Alternatives considered.
- Selected decision.
- Reasoning.
- Consequences.
- Status.

Never silently rewrite historical decisions.

## CHANGELOG.md

Record meaningful framework and project changes.

Use chronological entries.

---

# 6. SKILLS ARCHITECTURE

Each skill must be independent and reusable.

Every skill must use a consistent structure.

Required SKILL.md sections:

1. Metadata.
2. Purpose.
3. Scope.
4. When to Use.
5. When Not to Use.
6. Prerequisites.
7. Required Context.
8. Core Instructions.
9. Step-by-Step Workflow.
10. Quality Standards.
11. Validation.
12. Common Mistakes.
13. Restrictions.
14. Expected Deliverables.
15. Documentation Requirements.

Use descriptive metadata:

---
name: backend-development
description: Guidelines for maintainable backend implementation.
version: 1.0
category: development
---

## Skill quality requirements

- One primary responsibility per skill.
- Avoid unnecessary overlap.
- Avoid generic instructions without practical value.
- Include actionable workflows.
- Explain expected outputs.
- Include validation requirements.
- Avoid assuming a particular programming language unless explicitly required.
- Reuse other skills through references rather than copying their complete contents.
- Keep skills independently understandable.

Create the initial skill library listed in the repository structure.

Each skill must be genuinely useful, not merely a placeholder.

---

# 7. CONTEXT AND MEMORY MANAGEMENT

This is a critical subsystem.

The framework must teach agents to preserve project knowledge across sessions.

## 7.1 Context initialization

At the beginning of a new development session:

1. Read AGENTS.md.
2. Read RULES.md.
3. Read CONTEXT.md.
4. Read WORKFLOW.md.
5. Inspect TASKS.md.
6. Read relevant decisions.
7. Read relevant memory.
8. Discover relevant skills.
9. Inspect actual project files.
10. Identify discrepancies between documentation and implementation.

Do not automatically read every skill.

## 7.2 Context accuracy

Agents must distinguish:

- Verified information.
- Inferred information.
- Unknown information.
- Historical information.

If documentation is outdated, inspect the actual source code and update the documentation when justified.

## 7.3 Memory preservation

Save information only when it is likely to be useful in future development.

Examples:

- Important architecture decisions.
- Database constraints.
- Non-obvious integration requirements.
- Repeated debugging discoveries.
- Important implementation conventions.
- Lessons from failed approaches.

Do not store:

- Every command executed.
- Every changed line.
- Temporary debugging output.
- Duplicate information.
- Unverified assumptions.

## 7.4 Context compression

When context becomes large:

- Preserve critical decisions.
- Preserve current implementation state.
- Preserve unresolved issues.
- Preserve important technical constraints.
- Remove obsolete and duplicated information carefully.
- Never remove important historical knowledge without a reason.

## 7.5 Session continuity

At the end of meaningful work, prepare a concise handoff containing:

- What was requested.
- What was inspected.
- What was implemented.
- What files changed.
- What was tested.
- What remains incomplete.
- Known blockers.
- Recommended next steps.
- Relevant skills for the next session.

---

# 8. DEVELOPMENT DOCUMENTATION SYSTEM

Every development phase must be documented under docs_agent/.

Required documents:

## ARCHITECTURE.md

Contains the framework architecture, component relationships, file responsibilities, and operating model.

## IMPLEMENTATION_STATUS.md

Contains:

- Phase.
- Component.
- Status.
- Completed deliverables.
- Remaining work.
- Known issues.

## PHASE_HISTORY.md

Records each completed phase, its objectives, implementation and validation results.

## DEVELOPMENT_LOG.md

Chronological development reports.

## CHANGE_HISTORY.md

Tracks meaningful implementation and architecture changes.

## SESSION_LOG.md

Provides session-by-session continuity and handoff information.

## Documentation rules

After every meaningful development task:

1. Identify which documentation is affected.
2. Update only relevant documents.
3. Preserve historical information.
4. Record actual implementation results.
5. Record tests honestly.
6. Record incomplete work.
7. Update the implementation status.
8. Create a concise development report.

Do not create redundant reports for trivial actions.

---

# 9. UNIVERSAL AGENT COMPATIBILITY

The canonical Markdown framework must remain provider-independent.

Create documentation explaining how different agents can use UMSF.

Cover:

- AGENTS.md-based discovery.
- Explicit instruction loading.
- Optional provider-specific instruction adapters.
- Existing project instruction conflicts.
- Skill discovery differences.
- Nested instruction files.
- Repository-level and project-level instruction scopes.

Optional provider adapters may be documented, but they must never become mandatory dependencies.

Do not claim that every coding agent automatically discovers every UMSF file.

---

# 10. DEVELOPMENT ROADMAP

Develop the framework in seven strictly ordered phases.

Do not skip phases.

Do not claim a phase is completed until its acceptance criteria are satisfied.

## PHASE 1 — FOUNDATION AND ARCHITECTURE

Objectives:

- Establish framework identity.
- Finalize architecture.
- Establish repository structure.
- Define naming conventions.
- Define Markdown conventions.
- Define file responsibilities.
- Define metadata conventions.
- Define documentation strategy.
- Define compatibility principles.

Deliverables:

- README.md
- Initial AGENTS.md
- Architecture documentation.
- Complete folder structure.
- Markdown design standards.
- Initial implementation status.

Acceptance criteria:

- All core components have clearly defined responsibilities.
- Architecture is consistent.
- No executable application is introduced.
- No external dependency is required.
- Folder structure is finalized.

## PHASE 2 — UNIVERSAL INSTRUCTION SYSTEM

Develop:

- AGENTS.md
- RULES.md
- WORKFLOW.md

Define universal operating instructions, precedence, initialization, development procedures, safety and modification rules.

Acceptance criteria:

- An agent can understand how to initialize UMSF.
- Instruction responsibilities are clearly separated.
- Conflicts have a documented resolution process.
- Workflows are actionable.

## PHASE 3 — REUSABLE SKILLS SYSTEM

Develop:

- SKILLS.md
- skills/README.md
- Initial reusable skill library.
- Skill template.

Acceptance criteria:

- Every skill has complete metadata.
- Skills have clear scopes.
- Skills contain actionable workflows.
- Skill discovery works through Markdown instructions.
- Skills avoid unnecessary duplication.

## PHASE 4 — CONTEXT AND MEMORY SYSTEM

Develop:

- CONTEXT.md
- MEMORY.md
- DECISIONS.md
- Related templates.

Acceptance criteria:

- Current context is separated from historical knowledge.
- Decisions preserve their history.
- Agents can update knowledge consistently.
- Context initialization is documented.
- Unknown information is not fabricated.

## PHASE 5 — DEVELOPMENT CONTINUITY SYSTEM

Develop:

- TASKS.md
- CHANGELOG.md
- Session handoff procedures.
- Development report templates.
- docs_agent documentation.

Acceptance criteria:

- Tasks have explicit states.
- Development history is preserved.
- Session handoffs are actionable.
- Reports reflect actual changes.
- Future agents can continue unfinished work.

## PHASE 6 — COMPATIBILITY AND VALIDATION

Validate the complete framework against different agent instruction models.

Check:

- Universal entry point.
- Explicit loading procedure.
- Skill selection.
- Context preservation.
- Instruction precedence.
- Existing project integration.
- Nested project instructions.
- Conflicting documentation.
- Large-context handling.
- Missing files.
- Empty project initialization.

Create a manual compatibility matrix.

Do not claim to have tested an agent that was not actually tested.

Acceptance criteria:

- Framework instructions are internally consistent.
- Every referenced file exists.
- No broken Markdown navigation.
- No conflicting file responsibilities.
- All documented workflows can be followed without external software.

## PHASE 7 — RELEASE AND FINAL DOCUMENTATION

Develop:

- Final README.md.
- Installation instructions.
- Usage examples.
- Integration guidance.
- Architecture documentation.
- Contribution guidelines.
- Release checklist.

Acceptance criteria:

- A developer can clone the repository.
- A developer can copy UMSF into an existing project.
- A compatible coding agent can initialize the framework using the documented instructions.
- The framework requires no package installation.
- All seven phases are documented.

---

# 11. EXECUTION RULES

Follow these rules throughout development.

## Rule 1: Inspect before implementation

Inspect the existing repository before creating or modifying files.

If the repository is empty, initialize the proposed structure.

If it contains existing work, preserve it.

## Rule 2: Work phase by phase

Complete one phase at a time.

Do not implement future phases prematurely unless necessary to establish an agreed architecture.

## Rule 3: Avoid unnecessary complexity

Prefer short, explicit and actionable Markdown instructions.

Do not create a file simply to increase the number of files.

Every file must have a clear responsibility.

## Rule 4: Do not duplicate knowledge

Use references between Markdown documents.

Maintain one authoritative location for each type of information.

## Rule 5: Validate every phase

Check:

- File existence.
- Correct paths.
- Markdown structure.
- Internal references.
- Metadata consistency.
- Responsibility separation.
- Instruction consistency.

Use available local tools if necessary, but do not introduce dependencies into the framework.

## Rule 6: Preserve user control

Do not make destructive changes without authorization.

Do not silently modify unrelated source code.

Do not claim success without verification.

## Rule 7: Maintain documentation

Update docs_agent/ after every meaningful phase.

Keep implementation status accurate.

---

# 12. REQUIRED DEVELOPMENT REPORT FORMAT

At the end of each phase, create a report using this structure:

# Phase [NUMBER] — [PHASE NAME]

## 1. Objectives
What this phase intended to achieve.

## 2. Architecture
What architectural decisions were made.

## 3. Implemented Files
List every created or modified file.

## 4. Implementation Details
Explain the actual work completed.

## 5. Validation
List checks performed and their actual results.

## 6. Acceptance Criteria
List each criterion and whether it passed.

## 7. Issues
Record unresolved problems.

## 8. Decisions
Record important decisions and their rationale.

## 9. Context Updates
Identify updated context, memory, tasks and decisions.

## 10. Next Phase
Describe the next phase and outstanding prerequisites.

Save phase-specific reports under:

docs_agent/phases/

Create this directory when beginning Phase 1.

Use:

docs_agent/phases/PHASE_01_FOUNDATION.md
docs_agent/phases/PHASE_02_INSTRUCTIONS.md
docs_agent/phases/PHASE_03_SKILLS.md
docs_agent/phases/PHASE_04_CONTEXT_MEMORY.md
docs_agent/phases/PHASE_05_CONTINUITY.md
docs_agent/phases/PHASE_06_COMPATIBILITY.md
docs_agent/phases/PHASE_07_RELEASE.md

---

# 13. INITIALIZATION AND EXECUTION

Begin immediately.

First:

1. Inspect the current working directory.
2. Identify existing files and documentation.
3. Determine whether this is a new repository or an existing project.
4. Preserve existing work.
5. Establish the UMSF architecture.
6. Begin Phase 1.

Do not simply explain what you would do.

Actually create and maintain the Markdown files in the local repository.

Do not ask the user to manually create files that you can create yourself.

If an important decision is genuinely required, ask one focused question rather than inventing an answer.

Do not move to Phase 2 until Phase 1 acceptance criteria are satisfied.

At the end of Phase 1:

- Validate all deliverables.
- Update docs_agent/IMPLEMENTATION_STATUS.md.
- Update docs_agent/PHASE_HISTORY.md.
- Create docs_agent/DEVELOPMENT_LOG.md.
- Create docs_agent/SESSION_LOG.md.
- Generate docs_agent/phases/PHASE_01_FOUNDATION.md.
- Provide a concise completion report.

Then wait for the user's instruction to continue to Phase 2.

---

# 14. FINAL SUCCESS DEFINITION

UMSF is successful when:

A developer can clone the repository, copy its Markdown framework into any software project, open that project with a compatible AI coding agent, and instruct the agent to read AGENTS.md.

The agent must then be able to:

- Understand the framework.
- Inspect the existing project.
- Load the correct context.
- Discover relevant skills.
- Follow project rules.
- Execute development tasks.
- Validate its work.
- Preserve important knowledge.
- Update project documentation.
- Leave a useful handoff for the next session.

All without installing a framework runtime, connecting an external service, or introducing third-party dependencies.

**Your mission: Build UMSF as a complete, practical, reusable and genuinely universal Markdown Skills Framework. Start with Phase 1.**