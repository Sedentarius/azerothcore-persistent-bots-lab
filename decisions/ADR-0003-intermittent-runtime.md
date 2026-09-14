# ADR-0003: Support intermittent server runtime

- **Status:** Accepted
- **Scope:** Research timing and normal operation

## Context

The realm is also a recreational world. Requiring 24/7 operation would add hardware and operational constraints that are not necessary for most research questions.

## Decision

The research design must remain valid when the server runs only during selected hours.

Every relevant session records calendar timestamps, server runtime, and bot-hours. Experiments that require continuous operation, such as soak tests, must state that requirement explicitly.

## Consequences

- Cohort age cannot be described by calendar days alone.
- Systems based on absolute time, such as auctions or mail, must be analyzed separately from systems driven mainly by active runtime.
- A future 24/7 server can add continuous studies without changing the basic methodology.
