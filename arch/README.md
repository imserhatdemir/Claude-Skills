# arch/

Pre-implementation design and decision documentation. These skills produce artifacts for team review **before** any code is written.

## Skills

| Skill | Output | When to use |
|---|---|---|
| `arch:api-design` | REST API contract (request/response/errors) | Before implementing a new endpoint |
| `arch:db-schema` | Table definition + EF Core entity sketch | Before writing a migration |
| `arch:blazor-structure` | Component hierarchy + service layer design | Before building a new Blazor feature |
| `arch:threat-model` | STRIDE threat analysis with mitigations | Before launching a security-sensitive feature |
| `arch:spec` | Full technical specification | Before starting any non-trivial feature |
| `arch:adr` | Architecture Decision Record | When making a significant technical choice |
