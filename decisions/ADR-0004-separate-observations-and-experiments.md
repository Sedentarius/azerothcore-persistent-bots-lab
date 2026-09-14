# ADR-0004: Separate observations from controlled experiments

- **Status:** Accepted
- **Scope:** Evidence management

## Context

Normal play can reveal valuable behavior, but the player changes the world and does not follow a fixed experimental protocol.

## Decision

Findings from ordinary recreational play are recorded as `OBS-*` observations. Controlled tests are recorded as `EXP-*` experiments.

Observations may generate hypotheses and bug reports. They must not be presented as controlled causal evidence.

## Consequences

The project can remain enjoyable to play while preserving clear evidence boundaries.
