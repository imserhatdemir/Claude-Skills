---
description: Pre-release checklist covering migrations, config, secrets, dependencies, and deployment readiness
---

Run a pre-release check for $ARGUMENTS (version number or release branch) before deploying to production.

**Step 1** — Review the git log, pending migrations, and configuration changes since the last release.

**Database**
- [ ] All pending EF Core migrations applied to staging and verified
- [ ] No destructive migration without a tested rollback plan
- [ ] Database backup taken on production before deployment
- [ ] Long-running migrations scheduled during low-traffic window

**Configuration & Secrets**
- [ ] All new environment variables added to production config / secrets manager
- [ ] No new secrets committed to source control
- [ ] `appsettings.Production.json` reviewed for correctness
- [ ] Feature flags configured correctly for production

**Dependencies**
- [ ] NuGet and npm packages audited (`dotnet list package --vulnerable`, `npm audit`)
- [ ] No packages with known HIGH/CRITICAL vulnerabilities in release
- [ ] Third-party service API versions compatible

**Build & Tests**
- [ ] All tests passing on CI (unit, integration, e2e)
- [ ] Build warnings reviewed — none introduced by this release
- [ ] Bundle size within acceptable range (frontend)
- [ ] Performance benchmarks not regressed

**Deployment**
- [ ] Deployment order documented (DB migration before or after code deploy)
- [ ] Rollback procedure documented and tested
- [ ] Health check endpoints responding correctly on staging
- [ ] Monitoring and alerting configured for new features

**Communication**
- [ ] Changelog drafted and reviewed
- [ ] Breaking changes communicated to affected teams
- [ ] Release notes prepared for end users if applicable

Output a **go / no-go** summary with any blocking items listed clearly.
