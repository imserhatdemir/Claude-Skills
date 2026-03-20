---
description: Thorough code review covering correctness, maintainability, performance, and test coverage
---

Perform a code review on $ARGUMENTS (or the current git diff if not specified).

**Step 1** — Read the target file(s) or run `git diff` to identify all changes.

**Correctness**
- Logic errors, off-by-one, null/undefined handling
- Edge cases not covered
- Incorrect assumptions about data shapes or async behavior
- Race conditions in concurrent code

**Performance**
- N+1 queries or unnecessary network calls
- Heavy computations on the render/request path
- Missing memoization or caching where appropriate
- Allocations in hot loops (string concat, LINQ in tight loops)

**Maintainability**
- Functions doing more than one thing
- Magic numbers or strings without constants
- Deep nesting that can be flattened (guard clauses)
- Dead code or unused imports
- Naming that misleads or is ambiguous

**Test Coverage**
- Critical paths tested
- Edge cases and error paths covered
- Tests assert behavior, not implementation

> Security and auth concerns are handled by `/review:security`. Only flag obvious injection or data exposure here.

Output findings as a prioritized list: **Critical > Major > Minor > Nit**. Include `file_path:line_number` for each. Suggest a concrete fix for Critical and Major items.
