# 9. Implementation checklist

- [ ] Cargo is pinned to 3.9.4 or a later supported stable release / approved patched branch.
- [ ] Exact Cargo commit hash is recorded in the software inventory.
- [ ] Separate Cargo database/schema is configured.
- [ ] Cargo uses a unique least-privileged database credential with no core MediaWiki table access.
- [ ] Anonymous `runcargoqueries` is disabled.
- [ ] Ordinary-user `runcargoqueries` is disabled unless there is a documented need.
- [ ] Dedicated `cargo-query` group exists only if interactive querying is required.
- [ ] `recreatecargodata` and `deletecargodata` are restricted to a small administrative group.
- [ ] Cargo declaration/query templates and relevant Lua modules are protected/reviewed.
- [ ] `$wgCargoMaxQueryLimit` is reduced from the default 5,000 to a tested value.
- [ ] MySQL/MariaDB uses `$wgCargoQueryMaxExecutionTime`, or PostgreSQL uses an equivalent DB timeout.
- [ ] `$wgShowExceptionDetails` is false in production.
- [ ] Reverse proxy/WAF limits Cargo query, drill-down, API, and export abuse.
- [ ] CSP is deployed where feasible as XSS defense in depth.
- [ ] Sensitive-data authorization has been tested across every Cargo retrieval path.
- [ ] Logging/alerting covers slow queries, query errors, exports, and destructive Cargo operations.
- [ ] Incident-response and rollback procedures have been tested.

---

[← Previous: Incident response](08-incident-response.md) | [Back to README](../README.md) | [Next: References →](10-references.md)
