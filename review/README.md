# review/

Code quality, security, performance, and stack-specific review skills. Each skill outputs findings as a prioritized list (**Critical > Major > Minor > Nit**) with `file_path:line_number` references.

## Skills

| Skill | Scope | Key checks |
|---|---|---|
| `review:code` | Any codebase | Correctness, logic errors, dead code, test coverage |
| `review:dotnet` | C# / .NET | Async/await, DI lifetimes, null safety, sealed classes, `Span<T>` |
| `review:blazor` | Blazor Server/WASM | Lifecycle, `StateHasChanged`, `@key`, `IDisposable`, JS interop |
| `review:api` | REST APIs | HTTP semantics, status codes, pagination, resource-level auth |
| `review:ef` | EF Core | N+1 queries, `AsNoTracking`, DbContext lifetime, migration safety |
| `review:sql` | PostgreSQL / MSSQL | Index usage, implicit casts, `NOLOCK` risks, parameterization |
| `review:typescript` | TypeScript | `any` usage, null handling, generics, tsconfig strictness |
| `review:perf` | Frontend | Bundle size, code splitting, `React.memo`, Core Web Vitals |
| `review:security` | Full stack | Auth, secrets, injection, CORS, headers, env var exposure |
| `review:deps` | NuGet / npm | CVE vulnerabilities, outdated packages, license compliance |
| `review:logs` | Logging | Log levels, PII exposure, structured logging, noise reduction |
| `review:tests` | Tests | AAA pattern, isolation, coverage gaps, bUnit, `WebApplicationFactory` |
| `review:token-optimize` | AI/LLM code | Prompt efficiency, context window usage, caching, model routing |
| `review:api-docs` | OpenAPI/Swagger | `[ProducesResponseType]`, XML docs, examples, auth schemes |

## Responsibility boundaries

- **Security** concerns are centralized in `review:security`. Other review skills only flag obvious issues and cross-reference.
- **Dependency** vulnerabilities are in `review:deps`. `review:security` does not duplicate this.
- **EF migration** safety checks are in `review:ef` for code review and `check:migration` for pre-apply validation.
