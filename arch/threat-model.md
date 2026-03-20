---
description: Draft a threat model for a new feature or system using STRIDE methodology
---

Draft a threat model for $ARGUMENTS (feature name, system description, or diagram).

**Step 1** — Understand the feature/system by reading relevant code, docs, or the provided description.

**System Overview**
- What does this feature/system do?
- Who are the users (authenticated, anonymous, admin)?
- What data does it process or store?
- External systems it integrates with?

**Trust Boundaries**
- Where does control pass from one trust zone to another?
  - Internet -> Load balancer
  - Load balancer -> Application server
  - Application server -> Database
  - Application server -> External APIs
  - User browser -> Application (Blazor WASM boundary)

**Data Flow Diagram (text)**
```
[Actor] -> [Entry Point] -> [Process] -> [Data Store]
```
List each data flow with trust boundary crossings marked.

**STRIDE Threat Analysis**

For each trust boundary or component, identify threats:

| Threat | Category | Component | Attack Scenario | Mitigation | Risk |
|--------|----------|-----------|-----------------|------------|------|
| | Spoofing | | | | High/Med/Low |
| | Tampering | | | | |
| | Repudiation | | | | |
| | Information Disclosure | | | | |
| | Denial of Service | | | | |
| | Elevation of Privilege | | | | |

**STRIDE Categories:**
- **S**poofing — claiming to be someone else (auth bypass, token theft)
- **T**ampering — modifying data in transit or at rest
- **R**epudiation — denying an action occurred (missing audit logs)
- **I**nformation Disclosure — exposing data to unauthorized parties
- **D**enial of Service — making the system unavailable
- **E**levation of Privilege — gaining more access than authorized

**Top Risks (prioritized)**
1. [Highest risk threat] — mitigation: [action]
2. ...

**Mitigations Required Before Launch**
- [ ] Mitigation 1
- [ ] Mitigation 2

**Accepted Risks**
- Risk [X] accepted because [reason] — reviewed by [owner]

Output the completed threat model ready for security review.
