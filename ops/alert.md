---
description: Design monitoring alert rules with thresholds, severity tiers, routing, and runbooks
---

Design alert rules for $ARGUMENTS (service, feature, or incident description).

**Step 1** — Understand the service architecture and identify critical paths.

**Alert Design Principles**
- Alerts fire on symptoms (user impact), not causes (CPU high)
- Every alert has a clear action — if you don't know what to do, it should not page
- Alert fatigue prevention: start with fewer, higher-signal alerts
- Severity tiers: P0 (wake someone up) / P1 (fix during business hours) / P2 (track, fix in sprint)

**Core Alerts to Define**

For each alert, specify:
```
Name: [descriptive name]
Severity: P0 | P1 | P2
Condition: [metric] [operator] [threshold] for [duration]
Evaluation window: [e.g. 5 minutes]
Fire when: [X consecutive failures / percentage of time]
Message: [what happened — include service, metric, current value]
Runbook: [link or inline steps]
Route to: [team / on-call rotation]
```

**Recommended Alert Categories**

Availability:
- HTTP 5xx error rate > 1% for 5 minutes (P0)
- Health check failing for > 2 minutes (P0)
- Service instance count below minimum (P1)

Latency:
- p95 response time > 2s for 5 minutes (P1)
- p99 response time > 5s for 5 minutes (P0 for critical endpoints)

Database:
- Connection pool exhausted (P0)
- Query time p95 > 1s for 10 minutes (P1)
- Replication lag > 30s (P1)

Business:
- Zero successful transactions in 10 minutes during business hours (P0)
- Failed payment rate > 2% (P0)

Infrastructure:
- Disk > 85% full (P1), > 95% (P0)
- Memory > 90% for 10 minutes (P1)

**Runbook Template for Each Alert**
```
## [Alert Name] Runbook
Symptom: What the user sees
Check first: [command or dashboard link]
Common causes: [list]
Resolution steps: [numbered list]
Escalate to: [team/person] if unresolved after [X minutes]
```

Output a complete alert specification with runbook stubs for each alert.
