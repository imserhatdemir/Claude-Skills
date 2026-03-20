---
description: Audit NuGet and npm dependencies for security vulnerabilities, outdated packages, and license compliance
---

Audit dependencies in $ARGUMENTS (project file, package.json, or solution root).

**Step 1** — Identify the package managers in use (NuGet, npm, bun, pnpm) and locate dependency files.

**Security Vulnerabilities**
- Run `dotnet list package --vulnerable` for NuGet packages
- Run `npm audit` or `bun audit` for frontend packages
- List all HIGH and CRITICAL vulnerabilities with CVE reference
- Identify if vulnerable package is a direct or transitive dependency

**Outdated Packages**
- Run `dotnet list package --outdated` for NuGet
- Run `npm outdated` for frontend
- Flag packages more than 2 major versions behind
- Note packages not updated in over 12 months (abandonment risk)

**Unused Dependencies**
- NuGet packages referenced in .csproj but not imported in any file
- npm packages in `dependencies` that should be in `devDependencies`
- Duplicate packages solving the same problem (e.g. two HTTP client libraries)

**License Compliance**
- Packages with restrictive licenses (GPL, AGPL) in a commercial project
- Packages with no license defined
- MIT, Apache 2.0, BSD licenses confirmed for safe commercial use

**NuGet Specific**
- Central Package Management (`Directory.Packages.props`) used for multi-project solutions
- Package versions consistent across projects
- Floating versions (`*`) flagged — use pinned versions

**npm/bun Specific**
- Lock file (`package-lock.json` / `bun.lockb`) committed and up to date
- No packages installed globally that should be local dev dependencies

Output findings as a prioritized list: **Critical > Major > Minor**. Include package name, current version, and recommended action.
