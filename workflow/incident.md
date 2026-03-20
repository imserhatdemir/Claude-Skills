---
description: Draft a production incident postmortem report
---

Draft a postmortem for the incident described in $ARGUMENTS (incident summary, date, or Slack/ticket link).

**Postmortem Structure:**

```
# Incident Postmortem: [Title]
Date: YYYY-MM-DD
Severity: P0 | P1 | P2
Status: Resolved

## Summary
One paragraph: what happened, who was affected, how long it lasted.

## Timeline
All times in UTC.
- HH:MM — Event or action
- HH:MM — Event or action
- HH:MM — Incident resolved

## Root Cause
Technical explanation of the underlying cause.
Distinguish between the trigger (what set it off) and the root cause (why the system was vulnerable).

## Impact
- Users affected: [number or percentage]
- Features unavailable: [list]
- Data loss or corruption: [yes/no — detail if yes]
- SLA breach: [yes/no]

## What Went Well
- Detection was fast
- Rollback procedure worked as expected
- [Other positives]

## What Went Wrong
- Alert did not fire in time
- Runbook was outdated
- [Other gaps]

## Action Items
| Action | Owner | Due Date | Priority |
|--------|-------|----------|----------|
| Add alert for X | @name | YYYY-MM-DD | High |
| Update runbook | @name | YYYY-MM-DD | Medium |

## Lessons Learned
Key takeaways to prevent recurrence or improve response time.
```

**Rules:**
- Blameless tone throughout — focus on systems and processes, not individuals
- Action items must be specific, assigned, and time-bound
- Root cause must go beyond "human error"

Output the postmortem ready to share with the team.
