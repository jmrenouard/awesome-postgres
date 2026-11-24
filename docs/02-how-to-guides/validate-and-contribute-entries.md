# Validate and Contribute Awesome Postgres Entries

## Prerequisites

- Read [`CONTRIBUTING.md`](../../CONTRIBUTING.md) before you edit [`README.md`](../../README.md).
- Install Python `3.10` or newer on your host.
- Confirm the target tool has a public license or `(Commercial Software)` label.

## Procedure

### Step 1: Verify Format and Category Rules

1. Add one item per pull request in alphabetical or section order inside [`README.md`](../../README.md).
2. Format every entry strictly as `* [Name](URL) - description.` on a single line.
3. Keep descriptions neutral without superlatives or promotional claims.

CAUTION: Do not submit unmaintained scripts, private tools, or blog posts. Maintainers reject non-compliant pull requests.

4. If the entry is a commercial product, append `(Commercial Software)` at the end of the description.

### Step 2: Check TOC Anchors, Links, and Diagrams

1. If you add a new `### Category` header in `README.md`, add its anchor link inside `## Contents`.
2. Run the repository verification tests to validate TOC anchors, English text, and Markdown blocks.

```bash
python3 -m unittest discover -s tests -p "test_*.py" -v
```

3. Run `audit_helpers.py` if available to confirm valid Mermaid syntax and zero ASCII diagrams.

NOTE: `.travis.yml` runs legacy `awesome_bot` external link checks on CI hosts.

## Validation

Confirm `unittest` passes with zero failures across all checks. Then inspect `git diff` to verify only the intended bullet entry and TOC lines changed:

```bash
git diff README.md
```

## Rollback

If validation checks report broken anchors or split lines, discard the local edits and inspect `README.md`:

```bash
git checkout -- README.md
```

## Related Documentation

- [Category Catalog, Entry Rules & SQL Matrix](../03-reference/categories-rules-and-sql-matrix.md)
- [Taxonomy, Curation Policy & Quality Gates](../04-explanation/taxonomy-and-curation-model.md)
