---
description: Review test quality, coverage gaps, assertion correctness, and test isolation
---

Review tests in $ARGUMENTS (or current test file/selection if not specified).

**Step 1** — Read the test file(s) and identify the test framework (xUnit, NUnit, Jest, Vitest, bUnit).

**Test Structure**
- Arrange / Act / Assert pattern followed
- One logical assertion per test (or grouped assertions for one behavior)
- Test names describe behavior, not implementation (`Should_ReturnError_WhenEmailIsInvalid`)
- No logic (loops, conditions) inside test bodies

**Assertion Quality**
- Assertions test behavior and outcomes, not internal implementation details
- `Assert.Equal` used with expected value first, actual second
- Exception assertions use `Assert.ThrowsAsync<T>` not try/catch
- Collection assertions check content, not just count

**Test Isolation**
- Tests do not share mutable state
- Database tests use transactions rolled back after each test or isolated test databases
- External services mocked or faked — no real HTTP calls in unit tests
- Clock / DateTime abstracted (`IDateTimeProvider`) for deterministic time-dependent tests

**Coverage Gaps**
- Happy path tested but no edge cases (empty input, null, boundary values)
- Error paths and exception scenarios not covered
- Authorization checks not tested (unauthenticated, wrong role)
- Async cancellation paths not tested

**Blazor / UI Tests**
- `bUnit` used for Blazor component testing
- Component renders tested with parameter variations
- Event callbacks verified (button clicks, form submissions)

**Integration Tests**
- `WebApplicationFactory<T>` used for ASP.NET Core integration tests
- Database seeded consistently before each test
- Tests verify end-to-end behavior through HTTP, not just service layer

Output findings as a prioritized list: **Critical > Major > Minor > Nit**. Include `file_path:line_number`.
