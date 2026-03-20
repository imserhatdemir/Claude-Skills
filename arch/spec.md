---
description: Generate a technical specification for a new feature with scope, design, and API contract
---

Write a technical specification for the following feature: $ARGUMENTS

**Step 1** — Read relevant existing code, models, and services to understand current architecture.

**Spec Structure:**

```
# Feature: [Name]

## Problem Statement
What user problem does this solve? What is the current pain point?

## Proposed Solution
High-level description of what will be built.

## User Stories
- As a [user type], I want to [action] so that [outcome]

## Scope
**In scope:**
- Item 1
- Item 2

**Out of scope:**
- Item 1 (reason)

## Technical Design

### Frontend
- Components to create or modify
- State management changes
- API calls required

### Backend
- Endpoints to create or modify
- Data model changes (new tables, fields, indexes)
- Business logic summary

### Data Flow
Describe how data moves through the system for the primary use case.

## API Contract
Request/response shapes for any new or changed endpoints.

## Edge Cases & Error States
- Case 1: what happens and how it is handled
- Case 2: what happens and how it is handled

## Open Questions
- Question 1 (owner: ?)
- Question 2 (owner: ?)

## Success Metrics
How will we know this feature is working correctly and delivering value?

## Dependencies & Risks
- Dependency on X team / service
- Risk: Y could happen — mitigation: Z
```

Use the current codebase structure and conventions where relevant. Flag open questions rather than assuming answers.
