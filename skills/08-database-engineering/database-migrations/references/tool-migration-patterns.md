# Database Migration Tool Patterns (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `database-migrations`  
> Domain: 08 — Database Engineering  

---

## 1. Overview
Concrete syntax and operational recipes for zero-downtime database migrations across PostgreSQL, Prisma, Drizzle, Django, and golang-migrate. Load this reference only when generating tool-specific migration scripts.

---

## 2. PostgreSQL Direct SQL (Raw DDL)

### 2.1 Safe Concurrent Index Creation
```sql
-- Creating an index concurrently prevents locking read/write traffic
CREATE INDEX CONCURRENTLY IF NOT EXISTS idx_users_active_email
ON users (email)
WHERE status = 'active';
```

### 2.2 Adding Non-Null Columns Safely (Postgres 11+)
```sql
-- Postgres 11+ supports adding columns with constant default without table rewrite
ALTER TABLE orders
ADD COLUMN IF NOT EXISTS currency VARCHAR(3) NOT NULL DEFAULT 'USD';
```

---

## 3. Prisma Schema Migration Patterns
- Generate migration: `npx prisma migrate dev --create-only --name add_currency_to_orders`
- Review generated SQL in `prisma/migrations/` before applying.
- In production CI/CD: `npx prisma migrate deploy` (never run `db push` in production).

---

## 4. Drizzle ORM Migration Patterns
- Generate SQL: `npx drizzle-kit generate`
- Apply migrations: `npx drizzle-kit migrate`
- Always verify generated `.sql` files for missing `CONCURRENTLY` clauses on index additions.

