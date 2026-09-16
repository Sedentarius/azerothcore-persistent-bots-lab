# EXP-000 / RUN-0001 — 24-hour upstream characterization

## Status

**Run status:** completed  
**Experiment status:** incomplete; not ready to freeze.

RUN-0001 reached the 24-hour server-runtime target. It did not satisfy all EXP-000 completion thresholds. The experiment manifest requires at least four server sessions and two clean restarts. RUN-0001 contained two measured sessions and no clean restart. The only restart inside the measured window followed an unplanned power outage.

Several required measurement groups were also not collected continuously in this run, including host/container CPU and memory, database growth, exact human-online time, and direct whole-population bot-hours.

This report therefore publishes the 24-hour characterization as evidence without treating EXP-000 as finished.

## Baseline identity

Selected upstream bundle:

- deployment bundle: `7da03710f8cfbc9729760c9a9f54d19a217ad80c`
- AzerothCore: `413bea61a85e20d9caef7d66fc601a661fdddd9d`
- mod-playerbots: `b949b50bfcdd4fab937781bac2d7765e39330e4b`
- mod-individual-progression: `977e2005bacf97f35e506eb27b8af6b2ea1136af`
- mod-multibot-bridge: `759c100d5e508b9af28531a2642ded70619828ba`
- mod-era-talents: `3a0d9776c6837d8a5e5038c23c01c4fc388d90f8`

Runtime environment captured at publication:

- Docker 29.7.2
- Docker Compose v5.5.1
- local timezone: America/Santiago

The effective PlayerBots configuration included:

- `AiPlayerbot.MinRandomBots = 500`
- `AiPlayerbot.MaxRandomBots = 500`
- `AiPlayerbot.DisableRandomLevels = 0`
- `AiPlayerbot.RandomBotFixedLevel = 0`
- `AiPlayerbot.LevelBrackets.Enabled = 1`
- `AiPlayerbot.LevelBrackets.Dynamic.UseDynamicDistribution = 1`
- `AiPlayerbot.LevelBrackets.Dynamic.RealPlayerWeight = 10`
- `AiPlayerbot.LevelBrackets.Dynamic.SyncFactions = 1`
- `AiPlayerbot.ResetBotLevel.Enabled = 0`
- `AiPlayerbot.BotActiveAlone = 10`
- `AiPlayerbot.EnablePeriodicOnlineOffline = 0`

## Exposure

Measured worldserver runtime was **24 h 00 m 00.916 s**.

Session 1:

- operational start: 2026-09-14 23:40:13.554 CLST
- last logged event before power loss: 2026-09-15 15:32:56.187 CLST
- measured runtime: 15 h 52 m 42.633 s

Interruption:

- log gap: 2 h 00 m 36.398 s
- cause: unplanned local power outage

Session 2:

- operational start: 2026-09-15 17:34:14.428 CLST
- graceful stop signal: 2026-09-16 01:41:32.711 CLST
- measured runtime: 8 h 07 m 18.283 s

The endpoint query recorded **500 characters online and 500 RNDBOT characters online** immediately before shutdown.

A 10-bot observational cohort was sampled every 10 minutes. The published series contains 145 snapshots and 1,450 bot rows. All 10 cohort bots were online in 100% of captured snapshots.

## Deployment incident

The fresh installation entered a worldserver restart loop because two required PlayerBots base tables were absent:

- `playerbots_weightscales`
- `playerbots_weightscale_data`

The final worldserver log contains 22 failed attempts reporting each missing table and 22 `Could not prepare statements of the Playerbots database` failures.

The missing upstream PlayerBots base SQL was imported manually. This is treated as a deployment-recovery incident, not as a behavioral intervention. Measurement began only after a stable successful world initialization.

See project issue #4 for the incident record.

## Result 1 — RNDBOT level state is not individually persistent under the selected baseline policy

### Observation

The 10-bot cohort produced 27 observed level-change events.

- 13 were one-level increases compatible with ordinary progression.
- 14 changed a bot by more than one level in a single 10-minute observation interval.

Examples include:

- Hjorgul: 14 -> 74 -> 3, later 4 -> 28 -> 76
- Kelgih: 19 -> 4, later 4 -> 34 -> 70
- Ramdiir: 55 -> 2, later 6 -> 57
- Sugzapo: 69 -> 1, later 2 -> 49 -> 38 -> 78
- Caminevane: 17 -> 70

All 14 large changes ended with current XP equal to zero.

### Evidence

The effective configuration enables dynamic level brackets and leaves random levels enabled.

The pinned PlayerBots implementation can assign a new bracket level and call `PlayerbotFactory::Randomize(false)`. The factory directly changes level state and resets current XP when the assigned level changes.

### Result

The selected baseline periodically rewrites RNDBOT level state to satisfy population-distribution policy. Large observed level changes are therefore not evidence of earned gameplay progression.

This result supports treating per-character level history as non-persistent under this baseline configuration.

## Result 2 — synthetic money is part of RNDBOT reinitialization

### Observation

Large level-rewrite events were frequently accompanied by large discontinuous money changes. By contrast, one-level progression-compatible events usually showed small or zero money changes.

Examples:

- Ramdiir 6 -> 57: about 69 g -> 2,656 g
- Sugzapo 38 -> 78: about 1,864 g -> 3,010 g
- Caminevane 17 -> 70: about 810 g -> 1,729 g

### Evidence

The pinned PlayerBot factory initializes money from a random range proportional to level during full randomization.

### Result

RNDBOT money balances in the selected baseline cannot be interpreted as purely earned economic history. At least some balances are synthetic state generated by bot reinitialization.

## Result 3 — ordinary autonomous progression is also observable

### Observation

The same cohort contains level changes compatible with ordinary gameplay progression. These events show a one-level increase, high pre-level XP, low residual post-level XP, and no large synthetic money reset.

Examples include:

- Kelgih 70 -> 71
- Fisy 77 -> 78
- Caminevane 70 -> 71
- Nythinne 79 -> 80
- Kany 56 -> 57
- Hjorgul 76 -> 77
- Tibevon 75 -> 76

Low-level sequences were also observed between artificial resets, including Ramdiir 2 -> 3 -> 4 -> 5 -> 6.

Across the 145-snapshot series, every cohort bot had repeated XP-increase intervals and repeated location changes.

### Inference

The upstream AI is capable of producing autonomous movement and progression-like behavior. The primary continuity problem observed in RUN-0001 is not an inability to gain XP. It is the coexistence of ordinary progression with population-management routines that can later overwrite character state.

This inference does not establish quest completion, kill provenance, or exact XP source for every increase because those actions were not directly instrumented.

## Result 4 — no permanent stuck loop was observed in the cohort

All 10 cohort bots changed position repeatedly during the run.

Location-change intervals per bot ranged from 92 to 124 across the captured series. Periods with no persisted state change occurred, including pauses of up to roughly 100 minutes for some bots, but every sampled bot later resumed changing state.

Because `AiPlayerbot.BotActiveAlone = 10` and SmartScale can reduce autonomous activity when no real player is nearby, a period without persisted movement is not by itself evidence of a navigation failure.

### Navigation errors outside the cohort

The worldserver log recorded 14 invalid teleport attempts affecting nine named bots. The most common repeated case was Valriaad with four events. The rejected coordinates commonly used an invalid `Z = -200000` sentinel.

The server rejected these teleports. RUN-0001 did not establish that any affected bot remained permanently stuck afterward.

## Result 5 — restart persistence was favorable in the sampled cohort

An unplanned power outage separated the two measured sessions.

After restart:

- the worldserver returned to stable operation;
- the online population returned to 500 RNDBOTs;
- all 10 cohort bots returned online;
- no immediate large re-level event was observed in the cohort;
- later progression-compatible events continued.

The outage therefore did not produce an observable cohort-wide state reconstruction.

This is a sampled persistence result, not proof that all PlayerBot state survives every restart.

## Reliability and world-loop observations

The final log contains:

- 25 worldserver start attempts total;
- 22 startup failures caused by the missing PlayerBots tables before recovery;
- 2 successful measured world initializations;
- one graceful measured shutdown.

During stable operation, 170 logged update-diff events exceeded the logging threshold.

Across their associated 500-tick summaries:

- median of reported mean tick time: 19 ms
- range of reported mean tick time: 11–29 ms
- median of reported median tick time: 6 ms
- range of reported median tick time: 4–10 ms
- median reported p95: 64.5 ms
- maximum reported p95: 107 ms
- median reported p99: 75 ms
- maximum reported p99: 139 ms
- maximum reported tick in these summaries: 327 ms

These are event-triggered log summaries, not an unbiased continuous latency sample.

## What RUN-0001 does not establish

RUN-0001 does not establish:

- exact whole-population bot-hours;
- human-online seconds;
- host or container CPU and RAM distributions;
- database growth;
- rates for stuck events per bot-hour;
- item, consumable, repair, or trainer provenance;
- exact quest-versus-grind contribution to XP;
- general behavior at x1 rates;
- behavior after disabling LevelBrackets;
- persistent-world behavior under project interventions.

## Decision impact

RUN-0001 provides direct evidence for the design concern already recorded in `ADR-0002`: dynamic level brackets are incompatible with an experiment that requires continuous individual character histories.

It also provides a positive reason to continue testing organic progression rather than replacing PlayerBots wholesale. Ordinary autonomous XP gain, movement, and one-level progression were observed when bots were not being rewritten.

The next intervention experiment should measure a clean level-1 population with artificial re-leveling disabled, x1 progression, and stronger activity/progression telemetry.

## Completion assessment

RUN-0001 completed its 24-hour window successfully.

EXP-000 is **not yet complete** under its declared protocol because:

1. measured server sessions: 2; required: 4;
2. clean restarts: 0; required: 2;
3. exact bot-hours were not directly measured;
4. required host/container performance telemetry was not continuously collected;
5. required database-growth measurements were not collected;
6. several resource-provenance measurements remain unobserved.

The correct next step is to preserve RUN-0001, complete the missing baseline exposure/provenance requirements in additional measured sessions, and only then freeze EXP-000.
