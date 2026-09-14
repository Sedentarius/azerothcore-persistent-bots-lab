# EXP-000 Protocol

## Goal

Capture the behavior of a fresh upstream deployment before project interventions.

## Pre-run freeze

Before collecting baseline data, record and freeze:

1. exact upstream repository revisions;
2. Docker image or local build identity;
3. effective server and module configuration;
4. every deviation from upstream defaults;
5. host hardware and operating environment summary;
6. client build and locale;
7. planned bot population;
8. runtime target or stopping rule;
9. metrics and sampling intervals.

If any behavior-changing configuration is changed after collection starts, close the current run and start a new run revision.

## Initial state

Use a new test world/database state suitable for the selected upstream stack. Do not carry characters or bot progression from the project's modified QA world into the baseline.

Project-specific patches are not allowed.

Do not disable or repair upstream behavior merely because it conflicts with the final project design. Record it first.

## Measurement blocks

### A. Population and progression

Record initial and final bot counts, online counts, level distribution, and unexplained level changes. When possible, snapshot the distribution at fixed server-runtime intervals.

### B. Persistence

Select a documented sample of bots. Record level, XP, money, equipment, inventory summary, skills, and other relevant state before and after a clean worldserver restart.

### C. Resource and maintenance behavior

Observe whether upstream systems create, replace, refill, repair, teach, or otherwise modify resources or character state without an identifiable in-world transaction. Record the mechanism only when evidence supports it.

### D. Economy state

Record money distribution and major money or item changes that can be measured reliably. Do not infer item provenance when it is not observable.

### E. Navigation and autonomy

Count and localize available stuck, recovery, travel, or path failures. If upstream telemetry is insufficient, state the limitation; do not add project telemetry during the baseline run.

### F. Group systems

Where the fresh stack exposes them, record basic party role behavior and Dungeon Finder behavior without project-specific tuning.

### G. Performance and reliability

Record server runtime, bot-hours, human-presence time, host CPU and memory summaries, available world-loop latency metrics, database size/growth, crashes, startup failures, and relevant error logs.

## Restart check

Perform at least one clean shutdown and restart during the baseline. The exact point in runtime must be recorded.

## Human intervention

Record any GM command, manual summon, forced teleport, manual bot control, or other intervention that could change measured behavior.

Routine login and recreational observation are allowed but human-online time must be recorded.

## Reporting

Prefer distributions and rates over isolated examples. Every rate must include its denominator.

Examples:

- stuck recoveries per 1,000 bot-hours;
- level changes per 100 bots per server-hour;
- crashes per server-hour;
- median and quantile level distribution at defined exposure points.

Publish individual events as supporting evidence when sample sizes are small.

## Completion condition

`EXP-000` is complete only when:

- the upstream identity and effective configuration are archived;
- the declared exposure target is reached;
- required datasets or evidence are preserved;
- a baseline report is generated;
- limitations are explicit;
- the baseline is tagged or otherwise frozen before project interventions begin.
