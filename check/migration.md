---
description: Pre-flight checklist before applying an EF Core migration to any environment
---

Review the EF Core migration in $ARGUMENTS (migration file or name) before applying it.

**Step 1** — Read the migration file and list every operation.

**1. Read the Migration**
- List every operation: AddColumn, DropColumn, CreateTable, DropTable, AlterColumn, CreateIndex, etc.

**2. Destructive Operations Check**
- `DropColumn` / `DropTable` — is the column/table still referenced in code?
- `AlterColumn` changing type — will existing data convert cleanly?
- Removing a non-nullable constraint — are there existing NULLs in that column?

**3. Data Migration Check**
- New non-nullable column without a default — will fail on tables with existing rows
- Column rename that requires data copy — EF drops and recreates by default (data loss risk)
- Suggest a data migration script if needed before/after applying

**4. Index Operations**
- `CreateIndex` on a large table — will lock the table in MSSQL (use `ONLINE = ON`)
- PostgreSQL: prefer `CREATE INDEX CONCURRENTLY` for production (not possible in EF migrations — note manual step)

**5. Down() Method**
- `Down()` method is implemented and will correctly reverse the migration
- Test `Down()` reversal is safe (no data loss on rollback)

**6. Environment Checklist**
- [ ] Migration tested on a local database with production-like data volume
- [ ] Backup taken before applying to staging/production
- [ ] Applied to staging first and verified application behavior
- [ ] Deployment order: deploy migration before or after code deploy? (flag breaking changes)
- [ ] Rollback plan documented

**7. Multi-Database**
- If targeting both PostgreSQL and MSSQL: verify migration SQL is compatible or separate migrations exist

Output a summary of findings and a **go / no-go** recommendation with reasons.
