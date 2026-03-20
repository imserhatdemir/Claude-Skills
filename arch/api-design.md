---
description: Design and validate a new REST API endpoint before implementation
---

Design the API endpoint described in $ARGUMENTS and produce a complete contract before any code is written.

**Resource & URL**
- Identify the resource noun (e.g. `users`, `orders`, `invoices`)
- Correct HTTP method for the operation
- URL structure: `/api/v1/{resource}/{id}/{sub-resource}`
- Query parameters for filtering, sorting, pagination

**Request Contract**
```
Method: POST | GET | PUT | PATCH | DELETE
URL: /api/v1/...
Headers:
  Authorization: Bearer {token}
  Content-Type: application/json

Body (if applicable):
{
  "field": "type — required/optional, validation rules"
}
```

**Response Contract**
```
Success — HTTP 200 | 201 | 204
{
  "field": "type"
}

Error responses:
400 — Validation failure: { "errors": { "field": ["message"] } }
401 — Unauthenticated
403 — Unauthorized
404 — Resource not found
409 — Conflict (duplicate, state mismatch)
422 — Business rule violation
500 — Unexpected server error
```

**Authorization**
- Who can call this endpoint (roles, policies)
- Resource-level authorization rules (owner only, admin override)

**Side Effects**
- Database writes triggered
- Events published or webhooks fired
- Cache invalidation required

**Edge Cases**
- What happens with empty collections
- Concurrent modification handling
- Idempotency for POST (if needed)

**Breaking Change Assessment**
- Is this a new endpoint (safe) or a change to an existing one
- If changing: what clients are affected and migration path

Output the full contract in the format above, ready for team review before implementation begins.
