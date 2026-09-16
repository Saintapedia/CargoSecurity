# 14. Insufficient logging, detection, and incident response

**Severity:** Medium-High

## Risk

Without database, web, and MediaWiki audit visibility, malicious queries may look like ordinary user activity. A vulnerability can therefore be exploited repeatedly before administrators notice unusual query volume, errors, or data access.

## Evidence / context

Cargo creates identifiable special-page/API traffic and database workloads that can be monitored. Security logging is a compensating control because application-layer validation failures cannot be ruled out solely by configuration.

## Recommended fixes

- Log and alert on repeated Cargo query errors, unusually slow Cargo queries, large/rapid exports, repeated drill-down requests, and table recreation/deletion events.
- Retain MediaWiki user/action logs, reverse-proxy logs, DB slow-query/audit logs, and deployment/version records long enough to investigate incidents.
- Define an incident playbook that includes disabling Cargo query access, preserving logs, rotating Cargo DB credentials, patching, and reviewing stored values/templates.
- Baseline normal Cargo traffic and database latency so anomaly thresholds are meaningful.

## Validation

- Generate test alerts for a burst of Special:CargoQuery/Drilldown traffic and an intentionally slow non-production query.
- Confirm Cargo-admin actions can be attributed to a named user/change record.
- Run a tabletop exercise using the incident-response sequence in [Incident response](../08-incident-response.md).

---

[← Previous: File/display/export formats](13-file-display-export-formats.md) | [Back to risk matrix](../02-risk-matrix.md) | [Back to README](../../README.md)
