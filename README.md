# AzerothCore Persistent Bots Lab

A public research and engineering project about persistent autonomous bot populations in an AzerothCore world.

The project studies how PlayerBots behave when they are treated as persistent characters rather than disposable population fillers. The world starts in a Vanilla-like stage, progresses through TBC and WotLK, and aims to preserve normal game causes for level, money, equipment, professions, travel, group activity, and economic behavior.

PlayerBots are mainly rule-based autonomous agents. This repository does **not** describe them as machine-learning agents unless a future component actually uses machine learning.

## Current status

**Phase:** pre-reset design and QA

**Initial world target:** level 1-60, x1 rates, persistent bot cohorts, historical progression controls, no artificial level redistribution, and no generated gold, food, equipment, or repairs unless a documented compatibility exception is required.

No experimental result should be treated as established until its protocol, runtime exposure, configuration, data, and limitations are published.

## Main research questions

1. Can a persistent PlayerBots population progress for long periods without artificial level redistribution or routine resource generation?
2. What economic behavior emerges when bots must obtain money, equipment, consumables, training, and profession materials through normal game systems?
3. How do bot cohorts introduced at different times change population structure and world activity?
4. Which failures are caused by agent logic, navigation, configuration, era compatibility, or server infrastructure?
5. How reliably can autonomous groups complete dungeons and later raid content with limited human intervention?
6. Which configuration and code changes are useful enough to contribute back to the AzerothCore and PlayerBots ecosystem?

See [`docs/research-questions.md`](docs/research-questions.md) for scope and measurement rules.

## Core principles

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
| `analysis/` | Reproducible analysis code |
| `results/` | Experiment reports and generated summaries |
| `qa/` | Regression and pre-release validation |
| `fixtures/` | Small canonical datasets for tests and AI review |
| `incidents/` | Failures, root causes, and regression links |
| `scripts/` | Realm, export, telemetry, backup, and manifest tooling |

`PROJECT.yaml` is the machine-readable project entry point. `INDEX.yaml` links stable IDs to repository paths.

## Runtime model

The realm does not need to run 24/7. Research exposure is recorded with three clocks:

- **calendar time:** real elapsed time;
- **server runtime:** time the world server was running;
- **bot-hours:** summed online exposure across bots.

Normal play sessions are valid observational data. Controlled experiments are declared separately and use predefined protocols.

## Reproducibility target

A result should eventually be traceable through this chain:

`commit -> release manifest -> session(s) -> experiment -> dataset -> analysis -> result -> decision or patch`

See [`docs/reproducibility.md`](docs/reproducibility.md).

## Software base

The current project uses:

- World of Warcraft 3.3.5a client, build 12340, as the protocol/client base;
- AzerothCore;
- PlayerBots / `mod-playerbots`;
- `mod-individual-progression`;
- `mod-era-talents`;
- Docker-based local deployment.

Exact revisions are not claimed in this README. They belong in release manifests under `manifests/releases/`.

## Legal and data boundaries

This repository will not distribute Blizzard client files, MPQ archives, copyrighted game assets, account credentials, secret keys, or private database dumps. Upstream projects retain their own licenses and attribution. Project-wide licensing is being documented before reusable code or derivative patches are published; see [`docs/licensing.md`](docs/licensing.md).

## Project maturity

This repository is intentionally starting small. Empty scientific ceremony is avoided. New schemas, standards, and automation are added only when they protect reproducibility, reduce ambiguity, or make results easier to review.
