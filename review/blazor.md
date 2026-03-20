---
description: Review Blazor component lifecycle, rendering, state management, and JS interop quality
---

Review Blazor component code in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the target `.razor` and `.razor.cs` files. Identify hosting model (Server / WASM / Auto).

**Component Lifecycle**
- `OnInitializedAsync` used for async data loading (not `OnInitialized`)
- `OnParametersSetAsync` used when reacting to parameter changes, not constructor
- `IDisposable` / `IAsyncDisposable` implemented where subscriptions or timers exist
- No async void event handlers — use `async Task` and handle exceptions

**Rendering & Performance**
- `StateHasChanged()` called only when necessary — not after every operation
- `ShouldRender()` overridden to prevent unnecessary re-renders on complex components
- `@key` directive used on list items to preserve DOM identity
- Heavy components wrapped with `<Virtualize>` for long lists
- `[Parameter]` properties not mutated directly (breaks change detection)

**State Management**
- State shared via cascading values, services, or state containers — not prop drilling
- `[CascadingParameter]` used appropriately, not overused
- Component state reset correctly when parameters change

**Data Fetching**
- Loading and error states handled and displayed to user
- API calls not duplicated across parent and child components
- `CancellationToken` passed to async calls where component can be disposed mid-request

**JavaScript Interop**
- `IJSRuntime` calls wrapped in try/catch (JS exceptions don't propagate cleanly)
- JS interop deferred until after render (`OnAfterRenderAsync` with `firstRender`)
- Large JS interop replaced with native Blazor alternatives where possible

**Forms & Validation**
- `EditForm` with `DataAnnotationsValidator` and `ValidationSummary` used
- `Model` binding on `EditForm` not bypassed
- Custom validators implemented as `ValidationAttribute`, not inline logic

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
