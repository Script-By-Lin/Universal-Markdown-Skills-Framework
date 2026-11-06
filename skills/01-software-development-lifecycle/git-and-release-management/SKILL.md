---
name: git-and-release-management
description: Govern version control workflows, branching conventions, semantic versioning, conventional commits, and release tagging.
version: 2.0.0
category: software-development-lifecycle
tags: [git, versioning, semver, conventional-commits, changelog, releases]
---

# Skill: Git Versioning & Release Management

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: 01-software-development-lifecycle  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `git-and-release-management`
- **Category**: 01-software-development-lifecycle
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Govern version control workflows, branching conventions, semantic versioning, conventional commits, changelogs, and release tag creation.
- **When to Use**: Creating branches, staging commits, authoring CHANGELOG updates, cutting semantic releases, or tagging production builds.
- **Essential Invariants**:
  1. Strictly follow Conventional Commits format (feat:, fix:, chore:, refactor:, docs:, test:).
  2. Semantic Versioning (MAJOR.MINOR.PATCH) is mandatory for all release tags and CHANGELOG entries.
  3. Never commit secrets, local IDE configs, build artifacts, or unverified broken builds to main branches.
- **Minimal Workflow**:
  1. Verify working directory status and ensure all changes pass test suites before staging.
  2. Review staged diff to guarantee zero extraneous files or secrets are staged.
  3. Craft atomic conventional commit message reflecting intent and impact.
  4. Update CHANGELOG.md following Keep a Changelog standards upon release tagging.
- **Expected Deliverables**: Clean atomic git commits, updated CHANGELOG.md, and annotated git release tags.
- **Critical Restrictions**: Prohibit force pushes to protected branches; never commit credentials or generated binary artifacts.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose & Scope
Govern version control workflows, branching conventions, semantic versioning, conventional commits, and release tagging.

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
