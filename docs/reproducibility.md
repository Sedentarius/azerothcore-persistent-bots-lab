# Reproducibility

## Goal

Another developer should be able to determine what was run, why it was run, what changed, what data was recorded, and how the result was produced.

Perfect bit-for-bit replay is not always possible in a persistent multiplayer simulation. The project therefore distinguishes **environment reproducibility**, **protocol reproducibility**, and **result replication**.

## Minimum Reproducible Realm

A realm release should record at least:

- Git commit of this repository;
- exact AzerothCore revision;
- exact revisions of PlayerBots and all relevant modules;
- applied project patches in order;
- Docker image tags and preferably immutable digests;
- sanitized source configuration;
- captured effective configuration used by the server;
- database schema/migration state and project-owned migrations;
- client build and locale;
- hashes of required local client patches without distributing them;
- cohort creation procedure;
- QA status;
- known limitations.

## Session manifest

Every research-relevant server start/stop window should have a session record. The session records server runtime, release, realm stage, population exposure, and whether a human player was present.

A server crash produces an incomplete session. Do not fabricate a clean stop time; mark the termination reason.

## Randomness

Record seeds when a component exposes a meaningful reproducible seed. Do not claim deterministic replay when upstream systems use hidden, time-based, database, or process-level randomness that is not controlled.

## Effective configuration

The effective configuration loaded by the process is stronger evidence than a template or `.env` value. Releases should archive sanitized effective configuration and hashes.

## Databases

Do not publish live realm dumps as the default reproduction method. Prefer:

- schema/migrations;
- small synthetic fixtures;
- sanitized cohort creation scripts;
- exported research datasets;
- checksums for private backup artifacts when a checksum is useful for internal verification.

## Raw data

Published raw datasets are immutable. Corrections create a new dataset ID and deprecate the old one with an explanation.

## Analysis

Official results should be reproducible from scripts where practical. Notebooks may be used for exploration, but a published result should not depend on undocumented interactive notebook state.
