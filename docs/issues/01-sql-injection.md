# 1. SQL injection in Cargo query paths

**Severity:** Critical

## Risk

Cargo accepts SQL-like query components and converts them into database queries. Publicly disclosed Cargo vulnerabilities include SQL-injection flaws, including CVE-2025-62655, CVE-2026-58521, and CVE-2026-14363. A successful injection is much more damaging when Cargo can reach the primary MediaWiki schema with a broadly privileged account.

## Evidence / context

Wikimedia security advisories and CVE records document SQL-injection issues in Cargo. CVE-2026-58521 concerns a year-range filter; CVE-2026-14363 concerns Special:Drilldown. Some 2026 CVE version strings are expressed as MediaWiki release-branch versions, while OSV/CPE conversion data maps a Cargo fix to 3.9.1; administrators should verify patch presence instead of relying on one metadata field.

## Recommended fixes

- Run Cargo 3.9.4 or a later supported stable release, or a supported release branch with the relevant Cargo security patches confirmed.
- Place Cargo data in a separate database/schema using a separate database credential that has no access to MediaWiki core tables.
- Restrict `runcargoqueries` to a small approved group and do not expose interactive query construction to anonymous users.
- Apply database and application query timeouts so a malicious payload cannot run indefinitely even if validation fails.

## Validation

- Confirm the deployed Cargo commit/tag includes the patches referenced by the applicable Wikimedia security advisories.
- From the Cargo DB account, verify SELECT/DDL access to Cargo data only and verify access to core MediaWiki tables is denied.
- Perform a controlled security test of Special:Drilldown, Special:CargoQuery, and the Cargo query API using malformed filters/field names without running destructive payloads.

## Implementation note

Do not treat the `cargo__` table prefix as equivalent to a database security boundary. Database-level privilege separation is stronger and limits impact if application validation is bypassed.

---

[← Back to risk matrix](../02-risk-matrix.md) | [Next: Stored/reflected XSS →](02-stored-reflected-xss.md)
