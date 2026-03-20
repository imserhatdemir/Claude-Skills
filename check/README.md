# check/

Pre-flight validation checklists that produce a **go / no-go** recommendation. Run these before applying changes to shared environments.

## Skills

| Skill | When to run | Key validations |
|---|---|---|
| `check:migration` | Before applying an EF Core migration | Destructive ops, data loss risk, index locks, `Down()` method |
| `check:release` | Before deploying to production | Migrations, secrets, deps, CI status, rollback plan |
| `check:db-change` | Before merging schema changes | Naming conventions, indexes, backward compatibility, lock impact |
| `check:pentest` | Before a penetration test engagement | Scope definition, environment prep, attack surface checklist |
