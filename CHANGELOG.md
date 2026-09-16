# Changelog

## Revision 1.1 — September 14, 2026

| Change | Updated position | Why it changed |
|---|---|---|
| Stable version | Use Cargo 3.9.4 or a later supported stable release. | MediaWiki lists 3.9.4, released August 24, 2026, as the latest stable Cargo version. |
| Approval posture | "Approve only with compensating controls" rather than a blanket "generally reasonable" statement. | Recent SQL-injection and stored-XSS history justifies a more prescriptive enterprise baseline. |
| Database isolation | Treat separate Cargo database + separate credential as a hardening requirement for enterprise deployments. | Cargo documentation explicitly recommends a separate database to reduce security and performance blast radius. |
| Query permissions | Disable `runcargoqueries` for anonymous and ordinary users unless there is a documented need. | The right is true for everyone by default and controls Special:CargoQuery / Special:Drilldown; Cargo 3.8 also added permission checking to the querying API. |
| Query controls | Retain a low result ceiling and add execution timeouts / DB controls. | Cargo defaults to a 5,000-row maximum and no execution timeout; the built-in execution timeout is MySQL/MariaDB only. |
| Security advisories | Retain SQL-injection and XSS findings; clarify version-metadata inconsistencies. | Some 2026 CVE records describe MediaWiki release branches while OSV/CPE mapping references Cargo 3.9.1. Patch presence should be verified, not inferred from a single version field. |
