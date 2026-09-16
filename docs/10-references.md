# 10. References and source notes

Sources checked for this revision on September 14, 2026. URLs are included for administrative verification and should be rechecked during future security reviews.

| Source | URL | Use in this guide |
|---|---|---|
| MediaWiki - Extension:Cargo | https://www.mediawiki.org/wiki/Extension:Cargo | Current stable version, supported MediaWiki versions, configuration settings, rights, interfaces. |
| MediaWiki - Cargo version history | https://www.mediawiki.org/wiki/Extension:Cargo/Version_history | 3.9.4 release date; 3.9.1 timeout setting; 3.9.3 escaping fixes; Cargo 3.8 API permission check. |
| MediaWiki - Cargo download and installation | https://www.mediawiki.org/wiki/Extension:Cargo/Download_and_installation | Separate database recommendation; runcargoqueries default; exception-details credential warning; stable-vs-master warning. |
| MediaWiki - Cargo querying data | https://www.mediawiki.org/wiki/Extension:Cargo/Querying_data | Default query limit 100 and maximum query limit 5,000. |
| MediaWiki - Cargo FAQ | https://www.mediawiki.org/wiki/Extension:Cargo/FAQ | SQL-injection validation discussion and resource-exhaustion warning. |
| MediaWiki - Handling web crawlers | https://www.mediawiki.org/wiki/Manual:Handling_web_crawlers | Cargo special pages identified as expensive; runcargoqueries example. |
| MediaWiki - Cargo storing data | https://www.mediawiki.org/wiki/Extension:Cargo/Storing_data | recreatecargodata behavior, group assignment, maintenance script behavior. |
| Wikimedia Security - July 2026 extension/skin security supplement | https://lists.wikimedia.org/hyperkitty/list/mediawiki-announce%40lists.wikimedia.org/message/NWU4FJO6FSDPKCD7MK55356QJTFT47JH/ | Security release guidance and CVE-2026-14363 reference. |
| NVD - CVE-2025-62655 | https://nvd.nist.gov/vuln/detail/CVE-2025-62655 | Cargo SQL injection. |
| OpenCVE - CVE-2026-58521 | https://opencve.alliance.unm.edu/cve/CVE-2026-58521 | Cargo SQL injection via year-range filter; CVSS and vendor record. |
| OpenCVE - CVE-2026-14363 | https://opencve.alliance.unm.edu/cve/CVE-2026-14363 | Cargo Special:Drilldown SQL injection; vendor record. |
| OSV - CVE-2026-58521 | https://osv.dev/vulnerability/CVE-2026-58521 | Additional normalized vulnerability metadata and Cargo CPE mapping. |
| OSV - CVE-2026-14363 | https://osv.dev/vulnerability/CVE-2026-14363 | Additional normalized vulnerability metadata and Cargo CPE mapping. |
| NVD - CVE-2026-58519 | https://nvd.nist.gov/vuln/detail/CVE-2026-58519 | Stored XSS affecting Cargo before 3.9.1. |
| NVD - CVE-2026-39841 | https://nvd.nist.gov/vuln/detail/CVE-2026-39841 | Stored XSS affecting Cargo before 3.8.7. |
| NVD - CVE-2026-39840 | https://nvd.nist.gov/vuln/detail/CVE-2026-39840 | XSS affecting Cargo before 3.8.7. |

---

[← Previous: Implementation checklist](09-implementation-checklist.md) | [Back to README](../README.md)
