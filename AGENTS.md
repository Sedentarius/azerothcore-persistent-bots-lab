# Guide for software agents and AI reviewers

This repository is designed to be reviewed by both humans and software agents. This file defines the minimum reading order and evidence rules.

## Start here

Read these files before making project-level claims:

1. `PROJECT.yaml` - machine-readable project scope and current phase.
2. `INDEX.yaml` - stable IDs and repository paths.
3. `docs/methodology.md` - evidence and experiment rules.
4. `docs/glossary.md` - project terminology.
5. `docs/reproducibility.md` - provenance requirements.

Then read the specific experiment, dataset, incident, ADR, or release manifest relevant to the task.

## Evidence rules

Do not treat all repository text as equally strong evidence.

Use this order:

1. raw or published data with provenance;
2. reproducible analysis output;
3. completed experiment result;
4. QA result for a defined contract;
5. direct observation;
6. inference or interpretation;
7. design decision;
8. hypothesis or planned work.

An ADR records what the project chose to do. It does not prove that the choice is historically correct or experimentally superior.

An observation can identify a real event. It does not establish its cause unless the evidence supports that inference.

## Do not fill gaps silently

If an exact upstream commit, configuration value, runtime exposure, dataset, or result is missing, say that it is missing. Do not infer it from a nearby file, current upstream state, or general World of Warcraft knowledge.

Do not convert planned experiments into completed findings.

Do not describe PlayerBots as machine-learning agents unless the specific component being discussed actually uses machine learning.

## Provenance path

For a research result, try to resolve this chain:

`result -> experiment -> dataset -> session(s) -> release -> project commit + upstream commits + effective configuration`

Report broken links in this chain as reproducibility limitations.

## Stable IDs

Prefer project IDs when referring to artifacts:

- `ADR-*` decision
- `EXP-*` experiment
- `OBS-*` observation
- `SES-*` server session
- `DATA-*` dataset
- `INC-*` incident
- `C*` cohort

Do not replace these with database IDs in public documentation.

## Code and configuration review

When reviewing a patch or configuration change:

- identify the upstream revision it applies to;
- distinguish intended configuration from captured effective configuration;
- look for linked QA or experiments;
- check whether the change can create artificial levels, gold, items, consumables, repairs, or other state;
- check persistence and restart behavior when relevant;
- prefer a regression test over a prose claim.

## Writing style

Use simple American English. Prefer short sentences and concrete terms. Keep technical precision. See `docs/style-guide.md`.

## Safety and legal boundaries

Never request or publish credentials, private infrastructure secrets, live account databases, proprietary World of Warcraft client files, MPQ archives, or copyrighted game assets as part of normal repository work.
