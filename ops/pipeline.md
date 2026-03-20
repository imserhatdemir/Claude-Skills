---
description: Review CI/CD pipeline configuration for correctness, security, caching, and efficiency
---

Review the pipeline in $ARGUMENTS (workflow file, Azure DevOps YAML, or pipeline description).

**Step 1** — Read the pipeline file(s) and identify the CI/CD platform (GitHub Actions, Azure DevOps, etc.).

**Structure & Stages**
- Pipeline has distinct stages: build -> test -> security scan -> deploy
- Deploy stages gated by manual approval for production
- Failed stage stops pipeline — no deployment on test failure
- Branch policies enforced (main/master protected, PRs required)

**Build**
- Dependencies cached (NuGet, npm) to avoid re-downloading on every run
- Build is reproducible — no reliance on mutable external state
- Build artifacts versioned and stored (not rebuilt per environment)
- Docker images built once and promoted across environments

**Testing**
- Unit tests run on every PR
- Integration tests run before deploy to staging
- Test results published for visibility (JUnit XML, test summary)
- Coverage threshold enforced — build fails below minimum

**Security**
- Secrets stored in vault / secret manager — never in pipeline YAML
- `GITHUB_TOKEN` / service principal permissions scoped to minimum required
- Dependency vulnerability scan runs on every build
- SAST scan included (e.g. SonarCloud, CodeQL)
- Container image scan before push (e.g. Trivy)

**Deployment**
- Blue/green or rolling strategy (no hard cutover)
- Health check verified after deployment before marking success
- Automatic rollback on health check failure
- Deployment environment variables injected from secret store

**Efficiency**
- Jobs parallelized where independent (unit tests, linting, security scans)
- Unnecessary steps removed (redundant restores, duplicate checkouts)
- Pipeline runtime acceptable — flag stages taking > 10 minutes

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
