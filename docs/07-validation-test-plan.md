# 7. Validation test plan

All tests share the same pass criterion: the expected restriction/control works without breaking approved use.

| Test | Procedure |
|---|---|
| Version and patch verification | Confirm Cargo reports/records 3.9.4 or later, record the commit hash, and map applicable CVE patches to the deployed branch. |
| Anonymous access test | Verify Special:CargoQuery, Special:Drilldown, and Cargo querying API calls fail for anonymous users. |
| Ordinary-user access test | Verify ordinary authenticated users cannot use interactive Cargo querying unless explicitly approved. |
| Cargo-admin rights test | Verify only the intended Cargo-admin group has `recreatecargodata`/`deletecargodata`. |
| DB separation test | Using the Cargo DB credential, verify Cargo schema operations work and MediaWiki core table access fails. |
| Timeout test | Run a deliberately expensive but non-destructive query in staging and confirm the configured DB/application timeout ends it. |
| Result-limit test | Request more than the maximum allowed results and confirm the effective ceiling is enforced. |
| XSS test | Store representative hostile-looking strings and confirm they render as inert text or are rejected across used formats. |
| Authorization test | Create restricted test records and attempt to recover them through pages, special pages, APIs, drilldowns, and exports. |
| Rate-limit test | Generate a controlled burst of query/export requests and verify reverse-proxy/WAF throttles activate. |
| Error-disclosure test | Break the Cargo DB connection in staging and confirm reader-facing output does not expose connection secrets. |
| Monitoring test | Confirm alerting triggers for slow Cargo queries, query-error bursts, destructive Cargo actions, and abnormal export volume. |

---

[← Previous: Reverse proxy / WAF controls](06-reverse-proxy-waf.md) | [Back to README](../README.md) | [Next: Incident response →](08-incident-response.md)
