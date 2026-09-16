# 13. File, display, map, and export format handling

**Severity:** Medium

## Risk

Cargo renders data through many formats, including gallery/slideshow/zip, maps, calendars, feeds, and exports. Each renderer has its own escaping and data-handling behavior; some historical Cargo fixes specifically addressed escaping in these formats.

## Evidence / context

Cargo 3.9.3 included escaping fixes for field names and file names in gallery, slideshow, and zip formats. Cargo also supports external map services and spreadsheet export dependencies, which introduce additional data-flow and dependency considerations.

## Recommended fixes

- Upgrade to 3.9.4 or later and test every display/export format actually enabled on the wiki with hostile-looking values.
- Disable or avoid formats and third-party map services that are not required, reducing both attack surface and external data disclosure.
- Protect map/API keys and avoid embedding secrets in wikitext or client-visible configuration.
- Keep PhpSpreadsheet and other optional export dependencies patched if spreadsheet export is enabled.

## Validation

- Test file names containing quotes, HTML metacharacters, long strings, path-like segments, and unusual Unicode in gallery/slideshow/zip output.
- Inspect browser/network traffic from map formats to identify data sent to third parties.
- Run dependency/security scans for optional export libraries used by the deployment.

---

[← Previous: Broad SQL-function capability](12-broad-sql-function-capability.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Logging, detection, response →](14-logging-detection-response.md)
