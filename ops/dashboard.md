---
description: Design a Grafana or Azure Monitor dashboard for a service or feature
---

Design a monitoring dashboard for $ARGUMENTS (service name, feature, or use case).

**Step 1** — Understand the service architecture and identify key metrics to visualize.

**Dashboard Purpose**
- Define the primary audience: on-call engineer / product manager / executive
- Primary question this dashboard answers

**Panel Layout**

Row 1 — Service Health (always visible at top)
- Overall health status (green/red)
- Uptime % (last 24h, 7d, 30d)
- Active instances / pod count

Row 2 — Traffic
- Request rate (req/s) — time series
- HTTP status code breakdown (2xx, 4xx, 5xx) — stacked bar
- Top endpoints by volume — table

Row 3 — Latency
- p50, p95, p99 response time — time series
- Slowest endpoints — table
- Apdex score (if applicable)

Row 4 — Errors
- Error rate % — time series with threshold line
- Error count by type — pie or table
- Recent error log tail — logs panel

Row 5 — Database
- Query duration p95 — time series
- Active connections — gauge
- Slow queries — table

Row 6 — Business Metrics (service-specific)
- [Define key business metrics relevant to the service]

**Dashboard Variables**
- `$environment` — prod / staging / dev
- `$instance` — all / specific pod
- `$interval` — auto-adjusted time grouping

**Annotations**
- Deployment markers (when new versions were released)
- Incident markers

**Grafana Panel Config Notes**
- Default time range: last 3 hours
- Auto-refresh: 30s for on-call use, 5m for overview
- Thresholds: green < 1% error, yellow 1-5%, red > 5%

Output a dashboard specification ready to implement in Grafana or Azure Monitor.
