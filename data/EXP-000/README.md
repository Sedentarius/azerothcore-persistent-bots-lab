# EXP-000 published data

This directory contains compact publication-safe extracts for the two EXP-000 baseline runs.

## DATA-0001 — RUN-0001

- `DATA-0001-level-events.tsv`
- `DATA-0001-cohort-summary.tsv`
- `DATA-0001-effective-playerbots.txt`

These files support the initial 24-hour characterization.

## DATA-0002 — RUN-0002 and experiment closure

- `DATA-0002-exposure-summary.tsv` — session/runtime thresholds and conservative bot-hour integration.
- `DATA-0002-level-events.tsv` — five observed cohort level-ups.
- `DATA-0002-cohort-summary.tsv` — start/end and activity counts for the ten-bot cohort.
- `DATA-0002-restart-summary.tsv` — both clean restart recovery checks.
- `DATA-0002-performance-summary.tsv` — Windows-host and Docker-container resource summaries.
- `DATA-0002-database-summary.tsv` — first/final allocated database sizes.
- `DATA-0002-final-composition.tsv` — final class and race composition from post-run read-only queries.

## Raw evidence

The repository does not publish operational log bundles or database backups.

RUN-0002 raw evidence SHA-256:

`82753760cfdca330e15a50db33e322986a356a2bc8062df9d0a7f9dbe727ff83`

Post-run read-only addendum SHA-256:

`9606753428100dff6755c816262bd3c9b97135507e635da4c836053dbd98dd67`

## Known source-format defect

Three raw RUN-0002 TSV streams (`cohort.tsv`, `level-distribution.tsv`, and `database-size.tsv`) omitted one tab delimiter immediately after the fixed-width ISO-8601 timestamp. The original raw files remain immutable. Published DATA-0002 extracts were normalized from the recoverable records.

## Units and interpretation

- money: copper
- database sizes: bytes unless otherwise stated
- Docker CPU: Docker percentage accounting, which can exceed 100% across logical CPUs
- timestamps: America/Santiago (`-03:00` during the measured period)
- `organic_compatible_levelup`: compatible with ordinary progression but not proof of a specific XP source

Post-shutdown `characters.online` database flags are not interpreted as live connections.
