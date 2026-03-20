---
description: Review API endpoints for RESTful design, request handling, response consistency, and performance
---

Review the API code in $ARGUMENTS (or current selection if not specified).

**Step 1** — Read the controller/endpoint file(s) and identify the API style (minimal API / controller-based).

**Endpoint Design**
- RESTful resource naming (nouns, not verbs; plural collections)
- Correct HTTP methods (GET read, POST create, PUT/PATCH update, DELETE remove)
- No business logic leaked into URL structure
- Consistent base path and versioning (e.g. `/api/v1/`)

**Request Handling**
- Input validation at the boundary (required fields, types, formats)
- Query params sanitized and typed
- File upload size and type limits enforced

**Response Structure**
- Consistent response envelope across all endpoints
- Correct HTTP status codes (201 for create, 204 for delete, 400/422 for validation, 401/403 for auth)
- Error responses include a machine-readable code and human-readable message
- Pagination applied to list endpoints (limit/offset or cursor-based)

**Authentication & Authorization**
- Auth middleware applied to all protected routes
- Authorization checked at the resource level (not just route level)
- No sensitive data returned to unauthorized callers

**Performance**
- N+1 query patterns in list endpoints
- Missing indexes implied by query patterns
- Heavy endpoints that should be async/queued

> Deep security audit (CORS, headers, injection) is handled by `/review:security`. Flag only obvious issues here.

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
