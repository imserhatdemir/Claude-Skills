---
description: Review animations and transitions for quality, performance, accessibility, and consistency
---

Review animation and transition code in $ARGUMENTS (or current selection if not specified).

**Step 1** — Read the target file(s) and identify the animation approach (CSS transitions, Framer Motion, etc.).

**Motion Principles**
- Animations serve a purpose (guide attention, indicate state change, provide feedback)
- No decorative animations that add delay without value
- Enter/exit animations are paired and consistent

**Timing & Easing**
- Duration appropriate to element size (small: 100-200ms, large: 300-500ms)
- Easing curves match intent (ease-out for enter, ease-in for exit, ease-in-out for repositioning)
- No linear easing on UI elements (feels robotic)

**CSS Transitions**
- `transition` applied to specific properties, not `all`
- `transform` and `opacity` used for GPU-composited animations
- Avoid animating `width`, `height`, `top`, `left` — use `transform` instead

**Framer Motion (if used)**
- `variants` used for reusable animation states instead of inline objects
- `AnimatePresence` wraps conditionally rendered elements
- `layout` prop used for size/position transitions
- `useReducedMotion` respected for accessibility

**Performance**
- No layout-triggering properties animated (margin, padding, border)
- Heavy animations wrapped in `will-change` where appropriate (used sparingly)
- Animations disabled or reduced when `prefers-reduced-motion` is active

**Consistency**
- Same action always produces the same animation across the app
- Spring configs or duration constants centralized, not scattered

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
