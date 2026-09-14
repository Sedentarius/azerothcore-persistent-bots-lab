# System architecture

## Purpose

The repository describes and measures a local persistent AzerothCore realm built around PlayerBots. It is not a distribution of the World of Warcraft client or a replacement for upstream projects.

## Runtime layers

### Client layer

The protocol/client base is World of Warcraft 3.3.5a build 12340. Proprietary client files are not stored here. Required local patches are represented only by names, hashes, and reproducible instructions when legally appropriate.

### Core layer

AzerothCore provides world simulation, persistence, networking, game systems, maps, instances, pathfinding integration, and database access.

### Agent layer

PlayerBots provides rule-based autonomous player characters and group behavior.

### Progression layer

`mod-individual-progression` and `mod-era-talents` are used to approximate staged Vanilla -> TBC -> WotLK progression while keeping the 3.3.5a core/client base.

### Research layer

Project-owned scripts and telemetry record sessions, cohort exposure, economy events, navigation failures, QA, and experiment provenance.

## Persistent-world contract

The initial design aims for:

- level-1 bot creation;
- normal XP-based leveling;
- no dynamic reassignment of existing bot levels;
- x1 progression rates;
- persistent character state;
- era-aware race, class, spell, talent, and content gates;
- normal economic causes for money and items;
- reproducible restarts;
- Dungeon Finder retained as a deliberate quality-of-life feature.

Exceptions must be explicit and documented.

## Repository architecture

The repository separates five concerns:

1. **Source changes** - patches and scripts.
2. **Configuration** - sanitized source settings and captured effective settings.
3. **Execution provenance** - release and session manifests.
4. **Evidence** - observations and datasets.
5. **Interpretation** - analysis, results, ADRs, and incidents.

This separation reduces the chance that a design assumption is later mistaken for an observed result.

## External dependencies

Exact upstream repository URLs and commit SHAs belong under `upstream/` and release manifests. Documentation should not use floating branch names such as `master` or `main` as scientific provenance.

## Database policy

Live database dumps are backups, not public research artifacts. Public data should be sanitized exports with stable pseudonymous IDs and documented schemas.
