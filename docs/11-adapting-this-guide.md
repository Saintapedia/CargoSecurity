# 11. Adapting this guide to a specific wiki

This guide is intentionally written to apply to any MediaWiki Cargo deployment, not just one wiki. To get value from it for a specific wiki — including Saintapedia — localize it rather than editing the generic guide in place.

## Localize, don't fork

- Copy [`09-implementation-checklist.md`](09-implementation-checklist.md) into a **private** tracking document (an internal wiki page, ticket, or private repo) and mark each item done / in progress / not applicable for that deployment.
- Record the deployment's actual values next to each item — chosen `$wgCargoMaxQueryLimit`, group names, database host/schema names, timeout values — in that private tracker, not in this public repo.
- Keep secrets, hostnames, and any detail that would help an attacker (exact patch status, unpatched findings) out of anything public. Reference where the real values live (a secret manager, an internal runbook) instead of pasting them here.

## Fit the risk matrix to the deployment

- Revisit [`02-risk-matrix.md`](02-risk-matrix.md) against the wiki's actual threat model: is it public or private, does it store any sensitive/regulated data in Cargo tables, is it internet-facing? Priorities may shift accordingly (see [Authorization mismatch](issues/05-authorization-mismatch.md) in particular for data-sensitivity questions).
- Note which of the 14 issues are most relevant given the wiki's actual Cargo usage (e.g. a wiki with no map/export formats enabled can deprioritize [issue 13](issues/13-file-display-export-formats.md)).

## Track drift over time

- Record the deployment's exact Cargo commit hash and MediaWiki version per [Version drift](issues/11-version-drift.md), and recheck it against this guide's [References](10-references.md) as new CVEs are published — this guide's version references (3.9.4 as of the 2026-09-14 revision) will age.
- Assign an owner and a review cadence (e.g. quarterly, or on every Cargo/MediaWiki upgrade) for re-running the [validation test plan](07-validation-test-plan.md).

## For Saintapedia specifically

Use the steps above to produce Saintapedia's own private deployment-status tracker rather than adding Saintapedia-specific configuration to this repo. This keeps the guide reusable for other MediaWiki Cargo deployments while still giving Saintapedia a concrete way to apply it.

---

[← Previous: References](10-references.md) | [Back to README](../README.md)
