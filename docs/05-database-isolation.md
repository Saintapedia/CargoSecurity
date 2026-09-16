# 5. Database isolation and least privilege

The separate Cargo database is the single most important blast-radius control for SQL-injection risk. Cargo must be able to create and drop its own data tables, so a read-only account is not generally sufficient; scope the DDL privileges to the Cargo schema rather than granting server-wide rights.

```sql
-- Example for MySQL/MariaDB; adapt to local standards.
CREATE DATABASE wiki_cargo
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;

CREATE USER 'wiki_cargo'@'app-host-or-subnet'
  IDENTIFIED BY 'LONG-RANDOM-SECRET';

GRANT SELECT, INSERT, UPDATE, DELETE,
      CREATE, DROP, INDEX, ALTER
ON wiki_cargo.*
TO 'wiki_cargo'@'app-host-or-subnet';

-- Do NOT grant global privileges such as FILE, PROCESS, SUPER,
-- server administration, or access to the core MediaWiki schema.
```

- Keep the ordinary MediaWiki database account separately least-privileged; Cargo helper tables (including core Cargo metadata/helper tables) remain in the main MediaWiki database.
- Where operationally feasible, use network ACLs so the Cargo credential can connect only to the intended database service and from intended application hosts.
- For very high query volumes or stronger availability isolation, place Cargo data on separate database infrastructure, not merely a separate schema on the same overloaded server.

---

[← Previous: Hardened LocalSettings.php baseline](04-hardened-localsettings-baseline.md) | [Back to README](../README.md) | [Next: Reverse proxy / WAF controls →](06-reverse-proxy-waf.md)
