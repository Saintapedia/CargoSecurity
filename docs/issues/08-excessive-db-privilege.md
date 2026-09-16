# 8. Excessive database privilege and shared-database blast radius

**Severity:** Critical

## Risk

Cargo needs to create and drop its data tables. If Cargo uses the same broadly privileged account and database as core MediaWiki, an application-layer SQL flaw can have a much larger impact.

## Evidence / context

Cargo's official installation documentation explicitly recommends a separate database because a security leak could otherwise expose or modify information and because expensive Cargo queries can affect the main wiki. Cargo helper tables remain in the main MediaWiki database.

## Recommended fixes

- Use a separate Cargo database/schema and a unique Cargo DB credential.
- Grant the Cargo DB role only the privileges required within the Cargo schema (for example SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER as needed by the selected DB), with no global/admin/file privileges.
- Deny the Cargo role access to MediaWiki core schemas/tables and verify network/database ACLs reinforce that boundary.
- For high-availability environments, consider placing the Cargo database on separate infrastructure or a workload-isolated database service.

## Validation

- Log in as the Cargo DB user and verify core MediaWiki tables cannot be selected, modified, or dropped.
- Confirm the Cargo schema can still create/recreate its own tables after least-privilege changes.
- Review database grants after upgrades; ensure no installer or operational change silently broadened privileges.

See also: [Database isolation and least privilege](../05-database-isolation.md) for the concrete setup.

---

[← Previous: Privileged table recreation](07-privileged-table-recreation.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: API/export enumeration →](09-api-export-enumeration.md)
