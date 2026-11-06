---
name: database-design
description: Guidelines for relational and non-relational database schema design, normalization, indexing strategies, migrations, and query optimization.
version: 1.7.0
category: development
tags: [database, schema, sql, migrations, indexing, postgres, nosql, normalization]
---

# Skill: Database Schema Design & Modeling

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 08 — Database Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `database-design`
- **Category**: Database Engineering (Domain 08)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Design normalized relational schemas, NoSQL document models, and indexing strategies for data integrity and performance.
- **When to Use**: Creating new data models, establishing foreign key relationships, designing document schemas, or indexing queries.
- **Essential Invariants**:
  1. Enforce referential integrity using foreign keys and constraint checks in relational databases.
  2. Primary keys must be immutable and unique (UUIDv7, BigInt auto-increment, ULID).
  3. Create targeted indexes for all frequently filtered, joined, or sorted columns.
- **Minimal Workflow**:
  1. Identify entities, attributes, and cardinality (1:1, 1:N, N:M).
  2. Design normalized relational schema (3NF) or optimized document structure.
  3. Define foreign key constraints, unique indexes, and cascade policies.
  4. Author schema DDL or ORM migration files with automated schema verification tests.
- **Expected Deliverables**: Validated database schema DDL or ORM definitions with complete foreign key and index definitions.
- **Critical Restrictions**: Never store unindexed foreign keys in high-traffic tables; avoid unconstrained polymorphic relations.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes robust methodologies for data modeling, schema normalization, index design, foreign key constraints, migration authoring, and query performance optimization across relational and document databases.

---

### Scope
- **In-Scope**:
  - Relational schema modeling (3NF normalization, foreign keys, constraints).
  - Index strategy formulation (B-tree, GIN/GIST, composite index ordering).
  - Authoring reversible, non-blocking schema migrations.
  - Query profiling, EXPLAIN plan analysis, and N+1 query elimination.
- **Out-of-Scope**:
  - Backend controller routing and business service logic (delegate to [`skills/backend-development/SKILL.md`](../../backend-development/SKILL.md)).
  - Server infrastructure and DB clustering operations (infrastructure concern).

---

### When to Use
- When creating new database tables, collections, foreign keys, or indexes.
- When drafting schema migration scripts.
- When troubleshooting slow queries or high database CPU utilization.

---

### When Not to Use
- For purely client-side state caching or local storage implementations.
- For business logic that does not alter data structures or query patterns.

---

### Prerequisites
- Verified target database engine (e.g. PostgreSQL, SQLite, MySQL, MongoDB).
- Functional requirements and read/write access patterns understood.

---

### Required Context
- Existing schemas and migrations verified in `CONTEXT.md`.
- Mandatory constraints in `RULES.md`.

---

### Core Instructions
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

### Step-by-Step Workflow
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

### Quality Standards
- **Data Integrity**: Zero orphan records possible due to explicit foreign key constraints.
- **Query Efficiency**: P95 query execution time under 50ms for OLTP workloads.
- **Rollback Tested**: 100% of migration scripts pass both up and down execution without data loss.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Migration Invariance | Run `migrate:up` then `migrate:down` | Schema state resets cleanly without residual artifacts |
| Index Coverage | Query execution plan inspection | Critical filters and joins execute via Index Scan |
| Parameterization | SQL syntax check | Zero string concatenation in query formulation |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Unindexed Foreign Keys | Causes full table scans during cascade deletes and joins | Always add explicit index on foreign key columns |
| N+1 Query in ORM | Iterating over parent rows and fetching children multiplies database round-trips | Use eager joins or `WHERE id IN (...)` batch loading |

---

### Restrictions
- Do NOT perform non-parameterized SQL queries.
- Do NOT author destructive migrations (`DROP COLUMN`, `DROP TABLE`) without verified rollback plans and data backups.

---

### Expected Deliverables
- Paired schema migration files (`up` and `down`).
- Updated data model documentation or ERD definitions.

---

### Documentation Requirements
- Record schema changes and new database invariants in `CONTEXT.md`.
- Record indexing lessons in `MEMORY.md`.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
