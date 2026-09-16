# 8. Incident response for suspected Cargo compromise

1. Disable or sharply restrict `runcargoqueries` and rate-limit Cargo query/export traffic while preserving evidence.
2. Capture the exact Cargo/MediaWiki versions and commit hashes, web access logs, MediaWiki logs, DB audit/slow-query logs, and relevant reverse-proxy/WAF logs.
3. If SQL injection is suspected, isolate or rotate the Cargo database credential, inspect grants, and review both Cargo data and core MediaWiki data for unauthorized access or changes according to the actual DB privilege boundary.
4. Patch to a fixed supported release/branch and verify the security patch commit is present.
5. If XSS is suspected, search stored Cargo values, template histories, and recently modified pages for malicious payloads; upgrading alone does not remove hostile data already stored.
6. Rebuild/recreate affected Cargo tables only after preserving forensic data and confirming the source wiki/template content is clean.
7. Invalidate/rotate any API keys or secrets that could have been disclosed through Cargo-rendered content or detailed errors.
8. Restore query access in stages and monitor for recurrence.

---

[← Previous: Validation test plan](07-validation-test-plan.md) | [Back to README](../README.md) | [Next: Implementation checklist →](09-implementation-checklist.md)
