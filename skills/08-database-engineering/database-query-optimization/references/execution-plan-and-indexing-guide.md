# Query Execution Plan Analysis & Indexing Strategy (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.8.0  
> Authority: Level 3 Optional Reference Asset for `database-query-optimization`  
> Domain: 08 — Database Engineering  

---

## 1. Overview
This reference asset details the interpretation of query execution plans (`EXPLAIN ANALYZE`), scan types, join algorithms, and indexing strategies in PostgreSQL, MySQL, and SQLite. Load this document when diagnosing slow queries, evaluating composite index column ordering, or tuning high-volume database workloads.

---

## 2. PostgreSQL Execution Plan Interpretation

```sql
EXPLAIN (ANALYZE, BUFFERS, VERBOSE, COSTS)
SELECT o.id, o.total_amount, c.name
FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE o.status = 'completed' AND o.created_at >= '2026-01-01'
ORDER BY o.created_at DESC
LIMIT 50;
```

### 2.1 Key Execution Plan Node Types

| Node Type | Mechanism | Efficiency Tier | Diagnostic Action |
|---|---|---|---|
| **Seq Scan (Sequential Scan)** | Reads every page on disk from start to finish. | Low on large tables; OK on tiny tables. | Check if missing index on WHERE / JOIN columns. |
| **Index Scan** | Traverses B-Tree index, then fetches heap tuple. | High for selective queries (<5% of table). | Good; verify index selectivity. |
| **Index Only Scan** | Fetches all requested columns directly from index without visiting heap. | **Highest** (Maximum efficiency). | Use covering indexes (`INCLUDE` clause) to enable this. |
| **Bitmap Index Scan** | Creates bitmap of matching tuple pointers, then batches heap reads. | Moderate/High for medium selectivity (5-20%). | Normal when combining multiple indexes via AND/OR. |
| **Nested Loop** | For each outer row, searches inner table. | High when outer set is small and inner is indexed. | If inner table is large without index, causes severe lag. |
| **Hash Join** | Builds hash table of inner relation, probes with outer relation. | High for large un-indexed joins in memory (`work_mem`). | Watch for disk spills (`Batches: > 1`). |
| **Merge Join** | Joins two pre-sorted relations by scanning sequentially. | Very high when both inputs are pre-sorted by index. | Requires index supporting the join sort order. |

---

## 3. Index Design Rules

### 3.1 Composite Index Column Ordering (Equality First, Range Second)
When queries combine equality filters (`=`) and range filters (`>`, `<`, `BETWEEN`, `IN`):
1. **Column 1**: High-selectivity equality columns (`WHERE tenant_id = ? AND status = ?`).
2. **Column 2**: Range or sorting columns (`AND created_at >= ? ORDER BY created_at DESC`).
```sql
-- Optimal index for: WHERE tenant_id = 10 AND status = 'active' ORDER BY created_at DESC
CREATE INDEX idx_orders_tenant_status_created 
ON orders (tenant_id, status, created_at DESC);
```

### 3.2 Covering Indexes (`INCLUDE`)
Store non-predicate columns directly in index leaf nodes to avoid heap lookups:
```sql
-- Enables 100% Index Only Scan for query: SELECT total_amount FROM orders WHERE customer_id = 42;
CREATE INDEX idx_orders_customer_covering 
ON orders (customer_id) INCLUDE (total_amount);
```

### 3.3 Partial Indexes
Index only a subset of rows to save disk space and write overhead:
```sql
-- Indexes only unfulfilled orders (e.g. 2% of total rows)
CREATE INDEX idx_orders_pending 
ON orders (created_at) 
WHERE status IN ('pending', 'processing');
```

---

## 4. Keyset / Cursor Pagination vs OFFSET

### The OFFSET Trap (High Latency at Scale)
```sql
-- SLOW: Scans and discards 100,000 rows before returning 50 rows
SELECT id, title, created_at FROM events ORDER BY created_at DESC LIMIT 50 OFFSET 100000;
```

### The Keyset / Cursor Solution ($O(1)$ Performance)
```sql
-- FAST: Uses index seek directly to the last known cursor position
SELECT id, title, created_at 
FROM events 
WHERE created_at < '2026-11-06T12:00:00Z' 
ORDER BY created_at DESC 
LIMIT 50;
```

