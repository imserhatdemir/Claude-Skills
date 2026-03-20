---
description: Review Dockerfile and docker-compose for security, layer optimization, and correctness
---

Review Docker configuration in $ARGUMENTS (Dockerfile, compose file, or directory).

**Step 1** — Read the Dockerfile and any docker-compose files in the target location.

**Dockerfile**

Base Image:
- Specific version tag used (`mcr.microsoft.com/dotnet/aspnet:8.0` not `:latest`)
- Minimal base image used (alpine or slim variant where possible)
- Official Microsoft images used for .NET (not community-maintained)

Multi-stage Build:
- Build stage separate from runtime stage
- Only runtime artifacts copied to final image (no SDK, source code, or test files)
- `.dockerignore` present and excludes: `.git`, `node_modules`, `bin`, `obj`, test files

Layer Optimization:
- `COPY` of dependency files (`.csproj`, `package.json`) before source code to cache restore layer
- `RUN` commands chained with `&&` to minimize layers
- `apt-get` installs cleaned up in same layer (`rm -rf /var/lib/apt/lists/*`)

Security:
- Container does not run as root (`USER` instruction sets non-root user)
- No secrets in `ENV` or `ARG` instructions
- `HEALTHCHECK` instruction defined
- Exposed ports documented with `EXPOSE`

**docker-compose**

- `restart: unless-stopped` on production services
- Health checks defined for all services
- Secrets via environment variables from `.env` file, not hardcoded
- Volumes defined for persistent data (database data directory)
- Networks explicitly defined — services not all on default bridge
- Resource limits set (`mem_limit`, `cpus`) for production compose

**Image Size**
- Current image size (estimate from layers)
- Opportunities to reduce: multi-stage build, smaller base, fewer tools

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
