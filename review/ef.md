---
description: Review Entity Framework Core queries, migrations, data access patterns, and DbContext usage
---

Review EF Core code in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the target file(s). Identify whether reviewing queries, repository layer, or migration files.

**Query Performance**
- N+1 queries: navigation properties accessed in loops without `.Include()`
- `AsNoTracking()` used for read-only queries
- `.ToListAsync()` called before filtering (client-side evaluation)
- Projections with `.Select()` used instead of loading full entities when only a few fields are needed
- `AsSplitQuery()` considered for queries with multiple collection includes

**Lazy Loading Risks**
- Lazy loading enabled without awareness of N+1 consequences
- Virtual navigation properties triggering unexpected queries outside the original scope

**DbContext Lifetime**
- DbContext registered as Scoped (not Singleton or Transient)
- DbContext not passed between threads
- Long-lived DbContext causing stale data or memory growth

**Migration Safety**
- `DropColumn` / `DropTable` — is the column/table still referenced in code?
- New non-nullable column without a default value
- Column type change — will existing data convert cleanly?
- Index creation on large tables — lock implications noted

**Repository Patterns**
- Generic repository not hiding useful EF features (`.Include`, `.AsSplitQuery`)
- Specification pattern used consistently if present
- `SaveChangesAsync` called at the right boundary (unit of work)

**Concurrency**
- Optimistic concurrency configured where needed (`[ConcurrencyCheck]` or row version)
- `DbUpdateConcurrencyException` handled

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
