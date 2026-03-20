# workflow/

Development process skills that generate standardized artifacts. These skills read your codebase and git history to produce ready-to-use output.

## Skills

| Skill | Output | Input |
|---|---|---|
| `workflow:commit` | Conventional commit message | `git diff --staged` |
| `workflow:pr` | Pull request (title + body + test plan) | Branch diff against `main` |
| `workflow:changelog` | Grouped release changelog | Commits since last tag |
| `workflow:ticket` | Linear/Jira ticket with acceptance criteria | Feature idea or bug description |
| `workflow:user-story` | User stories sliced by value | Feature or business requirement |
| `workflow:test-cases` | QA test scenarios with steps and test data | User story or acceptance criteria |
| `workflow:onboarding` | Developer onboarding guide | Project structure and docs |
| `workflow:incident` | Blameless postmortem report | Incident summary |
