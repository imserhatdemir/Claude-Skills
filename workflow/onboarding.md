---
description: Generate a new developer onboarding guide for the current project
---

Generate an onboarding guide for a new developer joining this project.

1. Read the project structure, `README.md`, solution files, and `package.json` to understand the stack.
2. Draft the following:

**Project Overview**
- What the project does in 2-3 sentences
- Tech stack summary (languages, frameworks, databases)
- Architecture overview (monolith / microservices / Blazor WASM / Server)

**Prerequisites**
- Required tools and versions (.NET SDK, Node/Bun, Docker, etc.)
- Required accounts or access (database, cloud, third-party services)
- IDE setup (VS / VS Code / Rider — extensions or plugins needed)

**Local Setup Steps**
1. Clone and branch strategy
2. Environment variable setup (`.env.example` → `.env.local`)
3. Database setup (connection string, migration command)
4. Run command for frontend and backend
5. Verify setup is working (URL, expected output)

**Development Workflow**
- Branch naming convention
- Commit message format
- PR process and review expectations
- How to run tests locally

**Key Concepts**
- Important architectural decisions a new dev needs to know
- Where to find things (auth, data access, shared components)
- What NOT to touch without discussion

**Contacts & Resources**
- [Placeholder for team contacts]
- Links to internal docs, Linear/Jira board, design files

Output as a markdown document ready to save as `ONBOARDING.md`.
