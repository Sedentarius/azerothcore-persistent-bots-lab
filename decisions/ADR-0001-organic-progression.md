# ADR-0001: Prefer organic persistent progression

- **Status:** Accepted
- **Scope:** Persistent bot population

## Context

Some PlayerBots population-management features can assign or reassign bot levels and resources to keep a convenient population distribution. That is useful for many servers but conflicts with a longitudinal world where individual bot history matters.

## Decision

Bots in the persistent research population should start from defined initial conditions and gain levels through normal XP. Existing bot levels must not be rewritten merely to maintain a desired population distribution.

The same principle applies to important resources: prefer normal game causes over automatic generation when practical.

## Consequences

- Population shape may become uneven.
- Low-level cohorts must be added deliberately if new-character activity is needed.
- Resource shortages are allowed to appear and may become useful findings.
- Convenience systems that generate state require explicit review.

## What this decision does not claim

This is a project design choice. It is not a claim about how original retail WoW operated or about the only correct way to configure PlayerBots.
