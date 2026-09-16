# 6. Template and parser-function abuse

**Severity:** High

## Risk

Cargo functionality is commonly driven by templates containing `#cargo_declare`, `#cargo_attach`, `#cargo_store`, `#cargo_query`, and `#cargo_compound_query`. An editor who can alter trusted Cargo templates may be able to change data schemas, query logic, display behavior, or persistent stored values.

## Evidence / context

Restricting Special:CargoQuery alone does not neutralize Cargo queries embedded in page/template rendering. Template modification is therefore part of the Cargo security boundary.

## Recommended fixes

- Protect Cargo declaration/query templates and relevant Lua modules; allow edits only by a template-maintainer or similarly trusted group.
- Use code review / approved revisions for changes to templates that declare schemas, store values, construct WHERE/JOIN expressions, or select display formats.
- Avoid passing unrestricted user-supplied text directly into query components. Constrain parameters to enumerated values or tightly validated formats where possible.
- Inventory all Cargo parser functions in templates and remove unused or legacy query pathways.

## Validation

- Search the Template and Module namespaces for `cargo_declare`, `cargo_attach`, `cargo_store`, `cargo_query`, `cargo_compound_query`, and `cargo_display_map`.
- Attempt to edit high-impact templates with an ordinary editor account and confirm protection is enforced.
- Review template history for unexpected changes and ensure changes are attributable to approved maintainers.

---

[← Previous: Authorization mismatch](05-authorization-mismatch.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Privileged table recreation →](07-privileged-table-recreation.md)
