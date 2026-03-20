---
description: Audit dark and light theme consistency across components, tokens, and contrast
---

Audit theme implementation in $ARGUMENTS (or entire codebase if not specified).

**Step 1** — Identify the theming approach (CSS variables, Tailwind dark:, MudBlazor theme, etc.).

**Token Usage**
- Hardcoded color values (`#fff`, `rgb(0,0,0)`) instead of theme tokens
- CSS variables or Tailwind dark: classes used consistently
- No color defined in only one theme (missing dark or light counterpart)

**Contrast & Readability**
- Text contrast meets WCAG AA (4.5:1 for body, 3:1 for large text) in both themes
- Placeholder and disabled text still readable in both themes
- Link colors distinguishable from body text in both themes

**Component Coverage**
- Modals, drawers, tooltips, and dropdowns themed correctly
- Form inputs, selects, and textareas have correct background and border in both themes
- Scrollbars styled if custom (match theme)
- Code blocks and syntax highlighting work in both themes

**Images & Icons**
- SVG icons use `currentColor` for theme adaptability
- Images with white/dark backgrounds that clash with opposite theme
- Shadows appropriate for theme (light: darker shadows, dark: subtle or glow)

**System Preference**
- `prefers-color-scheme` media query honored on initial load
- Theme toggle persisted to localStorage
- No flash of incorrect theme on page load (SSR hydration issue)

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
