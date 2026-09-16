# CargoSecurity

Security hardening guidance for the [MediaWiki Cargo extension](https://www.mediawiki.org/wiki/Extension:Cargo) — the SQL-like structured-data/querying extension used on Saintapedia and other MediaWiki wikis. This is **not** related to Rust's Cargo package manager.

- **Revision:** 1.1 — updated September 14, 2026
- **Current stable Cargo release reviewed:** 3.9.4

## Recommended enterprise posture

> Approve Cargo only with compensating controls: current stable code, a separate Cargo database and credential, restricted query permissions, bounded query execution, protected Cargo templates, endpoint rate limiting, and monitoring. Cargo should not be treated as a confidentiality boundary for sensitive data without explicit authorization testing.

## Executive summary

Overall risk: **Medium to High** before hardening; **Medium or lower** for typical public, non-sensitive use after the controls in this guide are implemented and verified.

- Cargo adds SQL-like querying, drill-down interfaces, parser functions, APIs, exports, table-management operations, and multiple display formats. Those capabilities materially expand the MediaWiki attack surface.
- The highest-consequence failure mode is SQL injection when Cargo shares the primary MediaWiki database or a broadly privileged database credential. Separate schema/account isolation sharply reduces the blast radius.
- Stored XSS remains important because malicious values can persist and execute in the browsers of later readers or administrators. Upgrading fixes vulnerable rendering paths but does not automatically prove that previously stored values are benign.
- Denial-of-service risk exists even when returned row counts are small because joins, sorting, grouping, range filters, and other operations can consume substantial database work before the result limit is applied.
- Cargo is best suited to public or low-sensitivity structured data. For confidential data, page-level authorization and Cargo row visibility must be tested independently across special pages, APIs, parser-function output, and export routes.

> **Important version note.** As of September 14, 2026, the MediaWiki Cargo page identifies 3.9.4 as stable. Do not run an unpinned master checkout in production merely to be "latest"; use a supported release/tag or a release branch with documented security backports and verify that relevant security patches are present.

## Contents

1. [Security posture and scope](docs/01-posture-and-scope.md)
2. [Risk matrix](docs/02-risk-matrix.md)
3. Detailed security issues and fixes (14 issues) — [docs/issues/](docs/issues/)
4. [Hardened LocalSettings.php baseline](docs/04-hardened-localsettings-baseline.md)
5. [Database isolation and least privilege](docs/05-database-isolation.md)
6. [Reverse proxy / WAF controls](docs/06-reverse-proxy-waf.md)
7. [Validation test plan](docs/07-validation-test-plan.md)
8. [Incident response for suspected Cargo compromise](docs/08-incident-response.md)
9. [Implementation checklist](docs/09-implementation-checklist.md)
10. [References and source notes](docs/10-references.md)
11. [Adapting this guide to a specific wiki](docs/11-adapting-this-guide.md)

See also: [CHANGELOG.md](CHANGELOG.md) for the revision history, and [source/](source/) for the original document this repo was derived from.

## Conclusion

Cargo can be deployed safely for many public or low-sensitivity structured-data use cases, but it should be treated as an application-level data query service rather than a passive template helper. The recommended approval condition is: current supported code, isolated Cargo database credentials, restricted interactive query rights, bounded query cost, protected Cargo templates, explicit authorization testing, and operational monitoring. For confidential or regulated data, validate Cargo as a separate authorization surface before approval.
