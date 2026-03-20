---
description: Convert acceptance criteria or user stories into structured QA test scenarios
---

Convert the acceptance criteria in $ARGUMENTS (user story, ticket, or feature description) into QA test scenarios.

**Step 1** — Read the user story or feature description and extract all acceptance criteria.

**Output format for each scenario:**

```
### TC-[number]: [Short test case title]
Priority: P0 | P1 | P2
Type: Functional | Edge Case | Negative | Security | Performance

Preconditions:
- User is logged in as [role]
- [Other setup required]

Steps:
1. [Action]
2. [Action]
3. [Action]

Expected Result:
[Exactly what should happen — UI state, data change, API response]

Test Data:
- Valid input: [example]
- Boundary input: [example]
- Invalid input: [example]
```

**Test Coverage Matrix**

For each acceptance criterion, generate:
- 1 happy path test (valid input, expected flow)
- 1-2 negative tests (invalid input, missing data, wrong role)
- 1 boundary test (min/max values, empty collections)
- 1 error handling test (network failure, server error)

**Test Categories to Cover**
- Functional: does the feature do what it should?
- Authorization: can only the right roles access it?
- Validation: are invalid inputs rejected with clear messages?
- State: does the system state change correctly after the action?
- UI: are loading, success, and error states displayed correctly?

**Automation Notes**
- Mark each test case: Automate | Manual only
- Automate: repeatable, stable, business-critical paths
- Manual only: visual checks, exploratory, one-off scenarios

Output all test cases grouped by feature area.
