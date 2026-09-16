# DATA-0001 — EXP-000 RUN-0001 cohort extracts

This directory contains sanitized, publication-safe extracts from the 24-hour `EXP-000 / RUN-0001` characterization window.

## Published files

- `DATA-0001-level-events.tsv` — all 27 observed level-change events in the 10-bot cohort, classified as either a large artificial re-level event or a one-level progression-compatible event.
- `DATA-0001-cohort-summary.tsv` — per-bot start/end state and simple longitudinal activity counts across the captured cohort series.
- `DATA-0001-effective-playerbots.txt` — effective PlayerBots configuration keys directly referenced by the analysis.

## Source series

The source observational series contains 145 timestamped TSV snapshots with 10 bots per snapshot (1,450 bot rows). Snapshots were taken approximately every 10 minutes. One 1 h 50 m capture gap overlaps the unplanned power outage and restart.

The raw snapshot bundle and full sanitized worldserver log are retained in the local publication archive used to produce this dataset. They are not committed here because this repository publishes compact reviewable extracts rather than operational log bundles.

## Cohort

Database GUIDs are preserved in these research extracts only as row identifiers. Public project documentation should refer to cohort members by name or project cohort identity rather than treating database GUIDs as stable project IDs.

Cohort members:

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

All 10 bots were `online = 1` in 100% of captured snapshots.

## Classification rule

`artificial_relevel` is used for an observed level change larger than one level between adjacent snapshots. In RUN-0001 every such event also ended with current XP equal to zero and matched the enabled LevelBrackets/full-randomization mechanism in the pinned PlayerBots code.

`organic_compatible_levelup` is deliberately weaker. It means a one-level increase whose XP transition and money behavior are compatible with ordinary progression. It does not prove whether the XP came from quests, kills, battlegrounds, or another normal XP-producing action.

## Units

- money: copper
- coordinates: persisted AzerothCore character coordinates
- snapshot time: America/Santiago (`-03:00` during this run)
- `location_change_intervals`: adjacent captured intervals where map/zone/XYZ changed
- `xp_increase_intervals`: adjacent intervals with unchanged level and increased XP
- `max_unchanged_continuous_minutes`: longest observed unchanged persisted state, excluding the power-outage capture gap

## Provenance

- experiment: `EXP-000`
- run: `RUN-0001`
- report: `analysis/EXP-000-RUN-0001-report.md`
- deployment bundle: `7da03710f8cfbc9729760c9a9f54d19a217ad80c`
- AzerothCore: `413bea61a85e20d9caef7d66fc601a661fdddd9d`
- mod-playerbots: `b949b50bfcdd4fab937781bac2d7765e39330e4b`

No credentials, database dumps, `.env` files, client assets, or private infrastructure secrets are included.
