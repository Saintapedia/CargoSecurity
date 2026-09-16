# 4. Public interactive query access

**Severity:** High

## Risk

Cargo's `runcargoqueries` right is true for everyone by default. That exposes interactive query and drill-down capabilities unless administrators explicitly override the default.

## Evidence / context

The official installation documentation states that `runcargoqueries` governs Special:CargoQuery and Special:Drilldown and is true for everyone by default. Cargo 3.8 added `runcargoqueries` permission checking to the querying API.

## Recommended fixes

- Set `runcargoqueries=false` for the `*` group (anonymous users).
- For enterprise deployments, also set `runcargoqueries=false` for ordinary authenticated users and grant it only to a dedicated `cargo-query` group with a documented business need.
- Add reverse-proxy/WAF rate limits to Special:CargoQuery, Special:Drilldown, and Cargo API traffic even after permission restrictions are applied.
- Review group membership periodically and remove stale access.

## Validation

- As anonymous and ordinary users, confirm Special:CargoQuery and Special:Drilldown return a permission failure.
- Test the Cargo querying API with the same low-privilege accounts and confirm permission enforcement on the installed version.
- Confirm only the intended group can use the interactive query interfaces.

## Implementation note

Do not assume `runcargoqueries` governs every parser-function query embedded in ordinary wiki pages. Embedded `#cargo_query` output is part of page rendering and must be reviewed through template/page-edit permissions and authorization testing.

`Special:CargoQuery` and `Special:Drilldown` (and the query/autocomplete APIs) all check the identical `runcargoqueries` right — confirmed directly in Cargo's source (`SpecialCargoQuery.php`, `CargoSpecialDrilldown.php`, `CargoQueryAPI.php`, `CargoQueryAutocompleteAPI.php`). There is no built-in way to make one public while keeping the other restricted. If a deployment needs Drilldown to stay public for legitimate browsing while restricting arbitrary CargoQuery use, that split has to be enforced outside Cargo's own permission system — for example by path-specific rate limiting/blocking at the reverse proxy or WAF (see [Reverse proxy / WAF controls](../06-reverse-proxy-waf.md)) rather than via `$wgGroupPermissions`.

---

[← Previous: Denial of service](03-denial-of-service.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Authorization mismatch →](05-authorization-mismatch.md)
