# EXP-000 Runbook

## Objective

Start from a new upstream deployment, play normally, and measure what the selected stack does before this project changes bot behavior or world rules.

The baseline world is temporary. It will not become the final persistent realm.

## Selected upstream stack

The baseline should use the same upstream stack that the project plans to modify:

- `lathcf/azerothcore-playerbots-docker-automated` as the deployment bundle;
- its selected AzerothCore / PlayerBots base;
- `mod-playerbots`;
- any modules shipped and enabled by the selected upstream bundle configuration.

Exact repository revisions must be captured before the first measured session. Do not describe a component as part of the baseline unless its exact revision and enabled state are recorded.

## Clean-state rule

Do not reuse characters, bot progression, or databases from the current modified QA world.

Create a new baseline database state from the selected upstream deployment. The baseline world must start clean enough that previous project experiments cannot affect its results.

## Allowed changes

Only deployment changes required to run and access the server are allowed, for example:

- database credentials;
- local filesystem paths;
- bind addresses and ports;
- Docker/Compose deployment values;
- account creation;
- client realmlist;
- local backup paths.

Record every deviation from upstream defaults in `baseline-deviations.yaml`.

Do not change a setting because it looks undesirable. Measure it first.

## Forbidden changes during baseline

Do not apply project patches or planned final-world tuning, including:

- disabling dynamic level management;
- changing XP or economy rates for the final design;
- removing PlayerBots maintenance or resource generation;
- changing bot level caps for historical progression;
- adding project telemetry inside worldserver or PlayerBots;
- adding Auction House behavior patches;
- adding Dungeon Clear;
- changing navigation data to fix a discovered failure;
- changing combat AI to improve observed behavior.

If a change is required to keep the baseline runnable, stop the current run, document the reason, and start a new run revision.

## Human play

Normal recreational play is allowed and encouraged.

Use a normal non-GM gameplay character for measured play. Administrative access may exist on a separate account, but GM commands that affect world or character state must not be used during a valid measured session unless the intervention is explicitly recorded.

Start at the normal level and play through normal game systems. Quest, explore, group with bots, use vendors, die, resurrect, travel, and use Dungeon Finder when naturally available.

The goal is not to play in a sterile laboratory. The goal is to make human presence observable.

Record human-online time for each session.

## External observation only

The baseline should be observed without modifying server behavior.

Allowed read-only collection includes:

- existing worldserver logs;
- Docker container metadata;
- `docker stats` or equivalent host metrics;
- read-only SQL queries and database-size snapshots;
- Git revision capture;
- effective configuration capture;
- session start/stop timestamps;
- client build and addon inventory;
- manual notes linked to a session ID.

Do not add instrumentation code to the server during EXP-000.

## Exposure target

Freeze the baseline with all of the following:

- at least **24 server-hours**;
- at least **2,000 bot-hours**;
- at least **4 separate server sessions**;
- at least **2 clean worldserver restarts** during the measured period;
- at least **1 continuous session of 4 hours or more**.

If 24 server-hours are reached before 2,000 bot-hours, continue until both exposure requirements are met.

The server does not need to run 24/7.

## Sampling schedule

Capture a population/state snapshot:

- immediately after the clean baseline becomes ready;
- at the start of each measured session;
- at the end of each measured session;
- immediately before a planned restart;
- after the restarted world has stabilized;
- near cumulative runtime milestones of 1 h, 4 h, 8 h, 12 h, and 24 h when practical.

Host-performance samples may be collected more frequently, such as every 60 seconds, because they are external observations.

## Required manual gameplay checks

During normal play, attempt the following when naturally reachable:

- ordinary questing and combat;
- death and resurrection;
- vendor purchase and sale;
- trainer interaction;
- grouping with PlayerBots;
- zone travel;
- at least one clean logout/login cycle;
- Dungeon Finder if the character becomes eligible during the baseline.

Do not use GM leveling merely to unlock a test. If a feature is not naturally reached, report it as not observed in this baseline rather than fabricating exposure.

## Restart checks

For each planned restart:

1. select a documented bot sample before shutdown;
2. capture the observable state available through read-only queries;
3. perform a clean shutdown;
4. restart the worldserver;
5. capture the same state again;
6. record unexplained changes separately from expected time-based changes.

Do not interpret a difference until the relevant upstream mechanism is known.

## Session validity

A session is valid when:

- the upstream identity is unchanged;
- no project patch or behavior-changing configuration was introduced;
- required timestamps exist;
- human interventions are recorded;
- collected data can be linked to the session ID.

Mark a session `contaminated` rather than deleting it if an accidental GM command, configuration edit, crash-recovery change, or other intervention could affect results. Contaminated sessions may remain useful as observations but should not be included silently in baseline aggregates.

## Completion

EXP-000 is complete only after:

- all exposure targets are met;
- exact upstream revisions are archived;
- effective configuration is captured;
- baseline deviations are frozen;
- session manifests are complete;
- baseline datasets or evidence are preserved;
- a compact baseline report is generated;
- limitations are explicit;
- the baseline state is tagged in Git before project interventions start.

Recommended tag name:

`baseline-upstream-v0.1.0`

## Handoff to the project experiment

Do not convert the measured baseline world into the final persistent realm.

After EXP-000 is archived:

1. stop the baseline cleanly;
2. retain the research artifacts and any private backup required for verification;
3. create a new clean database state;
4. apply the project intervention patchset;
5. run pre-reset QA;
6. only then create the persistent Vanilla world and its first cohort.

This preserves a clear boundary between upstream behavior and project behavior.
