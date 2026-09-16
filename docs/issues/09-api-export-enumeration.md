# 9. API, export, and automated enumeration

**Severity:** Medium-High

## Risk

APIs and export formats can enable bulk extraction much faster than normal page browsing. They can also be used to generate repeated expensive queries or retrieve fields users do not notice in the UI.

## Evidence / context

Cargo supports APIs and exports such as CSV/JSON/RSS and spreadsheet-oriented output. Cargo 3.8 added `runcargoqueries` permission checking to the querying API, but export and embedded-query behavior should still be validated for the installed configuration.

## Recommended fixes

- Restrict `runcargoqueries` and verify Cargo API permission behavior on the deployed version.
- Apply per-IP/per-account rate limits to Cargo API and export routes, with stricter limits for unauthenticated traffic.
- Disable or avoid export formats that are not required by the business use case, and review exported field sets for sensitive data.
- Use caching for safe, common read-only outputs rather than repeatedly executing expensive live queries.

## Validation

- Enumerate Cargo-related API modules/routes on the deployed wiki and test them as anonymous, ordinary, and approved users.
- Attempt high-volume export requests in a test environment and verify throttles activate before DB health is affected.
- Inspect representative CSV/JSON/spreadsheet exports for hidden or unintended columns.

---

[← Previous: Excessive DB privilege](08-excessive-db-privilege.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Error/credential disclosure →](10-error-credential-disclosure.md)
