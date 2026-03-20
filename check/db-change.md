---
description: Review database schema changes for naming, indexes, compatibility, and performance before merge
---

Review the schema changes in $ARGUMENTS (migration file, SQL script, or PR diff).

**Step 1** — Read the migration or SQL file and identify all schema modifications.

**Naming Conventions**
- Table names: PascalCase or snake_case — consistent with existing schema
- Column names consistent with existing conventions
- Foreign key constraint names follow pattern (e.g. `FK_Table_ReferencedTable_Column`)
- Index names descriptive and follow pattern (e.g. `IX_Table_Column`)

**Schema Design**
- Primary keys defined on all tables
- Foreign key constraints defined (not just application-level enforcement)
- Appropriate data types chosen (avoid `varchar(MAX)` / `TEXT` for short strings)
- Audit columns present where needed (`CreatedAt`, `UpdatedAt`, `CreatedBy`)
- Soft delete column (`IsDeleted`, `DeletedAt`) if applicable

**Nullable Columns**
- New non-nullable columns have a default value or migration populates existing rows first
- Nullable columns are intentional — document if business logic guarantees non-null

**Indexes**
- Index added for every foreign key column (not done automatically in MSSQL)
- Composite indexes ordered for anticipated query patterns
- Unique constraints defined where business rules require uniqueness

**Backward Compatibility**
- Old column/table still accessible during rolling deploy
- Column rename done in two steps (add new, migrate data, remove old)
- No breaking changes to views or stored procedures

**Performance Impact**
- Estimated row count of affected tables
- Index rebuild time for new indexes on large tables
- Lock implications of schema change (MSSQL vs PostgreSQL behavior noted)

Output a summary with a **go / no-go** recommendation and any required pre/post-deployment steps.
