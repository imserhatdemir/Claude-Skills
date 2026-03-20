# claude-commands

A curated collection of **47 custom slash commands** for [Claude Code](https://docs.anthropic.com/en/docs/claude-code), organized into 7 categories. Built for teams working with **.NET / Blazor / TypeScript** stacks, but most skills are stack-agnostic.

Each skill is a focused, reusable prompt that enforces consistent review criteria, generates standardized artifacts, or runs pre-flight checklists -- directly from your terminal.

## Quick Start

### Installation

Clone this repository into your Claude Code commands directory:

```bash
# Global commands (available in all projects)
git clone https://github.com/imserhatdemir/Claude-Skills.git ~/.claude/commands

# Project-scoped commands (available only in this project)
git clone https://github.com/imserhatdemir/Claude-Skills.git ~/.claude/commands
```

### Usage

```
/category:skill [argument]
```

The argument is typically a file path, feature name, or description. When omitted, the skill operates on the current diff or selection.

```bash
# Review a C# file for async patterns and DI issues
/review:dotnet Services/PaymentService.cs

# Generate a conventional commit message from staged changes
/workflow:commit

# Run a pre-release checklist before deploying
/check:release v2.4.0

# Design a database schema before writing migrations
/arch:db-schema "user subscription billing"

# Estimate AI API costs for a feature
/ai:cost "document summarization pipeline"
```

## Categories

### [`review/`](review/) -- Code Review & Audits (14 skills)

Static analysis and review prompts covering correctness, security, performance, and stack-specific patterns.

| Skill | What it does |
|---|---|
| `review:code` | General code review -- correctness, maintainability, performance, test coverage |
| `review:dotnet` | .NET async/await, dependency injection, null safety, sealed classes |
| `review:blazor` | Blazor component lifecycle, rendering, state management, JS interop |
| `review:api` | REST API design, HTTP semantics, request/response consistency |
| `review:ef` | EF Core queries, N+1 detection, migration safety, DbContext lifetime |
| `review:sql` | SQL performance, index usage, injection risks (PostgreSQL & MSSQL) |
| `review:typescript` | Type safety, `any` usage, null handling, tsconfig strictness |
| `review:perf` | Frontend bundle size, code splitting, rendering, Core Web Vitals |
| `review:security` | Auth, secrets management, injection, security headers, env vars |
| `review:deps` | NuGet/npm vulnerabilities, outdated packages, license compliance |
| `review:logs` | Log levels, PII exposure, structured logging, signal-to-noise |
| `review:tests` | Test quality, coverage gaps, isolation, assertion correctness |
| `review:token-optimize` | AI token usage analysis and cost reduction strategies |
| `review:api-docs` | OpenAPI/Swagger documentation completeness and quality |

### [`design/`](design/) -- UI/UX Design Review (6 skills)

Visual quality, accessibility, responsiveness, and user experience analysis.

| Skill | What it does |
|---|---|
| `design:ui` | UI consistency, accessibility (WCAG), responsiveness |
| `design:ux` | User flows, interactions, microcopy, cognitive load |
| `design:theme` | Dark/light theme consistency, token usage, contrast ratios |
| `design:landing` | Landing page conversion, visual hierarchy, mobile experience |
| `design:motion` | Animation quality, performance, `prefers-reduced-motion` |
| `design:mudblazor` | MudBlazor component usage, theming, styling overrides |

### [`arch/`](arch/) -- Architecture & Planning (6 skills)

Pre-implementation design and decision documentation.

| Skill | What it does |
|---|---|
| `arch:api-design` | REST API contract design with request/response schemas |
| `arch:db-schema` | Database table design with EF Core entity sketch |
| `arch:blazor-structure` | Component hierarchy, service layer, responsibility boundaries |
| `arch:threat-model` | STRIDE threat model with trust boundaries and mitigations |
| `arch:spec` | Technical specification with scope, design, and API contract |
| `arch:adr` | Architecture Decision Record with options analysis |

### [`workflow/`](workflow/) -- Development Process (8 skills)

Artifact generation for commits, PRs, tickets, and team documentation.

| Skill | What it does |
|---|---|
| `workflow:commit` | Conventional commit message from `git diff --staged` |
| `workflow:pr` | Pull request with title, summary, changes, and test plan |
| `workflow:changelog` | Release changelog grouped by type from git history |
| `workflow:ticket` | Linear/Jira ticket with acceptance criteria and estimate |
| `workflow:user-story` | User stories sliced by value with testable criteria |
| `workflow:test-cases` | QA test scenarios with steps, expected results, and test data |
| `workflow:onboarding` | Developer onboarding guide generated from codebase |
| `workflow:incident` | Blameless incident postmortem with timeline and action items |

### [`ops/`](ops/) -- DevOps & Observability (6 skills)

Infrastructure review and monitoring design.

| Skill | What it does |
|---|---|
| `ops:docker` | Dockerfile and docker-compose review (layers, security, size) |
| `ops:pipeline` | CI/CD pipeline review (GitHub Actions, Azure DevOps) |
| `ops:infra` | Infrastructure as Code review (Terraform, Bicep, ARM) |
| `ops:health-check` | Health check endpoint design (liveness, readiness, dependencies) |
| `ops:alert` | Alert rules with severity tiers, thresholds, and runbooks |
| `ops:dashboard` | Grafana / Azure Monitor dashboard specification |

### [`check/`](check/) -- Pre-flight Checklists (4 skills)

Go/no-go validation before deployments and changes.

| Skill | What it does |
|---|---|
| `check:migration` | EF Core migration safety review (destructive ops, data loss, locks) |
| `check:release` | Pre-release checklist (migrations, secrets, deps, rollback plan) |
| `check:db-change` | Schema change review (naming, indexes, backward compatibility) |
| `check:pentest` | Penetration test scoping and environment preparation |

### [`ai/`](ai/) -- AI Development (3 skills)

Prompt engineering, RAG pipeline review, and cost estimation.

| Skill | What it does |
|---|---|
| `ai:prompt` | System prompt review for clarity, safety, and token efficiency |
| `ai:rag` | RAG pipeline review (chunking, retrieval, re-ranking, grounding) |
| `ai:cost` | API cost estimation with model comparison and optimization tips |

## How Skills Work

Each skill is a Markdown file with a YAML frontmatter `description` field and a structured prompt body. Claude Code loads these as slash commands automatically.

**Anatomy of a skill:**

```markdown
---
description: One-line description used for skill matching and triggering
---

Instruction for Claude when the skill is invoked.

**Step 1** -- First action Claude should take (e.g., read the target files).

**Section Name**
- Checklist item or evaluation criterion
- Another criterion

Output format instructions (e.g., prioritized list with file:line references).
```

**Design principles behind this collection:**

- **Step 1 anchoring** -- Every skill starts with a concrete first action so Claude doesn't guess where to begin.
- **Clean responsibility boundaries** -- Security concerns live in `review:security`, not scattered across every review skill. Cross-references replace duplication.
- **Prioritized output** -- Review skills output findings as **Critical > Major > Minor > Nit** with `file_path:line_number` references.
- **Stack-aware, not stack-locked** -- .NET/Blazor specifics are in dedicated skills; general skills work with any stack.

## Customization

**Add a new skill:**

Create a `.md` file in the appropriate category folder with the frontmatter format shown above.

**Modify for your stack:**

Fork this repo and replace stack-specific skills (e.g., swap `review:blazor` for `review:react` or `review:ef` for `review:prisma`).

**Project-scoped overrides:**

Place modified skills in `.claude/commands/` at your project root. Project-scoped commands take precedence over global ones.

## License

MIT
