Analyze the current project and generate a complete, tailored .claude/ folder structure from scratch. Do not copy files from other projects.

## Phase 1 — Project Analysis

Run the following to understand the project:

```bash
# Root files
ls -1

# Package managers / tech stack signals
cat package.json 2>/dev/null || true
cat requirements.txt 2>/dev/null || true
cat pyproject.toml 2>/dev/null || true
cat go.mod 2>/dev/null || true
cat Cargo.toml 2>/dev/null || true
cat *.csproj 2>/dev/null || true
cat composer.json 2>/dev/null || true

# Directory structure (top 2 levels)
find . -maxdepth 2 -not -path '*/.git/*' -not -path '*/node_modules/*' -not -path '*/__pycache__/*' | sort
```

From the output, determine:
- **Languages & frameworks** (React, Next.js, FastAPI, Django, .NET, Go, etc.)
- **Database** (PostgreSQL, MySQL, SQLite, MongoDB, etc.)
- **ORM / migration tool** (SQLAlchemy+Alembic, Prisma, EF Core, GORM, etc.)
- **Testing framework** (pytest, Jest, xUnit, etc.)
- **Multi-tenant?** Look for `tenant_id`, `organization_id`, `workspace_id` in source files
- **AI integrations?** Look for anthropic, openai, gemini imports
- **Auth pattern** (JWT, session, OAuth)
- **Monorepo?** Multiple apps in subdirectories

## Phase 2 — Create Directory Structure

```bash
mkdir -p .claude/agents .claude/commands .claude/rules
```

## Phase 3 — Generate agents/

For each agent, write a `.claude/agents/<name>.md` file. Generate only the agents that make sense for this project's stack.

### Always generate:
- **code-reviewer.md** — tailored to the detected languages (e.g. TypeScript strict mode checks if TS, null safety if C#, etc.)
- **security-auditor.md** — tailored to the detected auth pattern, frameworks, and any AI integrations found

### Generate if applicable:
- **db-explorer.md** — if a database/ORM is detected; reference the actual ORM and migration tool found
- **api-explorer.md** — if a backend API framework is detected; reference the actual framework (FastAPI, Express, ASP.NET, etc.)
- **tenant-guard.md** — only if multi-tenancy signals are found in the codebase
- **test-runner.md** — if a test framework is detected

### Agent file format:
```
---
description: <one line — when to use this agent>
tools: <comma-separated list relevant to this agent>
model: <haiku for read-only/cheap tasks, sonnet for analysis/generation>
---

<System prompt tailored to this project's actual stack, file structure, and conventions>
```

Use `haiku` for agents that only read/search (db-explorer, api-explorer).
Use `sonnet` for agents that analyze or generate (code-reviewer, security-auditor, tenant-guard).

## Phase 4 — Generate commands/

Write a `.claude/commands/<name>.md` file for each command. Generate only commands that fit the project's workflow.

### Always generate:
- **review.md** — code review against main/master branch

### Generate if applicable:
- **migration.md** — if ORM + migration tool detected; use the actual CLI commands (e.g. `alembic`, `prisma migrate`, `dotnet ef migrations`)
- **logs.md** — if there is a backend server and/or frontend dev server
- **test.md** — if a test framework is detected; use the actual test command
- **add-page.md** or **add-feature.md** — if a frontend framework is detected; scaffold using the project's actual file structure

Each command file must reference real paths and real CLI commands found in the project, not generic placeholders.

## Phase 5 — Generate rules/

Write a `.claude/rules/<name>.md` file for each rule module. Use `globs:` frontmatter to scope each rule to the relevant file paths.

### Always generate:
- **code-style.md** (global scope) — infer from existing code: tabs vs spaces, naming conventions, import style, comment style

### Generate if applicable:
- **frontend.md** — scoped to frontend source files; reference actual state management, component patterns, and styling found
- **backend.md** — scoped to backend source files; reference actual framework patterns, error handling, and dependency injection found
- **ai-safety.md** — only if AI API usage is detected; reference the actual providers found
- **testing.md** — scoped to test files; reference actual testing patterns found

### Rule file format:
```
---
globs: <glob pattern for relevant files>
---

<Rules inferred from the actual codebase conventions>
```

## Phase 6 — Generate settings.json

Write `.claude/settings.json`. Base permissions on what the project actually uses:

```json
{
  "permissions": {
    "allow": [
      "Bash(git *)",
      "Bash(git log *)",
      "Bash(git diff *)",
      "Bash(git status)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force*)"
    ]
  }
}
```

Add allow rules for the actual package manager and dev commands found (e.g. `npm run *`, `uvicorn *`, `dotnet *`, `go run *`).
Always deny: `rm -rf`, force push, reading `.env` files directly.

## Phase 7 — Generate CLAUDE.md

Write `CLAUDE.md` in the project root. Include:
- **Commands** section: actual dev, build, test commands from package.json / Makefile / pyproject.toml
- **Architecture** section: inferred from directory structure and detected stack
- **Conventions** section: inferred from existing code patterns
- **Watch out for** section: any sharp edges detected (e.g. strict TS, multi-tenancy, env var patterns)

## Phase 8 — Summary

After all files are written, print a summary:
- List every file created
- Note which agents/rules were skipped and why
- Remind the user to review CLAUDE.md and adjust anything that was inferred incorrectly
