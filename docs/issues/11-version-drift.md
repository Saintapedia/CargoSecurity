# 11. Version drift, unstable master, or unverified security backports

**Severity:** High

## Risk

Running old Cargo releases leaves known vulnerabilities exposed; running an unpinned master can introduce unreviewed changes. Distribution packages and MediaWiki release branches may carry backported fixes that are not obvious from the displayed Cargo version.

## Evidence / context

Cargo's installation page says `git pull` can update to the latest code but warns it may not be a stable release. Current stable Cargo is 3.9.4. Wikimedia's July 2026 extension-security supplement recommends updating affected extensions to current master or the relevant supported release branch.

## Recommended fixes

- Pin production to Cargo 3.9.4 or a later supported stable tag, or to an organization-approved release branch with documented backports.
- Track Wikimedia security announcements, Cargo release history, CVE/OSV records, and package-vendor security notices.
- Record the exact Cargo commit hash in the system inventory so security patches can be verified even when version metadata is ambiguous.
- Test upgrades in staging, including schema updates, query behavior, exports, and permissions, before production promotion.

## Validation

- Record Special:Version output plus the filesystem/repository commit and compare them to the approved baseline.
- Check that CVE patch commits relevant to your branch are ancestors of the deployed commit where practical.
- Confirm unattended package updates cannot silently replace a pinned Cargo release with a different branch.

---

[← Previous: Error/credential disclosure](10-error-credential-disclosure.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Broad SQL-function capability →](12-broad-sql-function-capability.md)
