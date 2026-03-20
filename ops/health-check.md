---
description: Design or review health check endpoints with liveness, readiness, and dependency checks
---

Design or review health check implementation for $ARGUMENTS (service name, project, or existing endpoint).

**Step 1** — Read `Program.cs` or startup configuration to check existing health check setup.

**Endpoint Design**
- `/health/live` — liveness: is the process running? (no dependency checks, fast)
- `/health/ready` — readiness: is the service ready to handle traffic? (checks dependencies)
- `/health` — summary endpoint for general monitoring tools
- Response format: HTTP 200 (healthy) / 503 (unhealthy), JSON body with status per check

**ASP.NET Core Health Checks**
```csharp
builder.Services.AddHealthChecks()
    .AddNpgsql(connectionString, name: "postgres")
    .AddSqlServer(connectionString, name: "mssql")
    .AddUrlGroup(new Uri("https://external-api/ping"), name: "external-api")
    .AddCheck<CustomDependencyCheck>("custom");

app.MapHealthChecks("/health/ready", new HealthCheckOptions
{
    ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
});
app.MapHealthChecks("/health/live", new HealthCheckOptions
{
    Predicate = _ => false
});
```

**Dependency Checks to Include**
- [ ] Primary database (PostgreSQL / MSSQL)
- [ ] Secondary databases or read replicas
- [ ] External HTTP APIs (critical integrations only)
- [ ] Message queue / service bus connectivity
- [ ] Cache (Redis, in-memory) if used
- [ ] File storage (disk space, blob storage connectivity)

**What NOT to Check in Liveness**
- External services (a slow third-party should not kill your pod)
- Business logic validations
- Anything that takes more than 100ms

**Security**
- Health endpoints not exposed publicly without auth or IP restriction
- No sensitive data (connection strings, stack traces) in health response body

**Kubernetes / Container Integration**
- Liveness probe uses `/health/live` with failure threshold >= 3
- Readiness probe uses `/health/ready` with initial delay matching startup time
- Startup probe configured for slow-starting services

Output a review of existing implementation or a full design ready to implement.
