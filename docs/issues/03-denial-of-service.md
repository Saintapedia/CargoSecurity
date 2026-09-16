# 3. Denial of service and resource exhaustion

**Severity:** High

## Risk

Joins, sorting, grouping, range filters, calculations, and large intermediate result sets can consume database CPU, memory, temporary space, or connections. A small final result does not guarantee a cheap query.

## Evidence / context

Cargo's FAQ acknowledges that malicious or accidental queries can slow or crash the database/server. MediaWiki's crawler guidance identifies Special:CargoQuery and Special:Drilldown as expensive pages. Cargo defaults to a maximum query result limit of 5,000 and no execution timeout.

## Recommended fixes

- Lower `$wgCargoMaxQueryLimit` from the 5,000 default to a business-justified value such as 500 or less.
- For MySQL/MariaDB, set `$wgCargoQueryMaxExecutionTime` (for example 3000-5000 ms) and tune after measuring legitimate workloads.
- For PostgreSQL, enforce `statement_timeout` or an equivalent database/role-level limit because Cargo's built-in execution-time setting is documented for MySQL/MariaDB only.
- Rate-limit Cargo query/drill-down/API/export endpoints at the reverse proxy or WAF and consider hosting the Cargo database on separate database infrastructure for high-risk deployments.

## Validation

- Run load tests using worst-case legitimate queries and verify timeouts terminate expensive queries without exhausting worker pools.
- Monitor slow-query logs, DB CPU, temporary table usage, lock waits, and web request latency during tests.
- Verify anonymous clients are rate-limited and cannot generate sustained expensive traffic.

---

[← Previous: Stored/reflected XSS](02-stored-reflected-xss.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Public query access →](04-public-query-access.md)
