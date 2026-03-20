---
description: Review logging quality, log levels, PII exposure, structured logging, and signal-to-noise ratio
---

Review logging in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the target file(s) and identify the logging framework (Serilog, NLog, Microsoft.Extensions.Logging).

**Log Levels**
- `LogError` / `LogCritical` used only for actionable errors, not warnings
- `LogWarning` for recoverable issues, not informational messages
- `LogInformation` not used in tight loops (performance impact)
- `LogDebug` / `LogTrace` used for verbose developer details
- Production log level configured appropriately (not Debug in prod)

**PII & Sensitive Data**
- Passwords, tokens, or API keys logged at any level
- Email addresses, phone numbers, or national IDs in log messages
- Full request/response bodies logged (may contain sensitive fields)
- User IDs acceptable; full user objects are not
- Connection strings appearing in exception messages

**Structured Logging**
- Message templates use named placeholders (`"User {UserId} logged in"`) not string interpolation
- Log properties are typed values, not `.ToString()` of complex objects
- Consistent property names across the codebase (`UserId` not mixed with `userId` and `user_id`)
- Structured output configured for production (JSON)

**Exception Logging**
- Exception object passed as first argument to `LogError(ex, "message")` — not `ex.Message`
- Inner exceptions not swallowed before logging
- Stack traces preserved through async boundaries

**Noise & Signal**
- Log statements that fire on every request with no filtering
- Duplicate log entries for the same event at different levels
- Missing logs on critical paths (payment processing, auth failures, data mutations)

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
