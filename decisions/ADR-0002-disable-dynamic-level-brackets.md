# ADR-0002: Disable dynamic level brackets for persistent bots

- **Status:** Accepted
- **Scope:** PlayerBots population management

## Context

Dynamic level-bracket management is designed to keep a useful distribution of bots across level ranges. Reassigning the level of an existing bot breaks longitudinal character history.

## Decision

The final persistent realm will disable dynamic level brackets and other level-reset behavior that changes existing bot levels without earned XP.

## Validation requirement

Before the final reset, QA must create bots, record levels, progress a subset, restart the world, add a later cohort, and verify that earlier bots retain their earned levels.

## Consequences

Population balance will be an emergent result of progression and cohort introduction rather than a continuously enforced target.
