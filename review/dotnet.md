---
description: Review C# and .NET code for async patterns, dependency injection, null safety, and performance
---

Review .NET code in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the target file(s) and identify the project type (ASP.NET Core, library, worker service).

**Async/Await**
- No `async void` except event handlers — use `async Task`
- No `.Result` or `.Wait()` blocking calls on async methods (deadlock risk)
- `ConfigureAwait(false)` used in library code
- `CancellationToken` propagated through async call chains
- `Task.Run` not used to wrap synchronous code in web applications

**Dependency Injection**
- Services registered with correct lifetime (Singleton/Scoped/Transient)
- Scoped services not injected into Singleton services (captive dependency)
- `IHttpContextAccessor` used only where necessary
- Large constructor parameter lists — consider splitting the class

**Exception Handling**
- Specific exceptions caught, not bare `catch (Exception)`
- Exceptions not swallowed silently (empty catch blocks)
- `AggregateException` unwrapped when awaiting `Task.WhenAll`
- Global exception middleware present for unhandled exceptions

**Null Safety**
- Nullable reference types enabled (`<Nullable>enable</Nullable>`)
- Null checks on public method parameters
- `ArgumentNullException.ThrowIfNull()` used (.NET 6+)
- Null-forgiving operator (`!`) used with justification

**Performance**
- `StringBuilder` used for string concatenation in loops
- `IEnumerable` not enumerated multiple times (materialize with `.ToList()`)
- `Span<T>` / `Memory<T>` considered for hot paths
- `sealed` on classes not designed for inheritance

**Code Quality**
- Single Responsibility followed
- Magic strings/numbers replaced with constants or enums
- `record` types used for immutable DTOs
- Pattern matching used where it simplifies conditional logic

Output findings as a prioritized list: **Critical > Major > Minor > Nit**. Include `file_path:line_number`.
