# Data model

The data model starts small. New fields are added when they support a defined question or debugging need.

## Stable identifiers

Use stable public IDs instead of database primary keys where possible.

- Session: `SES-000001`
- Cohort: `C01`
- Bot: `BOT-C01-0001`
- Experiment: `EXP-001`
- Observation: `OBS-000001`
- Dataset: `DATA-POP-001`
- Incident: `INC-0001`
- Decision: `ADR-0001`

Internal GUIDs may be kept in private operational data when required, but should not be the public identity layer.

## Core entities

### Session

A period of world-server execution. Key fields include start, stop, runtime, release, realm stage, termination reason, human presence, bot population, and bot-hours.

### Cohort

A defined population introduced under common initial conditions. Record creation session, creation method, population size, era/stage, starting level policy, and other experimental conditions.

### Bot state snapshot

Suggested minimum fields:

`timestamp, session_id, bot_id, cohort_id, level, xp, money_copper, map_id, zone_id, x, y, z, online`

### Economy event

Suggested fields:

`timestamp, session_id, bot_id, event_type, item_id, quantity, money_delta_copper, source, counterparty_type`

Possible event types include loot, quest reward, vendor buy, vendor sell, repair, trainer, auction post, auction sale, auction buy, mail settlement, craft, and trade.

### Navigation event

Suggested fields:

`timestamp, session_id, bot_id, map_id, instance_id, x, y, z, destination_x, destination_y, destination_z, path_result, stuck_count, recovery_action`

### Dungeon run

Suggested fields:

`run_id, session_id, dungeon_id, start_time, end_time, party_size, human_present, tank_type, healer_type, result, bosses_killed, deaths, wipes, manual_interventions`

## Units

Encode units in field names where ambiguity is likely: `_seconds`, `_ms`, `_bytes`, `_copper`.

## Null semantics

Use `null` only for unknown or not-applicable values as defined by the schema. Do not use `0`, empty strings, `-1`, and `null` interchangeably.

## Time

Use ISO 8601 timestamps with an explicit offset or UTC `Z`. Session analysis should preserve the difference between absolute time and server runtime.

## Storage formats

- Markdown: human documentation.
- YAML: small manifests and indexes.
- CSV: simple rectangular datasets.
- JSONL: event streams and irregular records.
- Parquet: large analytical datasets when size justifies it.
- JSON Schema: validation of machine-readable records.
