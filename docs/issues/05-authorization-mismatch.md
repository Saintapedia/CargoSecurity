# 5. Authorization mismatch and excessive structured-data exposure

**Severity:** High

## Risk

Cargo centralizes data that may previously have been scattered across pages. Structured query, drill-down, and export interfaces can make information far easier to enumerate. Page-level or namespace-level read restrictions may not automatically translate into row-level Cargo authorization semantics.

## Evidence / context

Cargo is a data-query layer, not a general-purpose row-level authorization engine. The primary security concern is aggregation: information that is individually hard to browse can become searchable and exportable at scale.

## Recommended fixes

- Do not store secrets, regulated personal information, or access-controlled records in Cargo unless the authorization model has been explicitly tested for every retrieval path.
- Separate sensitive datasets from public Cargo tables and prefer dedicated applications/datastores when row-level authorization is required.
- Test special pages, APIs, parser-function output, drill-downs, and exports with unauthorized accounts and ensure restricted records cannot be inferred or enumerated.
- Minimize fields stored in Cargo to those needed for the public/authorized use case.

## Validation

- Create test records visible only to a restricted group and attempt to retrieve them through every Cargo interface.
- Search by unique values, ranges, counts, and groupings to detect indirect leakage even when full rows are hidden.
- Review exports for fields that are hidden in the normal page UI but still present in structured data.

---

[← Previous: Public query access](04-public-query-access.md) | [Back to risk matrix](../02-risk-matrix.md) | [Next: Template/parser-function abuse →](06-template-parser-function-abuse.md)
