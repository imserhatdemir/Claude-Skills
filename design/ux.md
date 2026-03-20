---
description: Review UX flows, interactions, user-facing copy, and cognitive load for usability issues
---

Review the UX of $ARGUMENTS (or current selection/page if not specified).

**Step 1** — Read the target page/component and trace the primary user flow.

**User Flow**
- Clear entry and exit points for each task
- Logical step progression; no dead ends
- Error states and empty states handled gracefully

**Feedback & Affordance**
- Loading states present for async actions
- Success/error messages are clear and actionable
- Interactive elements look clickable (hover, focus, cursor)

**Copy & Microcopy**
- Button labels are action-oriented (verb + noun)
- Error messages explain what went wrong and how to fix it
- Placeholder text is not used as a substitute for labels

**Cognitive Load**
- Forms are minimal and grouped logically
- Destructive actions require confirmation
- Defaults are sensible and reduce required input

**Mobile UX**
- Touch targets meet minimum size (44x44px)
- No hover-only interactions on mobile paths
- Modals/drawers usable on small screens

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
