---
description: Draft user stories with acceptance criteria from a feature idea or business requirement
---

Write user stories for $ARGUMENTS (feature idea, business requirement, or problem description).

**Step 1** — Understand the feature context by reading relevant code or docs if available.

**Format for each story:**

```
## Story: [Short title]

As a [specific user role],
I want to [specific action or capability],
So that [business outcome or user benefit].

### Acceptance Criteria
- Given [context], when [action], then [outcome]
- Given [context], when [action], then [outcome]
- Given [error condition], when [action], then [error is handled gracefully]

### Notes
- [Edge cases, constraints, or design considerations]
- [Out of scope for this story]

### Size: XS | S | M | L | XL
```

**Story Writing Rules**
- One story = one deliverable slice of value (vertically sliced through the stack)
- "As a user" is too vague — specify the role (admin, guest, billing manager)
- Acceptance criteria are testable — avoid "should be fast", prefer "loads in < 2s"
- Each story independently deployable where possible
- Split stories if they contain "and" in the "I want to" clause

**Slice the Feature**
Break the feature into multiple stories ordered by value:
1. Walking skeleton (minimum that delivers any value)
2. Core functionality
3. Edge cases and error handling
4. Polish and enhancements

Output all stories in the format above, ordered from highest to lowest value.
