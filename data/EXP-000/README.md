# EXP-000 published data

This directory contains sanitized, publication-safe extracts from the two EXP-000 baseline runs.

## DATA-0001 — RUN-0001 cohort extracts

Published files:

- `DATA-0001-level-events.tsv` — all 27 observed level-change events in the 10-bot cohort, classified as either a large artificial re-level event or a one-level progression-compatible event.
- `DATA-0001-cohort-summary.tsv` — per-bot start/end state and simple longitudinal activity counts.
- `DATA-0001-effective-playerbots.txt` — effective PlayerBots configuration keys directly referenced by the analysis.

The RUN-0001 source series contains 145 timestamped snapshots with 10 bots per snapshot (1,450 bot rows). One capture gap overlaps the unplanned power outage and restart.

## DATA-0002 — RUN-0002 and closure extracts

Published files:

- `DATA-0002-exposure-summary.tsv` — session/runtime thresholds and conservative bot-hour integration.
- `DATA-0002-level-events.tsv` — five observed cohort level-ups.
- `DATA-0002-cohort-summary.tsv` — start/end and activity counts for the ten-bot cohort.
- `DATA-0002-restart-summary.tsv` — both clean restart recovery checks.
- `DATA-0002-performance-summary.tsv` — Windows-host and Docker-container resource summaries.
- `DATA-0002-database-summary.tsv` — first/final allocated database sizes.
- `DATA-0002-final-composition.tsv` — final class and race composition from post-run read-only queries.

RUN-0002 raw evidence SHA-256:

`82753760cfdca330e15a50db33e322986a356a2bc8062df9d0a7f9dbe727ff83`

Post-run read-only addendum SHA-256:

`9606753428100dff6755c816262bd3c9b97135507e635da4c836053dbd98dd67`

The raw operational bundles and database backup are retained outside GitHub. They are not committed because this repository publishes compact reviewable extracts rather than operational logs or private database state.

## Cohort

The same ten-bot observational cohort was followed across both runs:

- Caminevane
- Tibevon
- Cekis
- Hjorgul
- Nythinne
- Kelgih
- Ramdiir
- Sugzapo
- Fisy
- Kany

Database GUIDs are retained in research extracts as row identifiers only.

## Classification rule

`artificial_relevel` is used for an observed level change larger than one level between adjacent snapshots when the event also matches the enabled LevelBrackets/full-randomization mechanism.

`organic_compatible_levelup` is deliberately weaker. It means a one-level increase whose XP transition and surrounding state are compatible with ordinary progression. It does not prove whether XP came from quests, kills, battlegrounds, or another normal source.

## Known RUN-0002 source-format defect

Three raw RUN-0002 TSV streams (`cohort.tsv`, `level-distribution.tsv`, and `database-size.tsv`) omitted one tab delimiter immediately after the fixed-width ISO-8601 timestamp. The original raw files remain immutable. DATA-0002 extracts were normalized from the recoverable records.

## Units and interpretation

- money: copper
- coordinates: persisted AzerothCore character coordinates
- database sizes: bytes unless otherwise stated
- Docker CPU: Docker percentage accounting, which can exceed 100% across logical CPUs
- snapshot time: America/Santiago (`-03:00` during these runs)
- post-shutdown `characters.online` database flags are not interpreted as live connections

## Provenance

- experiment: `EXP-000`
- runs: `RUN-0001`, `RUN-0002`
- final report: `analysis/EXP-000-final-report.md`
- deployment bundle: `7da03710f8cfbc9729760c9a9f54d19a217ad80c`
- AzerothCore: `413bea61a85e20d9caef7d66fc601a661fdddd9d`
- mod-playerbots: `b949b50bfcdd4fab937781bac2d7765e39330e4b`

No credentials, database dumps, `.env` files, client assets, or private infrastructure secrets are included.
