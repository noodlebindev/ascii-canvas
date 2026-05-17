# comparison-table — full example

**Topic:** PostgreSQL vs MySQL vs SQLite across 6 dimensions
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
PostgreSQL vs MySQL vs SQLite

┌──────────────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
│ Dimension            │     PostgreSQL        │       MySQL          │       SQLite         │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Schema flexibility   │ High — JSONB, arrays, │ Medium — JSON col,   │ Low — dynamic types, │
│                      │ custom types          │ limited arrays       │ no ADD COLUMN fully  │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Replication          │ ✓  streaming+logical  │ ✓  primary/replica   │ ✗  file-level only   │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Embedded use         │ ✗  needs server       │ ✗  needs server      │ ✓  single .db file   │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Concurrent writes    │ ✓  MVCC row-level     │ ~  InnoDB MVCC,      │ ~  WAL helps but     │
│                      │                      │    DDL table locks   │    still serializes  │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ JSON support         │ ✓  JSONB + operators  │ ~  JSON text col,    │ ~  JSON1 extension,  │
│                      │                      │    partial index     │    limited ops       │
├──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Operational overhead │ Medium — autovacuum   │ Medium — broad host  │ Low — file copy =    │
│                      │ tuning required       │ support, simpler     │ backup, zero config  │
└──────────────────────┴──────────────────────┴──────────────────────┴──────────────────────┘

Legend: ✓ strong   ~ partial / conditional   ✗ not supported
```

---

## Why this works

- Multi-line cells for "Schema flexibility" and "Concurrent writes" carry detail that a single ✓/✗ symbol would miss, but every cell wraps strictly within its column width so no line exceeds 100 cols.
- Six dimensions cover the decision-critical axes for a developer choosing a database — not every axis (no indexing speed, no community size), just the ones that determine architectural fit.
- The ✓ / ~ / ✗ legend at the bottom prevents ambiguity for the "~" values, which otherwise look like a data error without context.

## ASCII variant (if structurally different from Unicode)

```
PostgreSQL vs MySQL vs SQLite

+----------------------+----------------------+----------------------+----------------------+
| Dimension            |     PostgreSQL        |       MySQL          |       SQLite         |
+----------------------+----------------------+----------------------+----------------------+
| Schema flexibility   | High -- JSONB, arrays | Medium -- JSON col,  | Low -- dynamic types |
|                      | custom types          | limited arrays       | no ADD COLUMN fully  |
+----------------------+----------------------+----------------------+----------------------+
| Replication          | Y  streaming+logical  | Y  primary/replica   | N  file-level only   |
+----------------------+----------------------+----------------------+----------------------+
| Embedded use         | N  needs server       | N  needs server      | Y  single .db file   |
+----------------------+----------------------+----------------------+----------------------+
| Concurrent writes    | Y  MVCC row-level     | ~  InnoDB MVCC,      | ~  WAL helps but     |
|                      |                      |    DDL table locks   |    still serializes  |
+----------------------+----------------------+----------------------+----------------------+
| JSON support         | Y  JSONB + operators  | ~  JSON text col,    | ~  JSON1 extension,  |
|                      |                      |    partial index     |    limited ops       |
+----------------------+----------------------+----------------------+----------------------+
| Operational overhead | Medium -- autovacuum  | Medium -- broad host | Low -- file copy =   |
|                      | tuning required       | support, simpler     | backup, zero config  |
+----------------------+----------------------+----------------------+----------------------+

Legend: Y strong   ~ partial / conditional   N not supported
```
