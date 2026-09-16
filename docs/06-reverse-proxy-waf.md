# 6. Reverse proxy / WAF controls

Application permissions should be the primary access control. Network controls provide defense in depth and protect availability.

- Rate-limit Special:CargoQuery and Special:Drilldown per IP/account. Use substantially lower anonymous limits than authenticated limits.
- Rate-limit API requests that invoke Cargo queries and bulk exports; consider concurrency limits in addition to request-per-minute limits.
- Set upstream request and response size ceilings appropriate to normal Cargo exports.
- Alert rather than immediately block on new patterns during initial deployment so legitimate administrative operations can be baselined safely.
- Do not rely on robots.txt as a security control; hostile clients are not required to obey it.

---

[← Previous: Database isolation](05-database-isolation.md) | [Back to README](../README.md) | [Next: Validation test plan →](07-validation-test-plan.md)
