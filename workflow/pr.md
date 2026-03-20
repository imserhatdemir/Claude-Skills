---
description: Prepare and create a pull request with a well-structured title, summary, and test plan
---

Prepare a pull request for the current branch.

1. Run `git diff main...HEAD` and `git log main...HEAD --oneline` to understand all changes.
2. Identify the base branch (default: `main`).
3. Draft the PR:

**Title** — max 70 characters, imperative mood, no period.
Format: `type: short description`
Types: feat | fix | refactor | chore | docs | perf | test

**Body template:**
```
## Summary
- <what changed and why — 2-4 bullet points>

## Changes
- <notable implementation details>

## Test Plan
- [ ] <manual or automated steps to verify>
- [ ] <edge cases checked>

## Screenshots (if UI changes)
<attach or note "N/A">
```

4. Push the branch if not already pushed: `git push -u origin <branch>`
5. Create the PR with `gh pr create` using the drafted title and body.
6. Return the PR URL.

If $ARGUMENTS is provided, treat it as additional context or target branch override.
