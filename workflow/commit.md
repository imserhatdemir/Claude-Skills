---
description: Draft a conventional commit message based on staged changes
---

Generate a commit message for the current staged changes.

1. Run `git diff --staged` to read all staged changes.
2. Identify the nature of the change and the affected scope.
3. Draft a commit message following Conventional Commits:

**Format:**
```
type(scope): short description

optional body — what changed and why, not how
```

**Types:**
- `feat` — new feature
- `fix` — bug fix
- `refactor` — code change with no behavior change
- `perf` — performance improvement
- `style` — formatting, whitespace (no logic change)
- `test` — adding or updating tests
- `chore` — build, deps, config, tooling
- `docs` — documentation only

**Rules:**
- Subject line max 72 characters
- Imperative mood ("add", not "added" or "adds")
- No period at the end of subject
- Body explains *why*, not *what* (the diff shows what)
- Breaking changes noted as `BREAKING CHANGE:` in body

If $ARGUMENTS is provided, use it as additional context for the message.

Output only the final commit message, ready to copy. Do not run `git commit`.
