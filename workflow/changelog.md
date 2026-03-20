---
description: Generate a release changelog from git history since the last tag
---

Generate a changelog for the next release.

1. Run `git tag --sort=-version:refname | head -1` to find the last release tag.
2. Run `git log <last-tag>...HEAD --oneline` to get all commits since then.
3. Group commits by type and draft the changelog:

**Format:**
```
## [version] - YYYY-MM-DD

### New Features
- Description of user-facing change (#PR or commit ref)

### Bug Fixes
- Description of fix (#PR or commit ref)

### Performance
- Description of improvement

### Breaking Changes
- Description of breaking change and migration steps

### Internal
- Refactors, dependency updates, chore items (keep brief)
```

**Rules:**
- Write from the user's perspective — what does this change mean for them
- Skip commits that are purely internal with no user impact (unless breaking)
- Merge commits and version bump commits omitted
- Breaking changes always listed first with migration guidance

If $ARGUMENTS is provided, treat it as the version number for the release header.

Output the changelog section only, ready to paste into CHANGELOG.md.
