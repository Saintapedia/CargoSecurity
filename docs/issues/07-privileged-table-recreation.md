# 7. Privileged table recreation and deletion

**Severity:** High

## Risk

Cargo adds `recreatecargodata` and `deletecargodata` rights. Table recreation and deletion can cause data loss, inconsistent query results, high job-queue/database load, or service disruption.

## Evidence / context

Cargo documentation states that `recreatecargodata` is given to sysops by default and can be assigned to a dedicated group. Cargo 3.9.4 added a create-missing-tables-only maintenance option and prevents `cargoRecreateData.php` from handling the same page more than once.

## Recommended fixes

- Grant `recreatecargodata` and `deletecargodata` only to a small Cargo-admin group; do not grant these rights to ordinary editors.
- Prefer command-line maintenance under controlled change windows for large recreations, with backups and monitoring.
- Use replacement-table workflows where practical so the current table remains available until the rebuilt table is validated and switched.
- Require change tickets / peer review for destructive Cargo operations in production.

## Validation

- Use Special:ListGroupRights (or equivalent configuration review) to verify only intended groups hold Cargo destructive rights.
- Perform a non-production recreation and confirm job queues, DB load, and rollback procedures behave as expected.
- Verify backups include required Cargo and MediaWiki helper tables before destructive maintenance.

---

[← Previous: Template/parser-function abuse](06-template-parser-function-abuse.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Excessive DB privilege →](08-excessive-db-privilege.md)
