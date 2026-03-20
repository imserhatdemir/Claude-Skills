---
description: Review or generate OpenAPI/Swagger documentation quality for ASP.NET Core APIs
---

Review or generate API documentation for $ARGUMENTS (controller, endpoint, or project).

**Step 1** — Locate the Swagger/OpenAPI configuration and controller files.

**OpenAPI Coverage**
- All endpoints have `[ProducesResponseType]` for each possible HTTP status code
- Request body types documented with XML comments or Swashbuckle annotations
- Response types documented — no `IActionResult` without `[ProducesResponseType]`
- Endpoints tagged by resource/controller for logical grouping in Swagger UI

**Descriptions & Examples**
- Each endpoint has a summary (`/// <summary>`) and description
- Parameters have descriptions (query params, route params, headers)
- Request and response body properties have XML doc comments
- At least one example provided for complex request/response bodies
- Error response bodies documented (not just status code)

**Swashbuckle Configuration**
```csharp
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "API", Version = "v1" });
    c.IncludeXmlComments(xmlPath);
    c.EnableAnnotations();
    c.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme {...});
});
```

**Auth Documentation**
- JWT / API key scheme defined in Swagger config
- Protected endpoints marked with `[Authorize]` show lock icon
- Auth header format documented in API info description

**Versioning**
- API version reflected in Swagger doc title and URL
- Deprecated endpoints marked with `[Obsolete]`
- Version differences documented between v1 and v2 if multiple versions exist

**Quality Issues**
- Endpoints returning `200` for errors that should be `4xx`
- Missing documentation on enum values
- Nullable fields not marked as nullable in schema

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
