---
description: Review UI implementation for consistency, accessibility, responsiveness, and visual quality
---

Review the UI code in $ARGUMENTS (or current selection if not specified).

**Step 1** — Read the target component/page files and identify the UI framework in use.

**Consistency**
- Component reuse and design system adherence
- Spacing, color, and typography consistency
- Naming conventions for CSS classes / styled components

**Accessibility (a11y)**
- Semantic HTML elements used correctly
- ARIA labels where needed
- Keyboard navigation support
- Color contrast issues (WCAG AA: 4.5:1 body, 3:1 large text)

**Responsiveness**
- Mobile-first or adaptive layout
- Breakpoint coverage
- Overflow and truncation handling

**Performance**
- Unnecessary re-renders or heavy DOM trees
- Image optimization and lazy loading
- CSS specificity issues

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`. Suggest a fix for each Critical/Major item.
