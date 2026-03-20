---
description: Review MudBlazor component usage, theming, custom styling, and layout quality
---

Review MudBlazor usage in $ARGUMENTS (or current file/selection if not specified).

**Step 1** — Read the target `.razor` files and identify MudBlazor components in use.

**Component Usage**
- Native MudBlazor components used instead of raw HTML equivalents
- `MudForm` with `MudTextField`, `MudSelect` etc. instead of plain `<form>` / `<input>`
- `MudTable` / `MudDataGrid` used for tabular data with built-in sorting/pagination
- Dialog and drawer management via `IDialogService` not manual visibility flags
- Snackbar/notifications via `ISnackbar` not custom toast implementations

**Theming**
- Colors reference theme palette (`Color.Primary`, `Color.Error`) not hardcoded hex
- Custom theme defined in `MudThemeProvider` — not scattered inline styles
- Typography uses `Typo` enum values consistently
- Dark/light mode toggled via theme, not CSS overrides

**Styling Overrides**
- `Class` and `Style` parameters used minimally — prefer theme tokens
- `!important` in CSS overrides flagged — indicates theme conflict
- Component-specific CSS classes overridden in isolated CSS, not global
- Razor CSS isolation (`.razor.css`) used for component-scoped styles

**Layout & Responsiveness**
- `MudGrid` / `MudItem` with correct `xs`, `sm`, `md` breakpoints
- `MudHidden` used for responsive visibility instead of CSS display hacks
- `MudDrawer` properly configured for mobile/desktop variants

**Accessibility**
- `aria-label` provided for icon-only buttons
- `MudTooltip` added for icon buttons without visible text
- Form fields have associated labels via `Label` parameter

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
