# 2. Stored/reflected XSS and unsafe output rendering

**Severity:** High

## Risk

Cargo stores editor-controlled structured values and renders them through multiple display formats. Stored XSS can execute later in another user's browser, including an administrator's browser, and can therefore cross privilege boundaries.

## Evidence / context

CVE-2026-58519 affected Cargo before 3.9.1 and allowed stored XSS. Several other 2026 Cargo XSS issues affected versions before 3.8.7, including CVE-2026-39837, CVE-2026-39840, and CVE-2026-39841. Cargo 3.9.3 also included escaping fixes for field names and file names in gallery, slideshow, and zip formats.

## Recommended fixes

- Upgrade to Cargo 3.9.4 or later and keep MediaWiki core, skins, and dependent libraries on supported security releases.
- Review and protect templates that store Cargo values; do not let untrusted editors inject arbitrary HTML/URLs into fields that are later rendered by high-privilege users.
- Deploy a restrictive Content Security Policy as defense in depth, especially limiting `script-src`, `object-src`, and unsafe inline execution where feasible.
- After upgrading from an affected release, review suspicious stored Cargo values and recent template edits because upgrading does not automatically prove historical data is safe.

## Validation

- Test representative display formats with encoded HTML, javascript-like URLs, quotes, angle brackets, and malformed file names; output should be escaped or rejected as appropriate.
- Use a low-privilege test account to store values, then view the result with a separate browser profile and confirm no script executes.
- Review browser developer tools / CSP reports for blocked inline script or unexpected third-party script execution.

---

[← Previous: SQL injection](01-sql-injection.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Denial of service →](03-denial-of-service.md)
