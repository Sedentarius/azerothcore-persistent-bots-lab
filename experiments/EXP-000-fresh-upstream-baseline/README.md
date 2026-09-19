# EXP-000 - Fresh Upstream Baseline

## Purpose

Measure how the selected upstream server stack behaves before this project applies its own patches or behavioral configuration changes.

This experiment establishes a reference point for later work. It is descriptive first. It should not be used as a universal causal control when later changes modify several variables at once.

## Research question

How does a fresh upstream deployment behave under a documented local test population and runtime window?

## Final status

**Completed with limitations. Research closed after this baseline.**

EXP-000 contains two published runs:

- [`RUN-0001`](runs/RUN-0001.yaml) — initial 24-hour characterization.
- [`RUN-0002`](runs/RUN-0002.yaml) — additional exposure, continuous telemetry, two clean restarts, and closure measurements.

Final analysis: [`../../analysis/EXP-000-final-report.md`](../../analysis/EXP-000-final-report.md).

All declared exposure thresholds were met: more than 24 server-hours, more than 2,000 measured bot-hours, five sessions, two clean restarts, and a continuous session longer than four hours.

Several measurement groups remain incomplete and are preserved as explicit limitations. The experiment is not being extended to fill those gaps.

## Start here

Use [`runbook.md`](runbook.md) for the historical operational procedure.

The baseline exposure target is defined in [`metrics.yaml`](metrics.yaml). All deviations from upstream defaults are recorded in [`baseline-deviations.yaml`](baseline-deviations.yaml).

## Primary outputs

The completed experiment publishes:

- exact upstream revisions and deployment environment;
- all recorded deviations from upstream default configuration;
- bot population and level-distribution evidence;
- cohort level changes and persistence across restart;
- money-state evidence where observable;
- bot online population and measured exposure;
- server runtime and conservative bot-hours;
- host/container performance summaries;
- database allocation snapshots;
- navigation/error observations;
- group behavior observed during normal play;
- reliability incidents and restart recovery.

Missing resource-provenance measurements remain explicit `null`/not-observed limitations rather than being converted to zero.

## Gameplay policy

Normal recreational play was allowed and used a normal non-GM character.

RUN-0002 records one scoped human intervention: two existing RNDBOT characters were manually brought into the party because the starting area lacked available party support. The affected population window is documented and is not used as evidence of autonomous population behavior.

## What this experiment does not do

It does not test the project's proposed organic-progression configuration. It does not establish x1 persistent-world behavior, exact XP provenance, or the long-term economy after project interventions.

The baseline world was temporary and is not being upgraded in place into a final persistent realm.

## Publication rule

No baseline statistic is published without its denominator, exposure window, and provenance.

Unexpected behavior is reported as an observation unless the protocol supports a stronger conclusion.

## Project disposition

No follow-on intervention experiment is currently planned. The research program is paused after EXP-000 because project priorities changed and available resources are limited.

The baseline remains a frozen descriptive reference.
