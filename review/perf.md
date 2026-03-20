---
description: Audit frontend performance including bundle size, rendering, code splitting, and Core Web Vitals
---

Audit performance in $ARGUMENTS (or current codebase if not specified).

**Step 1** — Read `package.json`, build config (vite/webpack), and identify the frontend framework.

**Bundle Size**
- Large dependencies imported in full instead of tree-shaken (e.g. `import _ from 'lodash'`)
- Duplicate packages (multiple versions of the same library)
- Heavy libraries where a lighter alternative exists
- Unused dependencies in `package.json`

**Code Splitting**
- Routes lazy-loaded with `React.lazy` / dynamic imports
- Large components or modals not deferred until needed
- Third-party scripts (analytics, chat widgets) loaded async

**Rendering Performance**
- Components re-rendering without prop changes (missing `React.memo`)
- Expensive calculations not memoized (`useMemo`, `useCallback`)
- State updates causing unnecessary parent re-renders (state too high)
- Lists rendered without stable `key` props

**Loading Strategy**
- Images use lazy loading (`loading="lazy"` or Intersection Observer)
- Critical images preloaded (`<link rel="preload">`)
- Fonts loaded with `font-display: swap`
- API calls waterfall instead of running in parallel

**Core Web Vitals**
- LCP: identify the largest contentful element — is it optimized?
- CLS: layout shifts from images without dimensions or dynamic content insertion
- INP: long tasks on the main thread blocking interaction

**Build Config** (if applicable)
- `rollupOptions.output.manualChunks` configured for vendor splitting
- Source maps disabled in production
- Assets fingerprinted for cache busting

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
