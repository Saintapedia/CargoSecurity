# 4. Hardened LocalSettings.php baseline

The following is an enterprise starting point, not a universal drop-in configuration. Tune values to tested workload requirements and place these settings after Cargo is loaded where required by the extension documentation.

```php
wfLoadExtension( 'Cargo' );

// Interactive query access: deny by default.
$wgGroupPermissions['*']['runcargoqueries'] = false;
$wgGroupPermissions['user']['runcargoqueries'] = false;
$wgGroupPermissions['cargo-query']['runcargoqueries'] = true;

// Cargo administration: explicit least privilege.
$wgGroupPermissions['*']['recreatecargodata'] = false;
$wgGroupPermissions['*']['deletecargodata'] = false;
$wgGroupPermissions['user']['recreatecargodata'] = false;
$wgGroupPermissions['user']['deletecargodata'] = false;
$wgGroupPermissions['cargoadmin']['recreatecargodata'] = true;
$wgGroupPermissions['cargoadmin']['deletecargodata'] = true;

// Query output limits.
$wgCargoDefaultQueryLimit = 100;
$wgCargoMaxQueryLimit = 500;

// MySQL/MariaDB only: execution limit in milliseconds.
$wgCargoQueryMaxExecutionTime = 3000;

// Production error handling.
$wgShowExceptionDetails = false;

// Separate Cargo database (example placeholders).
$wgCargoDBserver = 'cargo-db.internal.example';
$wgCargoDBname = 'wiki_cargo';
$wgCargoDBuser = 'wiki_cargo';
$wgCargoDBpassword = 'LOAD_FROM_SECRET_MANAGEMENT';
$wgCargoDBtype = $wgDBtype;
```

> **PostgreSQL note.** Cargo documents `$wgCargoQueryMaxExecutionTime` as MySQL/MariaDB-only. For PostgreSQL, enforce an appropriate `statement_timeout` on the Cargo database role or database and validate it under representative query load.

> **API note.** Cargo 3.8 added `runcargoqueries` permission checking to the querying API. Still test the exact deployed API/export routes, because embedded parser-function output and non-query export paths may follow different authorization logic.

---

[← Previous: Detailed issues](issues/) | [Back to README](../README.md) | [Next: Database isolation →](05-database-isolation.md)
