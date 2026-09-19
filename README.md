# AzerothCore Persistent Bots Lab

A public research and engineering project about persistent autonomous bot populations in an AzerothCore world.

PlayerBots are mainly rule-based autonomous agents. This repository does **not** describe them as machine-learning agents unless a component actually uses machine learning.

## Current status

**Research paused after completion of the upstream baseline.**

[`EXP-000 - Fresh Upstream Baseline`](experiments/EXP-000-fresh-upstream-baseline/README.md) is closed as **completed with limitations**. It reached all declared exposure thresholds across five sessions and two runs. The final report is [`analysis/EXP-000-final-report.md`](analysis/EXP-000-final-report.md).

The project will not proceed to the previously planned intervention or persistent-world experiments at this time because priorities changed and available resources are limited.

The repository remains as a reproducible record of the baseline work and its negative, positive, and inconclusive results.

## Main baseline findings

- Default dynamic level management can rewrite individual RNDBOT level history.
- Synthetic money can accompany PlayerBots reinitialization.
- Autonomous movement and progression-compatible level-ups are observable.
- Two planned clean restarts recovered the configured 500-RNDBOT online population and preserved levels in the sampled ten-bot cohort.
- Invalid teleport attempts using a `Z=-200000` sentinel were observed.
- RUN-0002 provided continuous external CPU/RAM, population, database-size, and cohort telemetry.

These are descriptive results for the pinned baseline configuration, not universal causal conclusions.

## Research principles used

- Measure upstream behavior before replacing it.
- Separate observations from controlled experiments.
- Publish negative and inconclusive results.
- Record exact upstream revisions, effective configuration, interventions, and runtime exposure.
- Keep raw data immutable.
- Do not publish proprietary game files, credentials, private infrastructure details, or live database dumps.

## Repository map

| Path | Purpose |
| --- | --- |
| `experiments/EXP-000-fresh-upstream-baseline/` | Final experiment protocol and run manifests |
| `sessions/` | Measured session manifests |
| `data/EXP-000/` | Compact normalized datasets |
| `analysis/` | Baseline reports |
| `decisions/` | Architectural Decision Records |
| `upstream/` | Selected upstream baseline identity |
| `docs/` | Methodology, terminology, scope, and reproducibility rules |

`PROJECT.yaml` is the machine-readable project entry point. `INDEX.yaml` links stable IDs to repository paths.

## Reproducibility

The final evidence chain is:

`upstream revisions -> sessions -> RUN-0001/RUN-0002 -> DATA-0001/DATA-0002 -> EXP-000 final report`

Raw RUN-0002 operational evidence is retained outside GitHub and is identified in the run manifest by SHA-256.

## Legal and data boundaries

This repository does not distribute Blizzard client files, MPQ archives, copyrighted game assets, account credentials, secret keys, or private database dumps. Upstream projects retain their own licenses and attribution.
