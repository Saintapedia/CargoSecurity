# 2. Risk matrix

| # | Issue | Priority | Primary impact |
|---|---|---|---|
| 1 | [SQL injection](issues/01-sql-injection.md) | Critical | Database confidentiality, integrity, availability |
| 2 | [Stored/reflected XSS and unsafe output rendering](issues/02-stored-reflected-xss.md) | High | User/session compromise; privileged-browser actions |
| 3 | [Denial of service / expensive queries](issues/03-denial-of-service.md) | High | Database and wiki availability |
| 4 | [Public interactive query access](issues/04-public-query-access.md) | High | Attack surface, enumeration, resource abuse |
| 5 | [Authorization mismatch / excessive data exposure](issues/05-authorization-mismatch.md) | High | Confidentiality and bulk discovery |
| 6 | [Template and parser-function abuse](issues/06-template-parser-function-abuse.md) | High | Query execution, data integrity, persistent attack surface |
| 7 | [Privileged table recreation/deletion](issues/07-privileged-table-recreation.md) | High | Integrity and availability |
| 8 | [Excessive database privilege / shared database blast radius](issues/08-excessive-db-privilege.md) | Critical | Full wiki DB impact if query boundary fails |
| 9 | [API/export enumeration and bulk extraction](issues/09-api-export-enumeration.md) | Medium-High | Confidentiality, scraping, resource use |
| 10 | [Detailed error / credential disclosure](issues/10-error-credential-disclosure.md) | High | Database credential compromise |
| 11 | [Version drift, unstable master, or unverified backports](issues/11-version-drift.md) | High | Known-vulnerability exposure |
| 12 | [Overly broad SQL-function/query capability](issues/12-broad-sql-function-capability.md) | Medium-High | Complexity, performance, exploit surface |
| 13 | [File/display/export format handling](issues/13-file-display-export-formats.md) | Medium | XSS/content handling and data leakage |
| 14 | [Insufficient logging, detection, and response](issues/14-logging-detection-response.md) | Medium-High | Longer dwell time and weak forensic visibility |

---

[← Previous: Posture and scope](01-posture-and-scope.md) | [Back to README](../README.md) | [Next: Detailed issues →](issues/)
