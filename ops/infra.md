---
description: Review Infrastructure as Code (Terraform, Bicep, ARM) for correctness, security, and cost
---

Review IaC in $ARGUMENTS (file, module, or directory). Note the IaC tool (Terraform / Bicep / ARM) if known.

**Step 1** — Read the IaC files and identify the cloud provider and resource types.

**General IaC Quality**
- Resources named consistently and descriptively
- Tags / labels applied to all resources (environment, owner, cost-center)
- No hardcoded values that should be variables (region, size, passwords)
- Variables have descriptions and type constraints
- Sensitive variables marked as `sensitive = true` (Terraform) or equivalent

**Security**
- No secrets or credentials in IaC files or state
- Storage accounts / blobs not publicly accessible unless intentional
- Databases not publicly accessible — behind VNet or private endpoint
- Network security groups restrict inbound traffic to required ports only
- Managed identities used instead of service principal client secrets where possible
- Encryption at rest enabled on all storage and database resources

**State Management (Terraform)**
- Remote backend configured (Azure Storage, S3) — not local state
- State file encrypted at rest
- State locking enabled to prevent concurrent modifications
- Sensitive outputs marked as sensitive

**Idempotency & Safety**
- `terraform plan` output reviewed before apply — no unexpected destroys
- Resources that cannot be updated in-place identified (require destroy/recreate)
- `lifecycle { prevent_destroy = true }` on critical resources (databases, storage)
- Modules versioned and pinned — no floating version references

**Cost**
- Resource sizes appropriate for environment (don't run prod sizes in dev)
- Auto-scaling configured where traffic is variable
- Unused resources identified

Output findings as a prioritized list: **Critical > Major > Minor**. Include `file_path:line_number`.
