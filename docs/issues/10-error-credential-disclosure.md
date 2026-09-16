# 10. Detailed errors and database credential disclosure

**Severity:** High

## Risk

When a separate Cargo database is configured, a failed connection can include connection parameters in a stack trace. Exposing those details to readers can disclose the Cargo database password.

## Evidence / context

The Cargo installation documentation explicitly warns that if the database cannot be accessed while `$wgShowExceptionDetails` is true, readers may see a stack trace containing the Cargo DB server, database name, user, and password.

## Recommended fixes

- Keep `$wgShowExceptionDetails=false` in production.
- Store database secrets outside web-accessible document roots and use deployment secret-management controls appropriate to the hosting environment.
- Restrict application/error logs that may contain connection details and establish log-retention/access rules.
- Rotate the Cargo database credential immediately if it may have appeared in a reader-visible stack trace or exposed log.

## Validation

- In a non-production environment, deliberately misconfigure the Cargo DB endpoint and verify the user-facing error does not reveal credentials.
- Search production web logs and monitoring systems for accidental plaintext copies of Cargo DB credentials.
- Verify file permissions on LocalSettings.php and any included secret files.

---

[← Previous: API/export enumeration](09-api-export-enumeration.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Version drift →](11-version-drift.md)
