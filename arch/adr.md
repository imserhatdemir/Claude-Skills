---
description: Draft an Architecture Decision Record for a technical decision with options analysis
---

Draft an ADR for the decision described in $ARGUMENTS.

**Step 1** — Understand the decision context by reading relevant code and existing ADRs if any.

**Format:**

```markdown
# ADR-[number]: [Short title of the decision]

Date: YYYY-MM-DD
Status: Proposed | Accepted | Deprecated | Superseded by ADR-[X]
Deciders: [names or roles]

## Context

What is the situation that forces us to make a decision?
Include constraints, requirements, and the problem being solved.
Be specific — avoid vague statements.

## Decision Drivers

- Driver 1 (e.g. must support multi-tenancy)
- Driver 2 (e.g. team has no experience with X)
- Driver 3 (e.g. must deploy within 2 weeks)

## Considered Options

1. Option A — [name]
2. Option B — [name]
3. Option C — [name]

## Decision

We chose **Option [X]** because [brief rationale].

## Consequences

**Positive:**
- Consequence 1
- Consequence 2

**Negative:**
- Trade-off 1
- Trade-off 2

**Risks:**
- Risk 1 — mitigation: [how we address it]

## Options Analysis

### Option A — [name]
Description: ...
Pros: ...
Cons: ...

### Option B — [name]
Description: ...
Pros: ...
Cons: ...

### Option C — [name]
Description: ...
Pros: ...
Cons: ...
```

**Rules:**
- ADRs are immutable once accepted — create a new ADR to supersede, never edit
- Future readers should understand why the decision was made, not just what
- If the decision was obvious, it probably doesn't need an ADR

Output the completed ADR ready to save as `docs/adr/ADR-[number]-[slug].md`.
