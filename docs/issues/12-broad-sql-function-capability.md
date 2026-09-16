# 12. Overly broad SQL-function and query capability

**Severity:** Medium-High

## Risk

Cargo supports SQL-like expressions and a configurable set of allowed SQL functions. Every additional query feature increases validation complexity and can increase CPU cost or expose edge cases.

## Evidence / context

Cargo exposes `$wgCargoAllowedSQLFunctions`. Complex functions, joins, groupings, ordering, and range filters can be legitimate but should be treated as query execution capability rather than simple page display.

## Recommended fixes

- Keep `$wgCargoAllowedSQLFunctions` to the minimum set actually required; do not expand the allowlist merely for convenience.
- Prefer predefined templates/queries over free-form user construction for common reporting use cases.
- Bound query execution time and result count regardless of the allowed function list.
- Review new query features or functions as a security change requiring performance and input-validation testing.

## Validation

- Inventory the effective allowed SQL functions and compare them to documented business requirements.
- Test representative worst-case function/grouping queries under the configured timeout.
- Review query templates for string concatenation or dynamic function names derived from untrusted input.

---

[← Previous: Version drift](11-version-drift.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: File/display/export formats →](13-file-display-export-formats.md)
