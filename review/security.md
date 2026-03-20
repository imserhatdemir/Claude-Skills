---
description: Comprehensive security audit covering auth, secrets, input validation, injection, headers, and environment variables
---

Audit security in $ARGUMENTS (or entire codebase if not specified).

**Step 1** — Identify the application type (ASP.NET Core API, Blazor Server/WASM, fullstack with JS frontend) and scan for security-sensitive patterns.

**Authentication & Authorization**
- `[Authorize]` attribute applied to all protected controllers/endpoints
- Role and policy checks at the resource level, not just route level
- JWT token validation configured (issuer, audience, signing key, expiry)
- Refresh token rotation implemented and old tokens invalidated
- Cookie auth: `HttpOnly`, `Secure`, `SameSite=Strict` flags set

**Input Validation**
- All user input validated with Data Annotations or FluentValidation
- `ModelState.IsValid` checked before processing in controllers
- File uploads: extension whitelist, size limit, content type verified
- Path traversal risk in any file path constructed from user input

**Data Protection & Secrets**
- `IDataProtectionProvider` used for encrypting sensitive data at rest
- Connection strings and secrets NOT in `appsettings.json` — use env vars or secrets manager
- `UserSecrets` in dev, environment variables or Azure Key Vault in production
- PII not logged to application logs (passwords, tokens, personal data)

**Environment Variables**
- Secrets or API keys not hardcoded in source files
- Client-side code (browser bundle) does not contain server-only secrets
- `VITE_` / `NEXT_PUBLIC_` prefixed vars verified to not expose sensitive values
- `.env` files not committed to git (check `.gitignore`)
- `.env.example` file exists and is up to date with all required keys
- Server-only vars never imported in client-side code
- Required env vars validated on startup (fail fast, clear error message)

**SQL & Injection**
- Raw SQL via EF: `FromSqlRaw` uses parameters, not interpolated strings
- Dapper queries parameterized correctly
- No dynamic SQL with string concatenation in stored procedures
- No command injection via `Process.Start` with user input

**ASP.NET Core Security Headers**
- HTTPS redirection middleware enabled (`UseHttpsRedirection`)
- HSTS configured (`UseHsts`)
- CORS policy restrictive — no wildcard `*` origin in production
- Antiforgery tokens validated on state-changing form submissions
- Security headers present: `X-Content-Type-Options`, `X-Frame-Options`, `CSP`
- Rate limiting in place on public and auth endpoints

> Dependency vulnerabilities are handled by `/review:deps`. Only flag obviously dangerous packages here.

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
