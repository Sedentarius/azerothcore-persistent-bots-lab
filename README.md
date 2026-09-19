# AzerothCore Persistent Bots Lab

A public research and engineering project about persistent autonomous bot populations in an AzerothCore world.

The project studies how PlayerBots behave when they are treated as persistent characters rather than disposable population fillers. The original design intended a Vanilla-like stage followed by TBC and WotLK while preserving normal game causes for level, money, equipment, professions, travel, group activity, and economic behavior.

PlayerBots are mainly rule-based autonomous agents. This repository does **not** describe them as machine-learning agents unless a future component actually uses machine learning.

## Current status

**Research paused after completion of the upstream baseline.**

The formal baseline experiment, [`EXP-000 - Fresh Upstream Baseline`](experiments/EXP-000-fresh-upstream-baseline/README.md), is closed as **completed with limitations**. Across two runs and five measured sessions it reached all declared exposure thresholds.

Final analysis: [`analysis/EXP-000-final-report.md`](analysis/EXP-000-final-report.md).

The project will not proceed to the previously planned intervention or persistent-world experiments at this time because priorities changed and available resources are limited. The repository remains as a reproducible record of the completed baseline and of the future design that was not executed.

## Research sequence

1. **Fresh upstream baseline — completed.** Default behavior was characterized before project patches or behavioral tuning.
2. **Intervention build — deferred / not currently planned.** The intended project changes were not applied as part of this research program.
3. **Persistent Vanilla world — deferred / not currently planned.**
4. **Later eras — deferred / not currently planned.**

The baseline is a descriptive reference point. It is not automatically a causal control for experiments that change several variables at once.

## Main baseline findings

- Default dynamic level management can rewrite individual RNDBOT level history.
- Synthetic money can accompany PlayerBots reinitialization.
- Autonomous movement and progression-compatible level-ups are observable.
- Two planned clean restarts recovered the configured 500-RNDBOT online population and preserved levels in the sampled ten-bot cohort.
- Invalid teleport attempts using a `Z=-200000` sentinel were observed.
- RUN-0002 supplied continuous external CPU/RAM, population, database-size, and cohort telemetry.

See the final report for evidence, denominators, and limitations.

## Main research questions

The repository was designed around these questions. Only the upstream-baseline portion was completed.

1. How does the selected upstream stack behave before this project changes it?
2. Can a persistent PlayerBots population progress for long periods without artificial level redistribution or routine resource generation?
3. What economic behavior emerges when bots must obtain money, equipment, consumables, training, and profession materials through normal game systems?
4. How do bot cohorts introduced at different times change population structure and world activity?
5. Which failures are caused by agent logic, navigation, configuration, era compatibility, or server infrastructure?
6. How reliably can autonomous groups complete dungeons and later raid content with limited human intervention?
7. Which configuration and code changes are useful enough to contribute back to the AzerothCore and PlayerBots ecosystem?

Only question 1 received a completed formal characterization. The remaining questions are preserved as historical project scope, not as completed results.

See [`docs/research-questions.md`](docs/research-questions.md) for the original scope and measurement rules.

## Core principles

- Measure upstream behavior before replacing it.
- Prefer observable game causes over synthetic fixes.
- Separate observations from controlled experiments.
- Publish negative and inconclusive results.
- Record exact upstream revisions, effective configuration, patches, and runtime exposure.
- Keep raw data immutable.
- Use stable IDs for experiments, sessions, cohorts, datasets, decisions, and incidents.
- Make the repository easy to inspect by both humans and software agents.
- Do not publish proprietary game files, credentials, private infrastructure details, or live database dumps.

## Repository map

| Path | Purpose |
| --- | --- |
| `docs/` | Methodology, architecture, terminology, and research scope |
| `decisions/` | Architectural Decision Records (ADRs) |
| `upstream/` | Exact upstream dependencies and revision records |
| `config/` | Sanitized source and effective configuration |
| `patches/` | Small, reviewable changes against upstream projects |
| `manifests/` | Release and server-session provenance |
| `experiments/` | Controlled experiments and their protocols |
| `observations/` | Findings from normal recreational use |
| `data/` | Published datasets and metadata |
| `schemas/` | Machine-readable data definitions |
| `analysis/` | Reproducible analysis and reports |
| `results/` | Experiment reports and generated summaries |
| `qa/` | Regression and pre-release validation |
| `fixtures/` | Small canonical datasets for tests and AI review |
| `incidents/` | Failures, root causes, and regression links |
| `scripts/` | Realm, export, telemetry, backup, and manifest tooling |

`PROJECT.yaml` is the machine-readable project entry point. `INDEX.yaml` links stable IDs to repository paths.

## Runtime model

The realm did not need to run 24/7. Research exposure was recorded with three clocks:

- **calendar time:** real elapsed time;
- **server runtime:** time the world server was running;
- **bot-hours:** summed online exposure across bots.

Normal play sessions were valid observational data when human presence and interventions were recorded.

## Reproducibility

The final baseline evidence chain is:

`upstream revisions -> sessions -> RUN-0001/RUN-0002 -> DATA-0001/DATA-0002 -> EXP-000 final report`

RUN-0002 raw operational evidence is retained outside GitHub and identified by SHA-256 in the run manifest and final report.

See [`docs/reproducibility.md`](docs/reproducibility.md).

## Software base

The completed baseline used:

- World of Warcraft 3.3.5a client, build 12340, as the protocol/client base;
- AzerothCore;
- PlayerBots / `mod-playerbots`;
- `mod-individual-progression`;
- `mod-era-talents`;
- Docker-based local deployment.

Exact revisions are recorded in the EXP-000 run manifests.

## Legal and data boundaries

This repository does not distribute Blizzard client files, MPQ archives, copyrighted game assets, account credentials, secret keys, or private database dumps. Upstream projects retain their own licenses and attribution. See [`docs/licensing.md`](docs/licensing.md).

## Project maturity

The project closes its active research phase after one completed baseline characterization. The repository is retained as an archival research record and may be resumed later, but no additional experiments are currently planned.
