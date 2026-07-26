# slow-query-digest

> Ten thousand slow queries, one bad query shape.

**Status:** 🚧 In development

## Overview

Group slow queries by normalized shape rather than literal text, so one pattern executed ten thousand times reads as one problem.

## Features

- Normalizes literals, IN-lists and bind parameters into a stable query fingerprint
- Reads PostgreSQL CSV logs, plain `log_min_duration_statement` output and `pg_stat_statements` snapshots
- Ranks shapes by total time, not just worst single execution, so the cheap-but-constant query surfaces
- Per-shape percentiles (p50/p95/max), call count and a representative example with its literals intact
- Diffs two digests to show which shapes regressed between releases
- Text, JSON and single-file HTML reports for pasting into an incident review

## Stack

Python + `psycopg` for `pg_stat_statements` collection, `sqlglot` for query normalization, `click` for the CLI, `rich` for terminal tables.

## Usage

```bash
slow-query-digest analyze /var/log/postgresql/postgresql.csv --top 20 --sort total-time --format html
```

## License

MIT
