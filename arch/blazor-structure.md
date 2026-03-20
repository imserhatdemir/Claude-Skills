---
description: Review or design Blazor component hierarchy, service layer, and responsibility boundaries
---

Review or design the Blazor architecture for $ARGUMENTS (feature, page, or component tree) and evaluate:

**Component Hierarchy**
- Page components (routable, `@page`) contain only layout and orchestration logic
- Smart / container components handle data fetching and state
- Dumb / presentational components receive only parameters and emit callbacks
- Components not doing too many things (single responsibility)

**Service Layer**
- Business logic lives in injected services, not in components
- HTTP calls made in services (`IHttpClientFactory`), not directly in components
- Services registered with correct DI lifetime (Scoped for per-user state in Blazor Server)
- No `HttpClient` created with `new HttpClient()` — always injected

**State Management**
- Ephemeral UI state stays in the component
- Shared state between sibling components lifted to a parent or a state service
- Long-lived state (user session, settings) in a Scoped service or `CascadingValue`
- State mutations always trigger `StateHasChanged` or go through the state service

**Routing & Navigation**
- `NavigationManager` used for programmatic navigation
- Route parameters strongly typed
- Authorization on routes via `AuthorizeRouteView` and `[Authorize]`

**Proposed Structure** (if designing new feature)
```
Pages/
  FeaturePage.razor          — routable, thin orchestrator

Components/
  Feature/
    FeatureList.razor         — presentational, receives items via Parameter
    FeatureForm.razor         — form component, emits OnSubmit callback
    FeatureCard.razor         — single item display

Services/
  IFeatureService.cs
  FeatureService.cs           — HTTP calls, business logic

Models/
  FeatureDto.cs
  CreateFeatureRequest.cs
```

**Findings or Design Output**
- Flag components that violate these boundaries
- Suggest refactoring or propose the structure for a new feature

Output findings or a design document ready for team review.
