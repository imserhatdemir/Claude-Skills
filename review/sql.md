---
description: Review SQL queries for PostgreSQL and MSSQL covering performance, indexes, and injection risks
---

Review SQL in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the query file(s) or inline SQL. Note the target database engine (PostgreSQL / MSSQL).

**Query Performance**
- `SELECT *` used where specific columns would suffice
- Missing `WHERE` clause on UPDATE/DELETE (full table scan or accidental mass update)
- Implicit type conversions causing index bypass (e.g. comparing `varchar` to `nvarchar`)
- Correlated subqueries that can be rewritten as JOINs
- `DISTINCT` used to mask a join problem

**Index Usage**
- Columns in `WHERE`, `JOIN`, and `ORDER BY` have supporting indexes
- Composite index column order matches query patterns
- Covering indexes considered for frequently read queries
- Unused indexes identified (write overhead without read benefit)

**MSSQL Specific**
- `NOLOCK` / `READ UNCOMMITTED` used without understanding dirty read risk
- `OPTION (RECOMPILE)` on queries with parameter sniffing issues
- `SET NOCOUNT ON` in stored procedures

**PostgreSQL Specific**
- `EXPLAIN ANALYZE` used to verify query plan
- `CREATE INDEX CONCURRENTLY` for production index creation
- Proper use of `jsonb` operators and GIN indexes for JSON queries

**Security**
- No string concatenation for building SQL — use parameterized queries
- Dynamic SQL in stored procedures uses `sp_executesql` (MSSQL) or `EXECUTE ... USING` (PostgreSQL)
- User input never directly interpolated into query text

**Data Integrity**
- Transactions used for multi-statement operations
- Appropriate isolation level chosen
- Deadlock-prone access patterns identified (inconsistent table access order)

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
