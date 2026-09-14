# EXP-000 Preflight

Do not start measured gameplay until every **MUST** item below is complete.

## 1. Preserve the current QA world

**MUST**

- Perform a clean shutdown of the current QA world.
- Run the deployment bundle's normal database backup procedure.
- Verify that the backup files exist and are non-empty.
- Preserve the current project `.env` and effective configuration privately.
- Preserve any project patches or local files that are not already in Git.
- Record enough information to restore the QA world if needed.

The QA backup is not part of the public dataset. It may contain account and character data.

## 2. Prepare an isolated fresh baseline deployment

**MUST**

- Use a separate working directory or otherwise guarantee that the baseline starts from a new database state.
- Do not reuse the QA character database or PlayerBots database.
- Do not import QA characters or bot progression.
- Use the selected upstream bundle commit recorded in `../../upstream/baselines/EXP-000-selected-stack.yaml`.
- Verify the locally cloned component SHAs against the pinned SHAs before measurement.

If database isolation cannot be demonstrated, EXP-000 has not started.

## 3. Create baseline configuration

**MUST**

Start from the `.env.example` distributed at the selected bundle commit.

Change only values required for deployment and access. Typical examples are:

- a new strong database password;
- local network address required by WSL/Docker deployment;
- local filesystem paths;
- timezone if needed to represent the host correctly;
- account credentials.

Do not copy the project's tuned QA `.env` into the baseline.

Record every changed value in `baseline-deviations.yaml`. Secrets must be recorded as `redacted`, not committed.

## 4. Verify upstream identity

**MUST**

Before first measured startup, record:

- deployment bundle commit;
- AzerothCore fork commit;
- `mod-playerbots` commit;
- `mod-individual-progression` commit;
- `mod-era-talents` commit;
- other enabled module revisions that can affect measured behavior;
- Docker and Docker Compose versions;
- client build and locale.

The selected bundle currently targets WoW 3.3.5a build 12340.

## 5. Verify effective configuration

**MUST**

Capture the configuration actually consumed by the running server after setup, not only the source `.env`.

Check that project-specific final-world changes have not leaked into the baseline.

In particular, do not silently apply the project's planned x1 rates, level-60 bot cap, disabled dynamic level management, organic maintenance changes, AH patches, Dungeon Clear, or new telemetry.

## 6. Prepare the gameplay character

**MUST**

Create a normal non-GM account or otherwise ensure the measured gameplay character has no GM privileges.

Create a new level-1 character through the normal client flow.

Do not transfer items, gold, bags, skills, spells, or progress from the QA world.

The character is a baseline test character. It is not the final persistent-world main.

## 7. Prepare administrative access

**SHOULD**

Keep administrative access separate from the gameplay character.

Use admin commands only for server administration or diagnosis. Any command that changes measured world or character state must be recorded as an intervention.

## 8. Prepare client state

**MUST**

- Use WoW 3.3.5a build 12340.
- Use the client-side patches required by the selected upstream bundle.
- Record locale.
- Record the addon set used during the baseline.

UI addons are allowed. Gameplay automation that changes human behavior materially should not be introduced during the baseline.

## 9. Prepare read-only collection

**MUST**

Before measured play, confirm that the project can capture at least:

- session start and stop times;
- bot counts and level distribution;
- clean restart snapshots for a bot sample;
- database size at start and end;
- existing server logs;
- external CPU and memory measurements;
- human-online time;
- manual interventions and contamination status.

If a desired metric cannot be observed without patching the server, mark it `null` and document the limitation. Do not patch the baseline to obtain the measurement.

## 10. Create the first run record

**MUST**

Copy `runs/RUN-template.yaml` to the first real run file, for example:

`runs/RUN-0001.yaml`

Fill in the exact upstream identity and initial-state fields before the first measured session.

## 11. Start condition

EXP-000 data collection may begin only when:

- the old QA world is safely recoverable;
- the baseline database is demonstrably fresh;
- local SHAs match the selected upstream stack;
- baseline configuration deviations are documented;
- effective configuration has been captured;
- the gameplay character is new and non-GM;
- the first run record exists.

At that point, normal play can begin.
