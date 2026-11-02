---
name: database-design
description: Guidelines for relational and non-relational database schema design, normalization, indexing strategies, migrations, and query optimization.
version: 1.0.0
category: development
tags: [database, schema, sql, migrations, indexing, postgres, nosql, normalization]
---

# Skill: Database Design & Optimization

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `database-design`
- **Category**: Engineering & Data
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes robust methodologies for data modeling, schema normalization, index design, foreign key constraints, migration authoring, and query performance optimization across relational and document databases.

---

## 3. Scope
- **In-Scope**:
  - Relational schema modeling (3NF normalization, foreign keys, constraints).
  - Index strategy formulation (B-tree, GIN/GIST, composite index ordering).
  - Authoring reversible, non-blocking schema migrations.
  - Query profiling, EXPLAIN plan analysis, and N+1 query elimination.
- **Out-of-Scope**:
  - Backend controller routing and business service logic (delegate to [`skills/backend-development/SKILL.md`](../backend-development/SKILL.md)).
  - Server infrastructure and DB clustering operations (infrastructure concern).

---

## 4. When to Use
- When creating new database tables, collections, foreign keys, or indexes.
- When drafting schema migration scripts.
- When troubleshooting slow queries or high database CPU utilization.

---

## 5. When Not to Use
- For purely client-side state caching or local storage implementations.
- For business logic that does not alter data structures or query patterns.

---

## 6. Prerequisites
- Verified target database engine (e.g. PostgreSQL, SQLite, MySQL, MongoDB).
- Functional requirements and read/write access patterns understood.

---

## 7. Required Context
- Existing schemas and migrations verified in [`CONTEXT.md`](../../CONTEXT.md).
- Mandatory constraints in [`RULES.md`](../../RULES.md).

---

## 8. Core Instructions
1. **Explicit Constraints**:
   - Enforce data integrity at the database layer using `NOT NULL`, `UNIQUE`, `CHECK`, and `FOREIGN KEY` constraints. Never rely solely on application-level checks.
2. **Indexing Strategy**:
   - Index all foreign key columns.
   - For composite indexes, place columns filtered with equality (`=`) first, followed by range (`>`, `<`, `BETWEEN`) or sort (`ORDER BY`) columns.
   - Avoid over-indexing; every index degrades write/insert performance.
3. **Reversible, Non-Blocking Migrations**:
   - Every migration script must include a deterministic rollback mechanism (`down` migration).
   - In production databases, avoid adding default values to large tables without non-blocking techniques.
4. **Prevent N+1 Query Traps**:
   - Always load relational associations using eager loading, joins, or batch queries. Never query relational children inside a row iteration loop.

---

## 9. Step-by-Step Workflow
1. **Step 1: Entity-Relationship Modeling**
   - Identify entities, attributes, primary keys, and cardinality (1:1, 1:N, N:M).
2. **Step 2: Schema Normalization & Constraint Definition**
   - Normalize to Third Normal Form (3NF) to eliminate anomalies; identify deliberate denormalization only if justified by read profiling.
3. **Step 3: Migration Authoring**
   - Create paired `up` and `down` migration scripts using deterministic naming.
4. **Step 4: Index Optimization & Query Profiling**
   - Review critical queries with `EXPLAIN ANALYZE`; verify that index scans replace sequential table scans.
5. **Step 5: Migration Execution & Verification**
   - Execute migration in test environment; execute rollback; re-execute migration.

---

## 10. Quality Standards
- **Data Integrity**: Zero orphan records possible due to explicit foreign key constraints.
- **Query Efficiency**: P95 query execution time under 50ms for OLTP workloads.
- **Rollback Tested**: 100% of migration scripts pass both up and down execution without data loss.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Migration Invariance | Run `migrate:up` then `migrate:down` | Schema state resets cleanly without residual artifacts |
| Index Coverage | Query execution plan inspection | Critical filters and joins execute via Index Scan |
| Parameterization | SQL syntax check | Zero string concatenation in query formulation |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Unindexed Foreign Keys | Causes full table scans during cascade deletes and joins | Always add explicit index on foreign key columns |
| N+1 Query in ORM | Iterating over parent rows and fetching children multiplies database round-trips | Use eager joins or `WHERE id IN (...)` batch loading |

---

## 13. Restrictions
- Do NOT perform non-parameterized SQL queries.
- Do NOT author destructive migrations (`DROP COLUMN`, `DROP TABLE`) without verified rollback plans and data backups.

---

## 14. Expected Deliverables
- Paired schema migration files (`up` and `down`).
- Updated data model documentation or ERD definitions.

---

## 15. Documentation Requirements
- Record schema changes and new database invariants in [`CONTEXT.md`](../../CONTEXT.md).
- Record indexing lessons in [`MEMORY.md`](../../MEMORY.md).

