# EXP-000 — Final upstream baseline report

## Status

**Experiment status:** completed with limitations  
**Runs:** RUN-0001, RUN-0002  
**Measured sessions:** SES-0001 through SES-0005  
**Further experiments planned:** no

EXP-000 is closed as the project's final completed characterization. The declared exposure thresholds were met. Some required measurement groups remain incomplete; those gaps are preserved explicitly rather than filled by inference.

The project is not proceeding to an intervention experiment at this time because priorities changed and available resources are limited.

## Baseline identity

Both runs used the same pinned upstream stack:

- deployment bundle: `7da03710f8cfbc9729760c9a9f54d19a217ad80c`
- AzerothCore: `413bea61a85e20d9caef7d66fc601a661fdddd9d`
- mod-playerbots: `b949b50bfcdd4fab937781bac2d7765e39330e4b`
- mod-individual-progression: `977e2005bacf97f35e506eb27b8af6b2ea1136af`
- mod-multibot-bridge: `759c100d5e508b9af28531a2642ded70619828ba`
- mod-era-talents: `3a0d9776c6837d8a5e5038c23c01c4fc388d90f8`

The effective PlayerBots configuration relevant to interpretation is preserved in `DATA-0001-effective-playerbots.txt`.

## Exposure

RUN-0001 contributed **86,400.916 seconds** of measured worldserver runtime. RUN-0002 contributed **70,464.929 seconds**.

Total measured EXP-000 runtime was therefore **156,865.845 seconds**, or approximately **43 h 34 m 26 s**.

The experiment contained five measured sessions and two planned clean restarts. The longest continuous session was SES-0001 at **57,162.633 seconds**.

RUN-0002 continuously sampled the online population. A conservative integration of adjacent valid samples produced **9,720.264 bot-hours**. This value alone exceeds the declared 2,000 bot-hour threshold. RUN-0001 bot-hours are not added because whole-population exposure was not continuously sampled in that run.

| Requirement | Required | Observed |
| --- | ---: | ---: |
| Server runtime | 24 h | 43.57 h |
| Bot-hours | 2,000 | >= 9,720.264 |
| Server sessions | 4 | 5 |
| Clean restarts | 2 | 2 |
| Continuous session | 4 h | 15.88 h |

## Population structure

The frozen RNDBOT pool contained **100 accounts and 1,000 characters**.

Class construction was exactly balanced: 100 characters in each of the ten WotLK classes.

Race construction was not exactly balanced:

- Human: 92
- Orc: 71
- Dwarf: 83
- Night Elf: 116
- Undead: 94
- Tauren: 95
- Gnome: 84
- Troll: 88
- Blood Elf: 138
- Draenei: 139

This corresponds to 514 Alliance and 486 Horde characters.

During stable bots-only operation the configured online RNDBOT target was 500.

## Result 1 — dynamic population policy rewrites individual level history

RUN-0001 observed 27 level-change events in the ten-bot cohort:

- 14 large artificial re-level events;
- 13 one-level progression-compatible events.

The large changes matched the enabled dynamic LevelBrackets/randomization mechanism and ended with XP reset to zero. Large money discontinuities were also consistent with synthetic money initialization during randomization.

The baseline therefore does not preserve a continuous earned level or money history for every RNDBOT.

RUN-0002 did not contradict this result. Its same ten-bot cohort produced five level changes and all five were +1 progression-compatible events; no large cohort re-level occurred during RUN-0002. The global level distribution nevertheless shifted materially across RUN-0002, so the absence of a large event in the ten-bot sample must not be generalized to the whole population.

## Result 2 — autonomous progression is observable

Across both runs, the cohort produced repeated XP increases, movement, and one-level transitions compatible with ordinary autonomous gameplay.

RUN-0002 level-ups were:

- Cekis 62 -> 63
- Fisy 78 -> 79
- Kelgih 71 -> 72
- Ramdiir 57 -> 58
- Sugzapo 78 -> 79

All were +1 changes with high pre-level XP and low post-level residual XP. They are classified as `organic_compatible_levelup`, not as proof of a specific XP source.

The baseline evidence supports the narrower conclusion that PlayerBots can autonomously move and gain progression-compatible XP while default population-management systems may later overwrite individual histories.

## Result 3 — clean restart recovery was successful in the sampled baseline

RUN-0002 included two planned clean restarts.

Clean restart 1:

- new world initialization: `2026-09-16T17:03:44.494-03:00`
- first sampled return to 500 RNDBOTs: `17:05:46`
- observed recovery time: **121.506 s**

Clean restart 2:

- new world initialization: `2026-09-16T21:48:51.176-03:00`
- first sampled return to 500 RNDBOTs: `21:50:36`
- observed recovery time: **104.824 s**

All ten cohort bots were online after both restarts and none changed level across either restart comparison.

This is a favorable sampled persistence result. It does not prove that every PlayerBot state field survives every restart.

## Result 4 — navigation errors remain observable

RUN-0001 recorded 14 invalid teleport attempts affecting nine bots. RUN-0002's retained SES-0005 log contains another invalid teleport using the same characteristic `Z = -200000` sentinel, affecting Alltaa.

The evidence establishes that this invalid-teleport failure mode exists in the selected baseline. A whole-run rate is not reported for RUN-0002 because complete worldserver logs were not retained for every session.

No permanent stuck loop was demonstrated in the ten-bot cohort.

## Human gameplay window

Normal non-GM play occurred in SES-0004.

The `BASELINE` account recorded:

- last login: `2026-09-16 17:17:36`
- character `Rand` logout: `2026-09-16 18:27:22`

Measured human-online time was therefore **4,186 seconds** (1 h 09 m 46 s).

During the human-play window, two existing RNDBOT characters were manually brought into the party because the starting area had no available party support. The online count temporarily reached 502 RNDBOTs plus one human.

This intervention is documented and excluded from autonomous-population interpretation. The persistent pool remained 100 accounts / 1,000 RNDBOT characters, and the online population later returned to 500.

## Performance

RUN-0002 collected external performance samples at approximately one-minute intervals.

| Component | Metric | Median | P95 | Maximum |
| --- | --- | ---: | ---: | ---: |
| Windows host | CPU | 23.0% | 51.0% | 98.0% |
| Windows host | memory used | 23.096 GiB | 27.423 GiB | 31.633 GiB |
| worldserver | CPU | 210.960% | 228.739% | 255.960% |
| worldserver | memory used | 5961.728 MiB | 6096.742 MiB | 6107.136 MiB |
| database | CPU | 4.240% | 11.164% | 98.720% |
| database | memory used | 1848.320 MiB | 1869.824 MiB | 1875.968 MiB |

Docker CPU percentages are container CPU accounting and may exceed 100% when more than one logical CPU is used.

RUN-0001's world-loop values remain event-triggered summaries rather than unbiased continuous latency telemetry.

## Database allocation

RUN-0002 captured 115 database-size snapshots. Allocated size did not change between the first and last snapshot:

| Database | Start bytes | End bytes | Allocated growth |
| --- | ---: | ---: | ---: |
| acore_auth | 589,824 | 589,824 | 0 |
| acore_characters | 61,102,632 | 61,102,632 | 0 |
| acore_playerbots | 78,268,025 | 78,268,025 | 0 |
| acore_world | 475,301,888 | 475,301,888 | 0 |

This means no additional InnoDB allocation was observed by this metric. It does not mean the databases had no row updates.

## Reliability

RUN-0001 included an initial deployment-recovery incident: the fresh installer omitted two PlayerBots weightscale tables and worldserver failed repeatedly until the pinned upstream base SQL was imported.

After measurement began, RUN-0001 later experienced one unplanned local power outage.

RUN-0002 completed two planned clean restart cycles and the final clean shutdown without a measured crash.

A post-run DB-only query found one RNDBOT (`Uku`) with a stale `characters.online = 1` flag after worldserver had already been shut down. Post-shutdown DB flags are not interpreted as live connections.

## Evidence and provenance

RUN-0002 raw evidence archive SHA-256:

`82753760cfdca330e15a50db33e322986a356a2bc8062df9d0a7f9dbe727ff83`

Post-run read-only addendum SHA-256:

`9606753428100dff6755c816262bd3c9b97135507e635da4c836053dbd98dd67`

The repository publishes compact normalized extracts rather than full operational logs or database dumps.

## Limitations

EXP-000 closes with explicit measurement gaps:

1. RUN-0001 human-online seconds were not measured.
2. Item/consumable generation, automatic repair, and automatic training provenance were not directly observable; these remain `null`, not zero.
3. Complete RUN-0002 worldserver logs were not retained for every session, so navigation-error rates cannot be generalized across the whole run.
4. Raw RUN-0002 cohort, level-distribution, and database-size TSV files contain a missing-tab formatting defect after the timestamp. The records are recoverable because the timestamp width is fixed; published DATA-0002 extracts are normalized.
5. Exact XP source, quest-versus-grind contribution, and general behavior under the project's proposed x1 persistent-world configuration were not tested.

## Final disposition

EXP-000 met all declared exposure thresholds and is frozen as a descriptive upstream reference **with limitations**.

The project will not proceed to the previously planned intervention and persistent-world experiments at this time. Research activity is paused after this baseline because of changed priorities and limited available resources.

No causal claim is made beyond the evidence collected under the pinned upstream configuration.
