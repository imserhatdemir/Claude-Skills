---
description: Draft a Linear or Jira ticket from a feature idea or bug description
---

Draft a development ticket based on $ARGUMENTS (the feature idea, bug description, or context provided).

**Ticket Structure:**

```
Title: [type] Short, specific title (max 60 chars)
Type: Feature | Bug | Chore | Spike

## Description
Clear explanation of what needs to be done and why.
Include relevant context, links, or background.

## Acceptance Criteria
- [ ] Specific, testable condition 1
- [ ] Specific, testable condition 2
- [ ] Edge cases covered
- [ ] Error states handled

## Technical Notes
- Affected files or services (if known)
- Dependencies or blockers
- Suggested approach (optional — leave blank for assignee to decide)

## Out of Scope
- Explicitly list what this ticket does NOT cover to prevent scope creep

## Estimate
T-shirt size: XS | S | M | L | XL
```

**Rules:**
- Acceptance criteria must be verifiable (avoid "should feel fast", prefer "LCP < 2s")
- Bugs include: steps to reproduce, expected behavior, actual behavior
- Spikes include: a clear question to answer and a timebox
- Do not over-specify the implementation — leave room for the assignee

Output the ticket ready to paste. If multiple tickets are needed, output each separately.
