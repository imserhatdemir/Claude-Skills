---
description: Review TypeScript type safety, any usage, null handling, and missing type coverage
---

Review TypeScript usage in $ARGUMENTS (or current selection if not specified).

**Step 1** — Read the target file(s) and check `tsconfig.json` strict mode settings.

**any Usage**
- Explicit `any` that can be replaced with a proper type or `unknown`
- Implicit `any` from untyped function parameters
- `as any` casts that bypass type safety

**Type Definitions**
- Missing return types on exported functions
- Object shapes typed inline repeatedly instead of a shared interface/type
- Union types used where a discriminated union would be safer
- Enums vs string literal unions — consistency with project convention

**Null & Undefined Handling**
- Optional chaining (`?.`) missing where nulls are possible
- Non-null assertion (`!`) used without guarantee
- `strictNullChecks` violations if tsconfig is strict

**Generics**
- Functions that repeat logic for different types — could be generic
- Overly constrained generics that limit reuse
- Generic type parameters named single letters without context

**Type Assertions**
- `as SomeType` casts without a comment explaining why it is safe
- Double assertions (`as unknown as X`) indicating a type mismatch

**Config**
- `tsconfig.json` strict mode enabled
- `noImplicitAny`, `strictNullChecks`, `noUncheckedIndexedAccess` status

Output findings as a prioritized list: **Critical > Major > Minor > Nit**. Include `file_path:line_number`.
