# Category Catalog, Rules & SQL Matrix

## Software & Infrastructure Categories (`17` Sections)

| Section | Focus | Section | Focus |
| :--- | :--- | :--- | :--- |
| `High-Availability` | Replication, Patroni, failover | `Platforms` | Unified spatial/time-series stacks |
| `Backups` | pgBackRest, Barman, WAL archiving | `Work Queues` | `SKIP LOCKED` / `LISTEN` queues |
| `GUI` | Desktop and web SQL managers | `Optimization` | `EXPLAIN`, index advisors, tuning |
| `Distributions` | Packaged Postgres bundles | `Utilities` | Migrations, poolers, ETL tools |
| `CLI` | `psql`, TUI tools, schema diffs | `Language bindings` | Client drivers across 17 languages |
| `Server` | PostgreSQL-compatible engines | `PaaS` | Managed cloud PostgreSQL providers |
| `Security` | Proxy encryption & SQL firewall | `Docker images` | Containerized PostgreSQL distributions |
| `Monitoring` | Exporters, APM, query metrics | `Kubernetes` | Operators (CNPG, Zalando, KubeDB) |
| `Extensions` | Citus, PostGIS, TimescaleDB, pgAudit | — | — |

## Learning & Community Sections (`10` Sections)

`Tutorials`, `Blogs`, `Books`, `Documentation`, `Newsletters`, `Podcasts`, `Videos`, `Community`, `Roadmaps`, `External lists`.

## Mandatory Contribution Format (`CONTRIBUTING.md`)

- **Entry pattern:** `[item](link) - description.` (`1` item per PR, `1` link per item, English only).
- **Licensing label:** Append `(Commercial Software)` unless covered by an FSF-recognized open-source license.
- **Disallowed items:** Slides, videos, individual SQL snippets, unmaintained prototypes, and documentation-only tools.

## Legacy Link-Checker Configuration (`.travis.yml`)

- Runs `awesome_bot README.md --white-list psequel,elements.heroku.com/addons/heroku-postgresql,pgconfig,en.wikipedia.org/wiki/PostgreSQL,www.postgresql.org` on Ruby `2.2` (deprecated Travis CI; local verification uses `tests/test_docs_tutorials_howtos.py`).

## PostgreSQL SQL Cheat-Sheet Feature Summary

| Construct | Keyword / Operator | Primary Purpose |
| :--- | :--- | :--- |
| **CTE** | `WITH ... AS (...)` | Modular named subqueries and recursive queries |
| **Window Function** | `OVER (PARTITION BY ... ORDER BY ...)` | Row ranking and moving aggregates without collapsing rows |
| **UPSERT** | `INSERT ... ON CONFLICT (...) DO UPDATE` | Atomic idempotent insert-or-update handling |
| **JSONB** | `@>`, `->>`, `::jsonb` | Indexed containment and structured key extraction |
| **Arrays** | `ARRAY[...]`, `= ANY (...)` | Multi-value columns and membership predicates |
