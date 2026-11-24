# Tutorial 1: Explore Curated Categories and Practice PostgreSQL SQL Patterns

In this tutorial, you verify the repository's `27` curated sections, launch an isolated local PostgreSQL `16` container, and execute core SQL syntax patterns referenced under `Tutorials` (`SQL Syntax Cheat Sheet` in commit `87ac763`).

## Prerequisites

- Docker Engine (`20.10` or newer) for the local SQL lab
- Python `3.10` or newer to run local validation checks

## Step 1: Run Repository Structure Checks

Run the local verification suite to confirm TOC anchor coverage and valid Markdown formatting:

```bash
python3 -m unittest discover -s tests -p "test_*.py" -v
```

Expected output shows all tests passing cleanly with zero broken section links.

## Step 2: Launch an Ephemeral PostgreSQL Container

Start an isolated loopback container (`127.0.0.1` only):

```bash
docker run -d --name awesome-pg-lab --rm \
  -p 127.0.0.1:35433:5432 \
  -e POSTGRES_PASSWORD=AwesomePgLab_2026 \
  postgres:16-alpine
```

## Step 3: Practice CTEs, Window Functions, UPSERT, JSONB, and Arrays

Execute representative PostgreSQL queries covering each feature highlighted in the curated `Tutorials` entry:

```sql
CREATE TEMP TABLE curated_tools (
    slug TEXT PRIMARY KEY,
    category TEXT NOT NULL,
    stars INT NOT NULL,
    tags TEXT[] NOT NULL,
    metadata JSONB NOT NULL
);

INSERT INTO curated_tools (slug, category, stars, tags, metadata)
VALUES
    ('patroni', 'High-Availability', 7500, ARRAY['ha', 'etcd'], '{"license": "MIT", "oss": true}'::jsonb),
    ('pgbackrest', 'Backups', 2900, ARRAY['backup', 'wal'], '{"license": "MIT", "oss": true}'::jsonb),
    ('pgcli', 'CLI', 14200, ARRAY['cli', 'autocomplete'], '{"license": "BSD-3", "oss": true}'::jsonb)
ON CONFLICT (slug) DO UPDATE
SET stars = EXCLUDED.stars,
    tags = EXCLUDED.tags;

WITH ranked AS (
    SELECT
        slug,
        category,
        stars,
        ROW_NUMBER() OVER (PARTITION BY category ORDER BY stars DESC) AS rank_in_cat
    FROM curated_tools
    WHERE 'ha' = ANY (tags) OR metadata @> '{"oss": true}'::jsonb
)
SELECT slug, category, stars, rank_in_cat
FROM ranked
ORDER BY stars DESC;
```

## Step 4: Stop the Lab Container

```bash
docker stop awesome-pg-lab
```

## Next Steps

- Follow [How-To: Validate and Submit Curated Entries](../02-how-to-guides/validate-and-contribute-entries.md).
- Read [Reference: Category Catalog, Rules & SQL Matrix](../03-reference/categories-rules-and-sql-matrix.md).
