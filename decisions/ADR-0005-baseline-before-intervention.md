# ADR-0005 - Measure fresh upstream behavior before project interventions

**Status:** Accepted

## Context

The project plans to change PlayerBots behavior, world progression rules, resource provenance, cohort creation, telemetry, and other server behavior.

If those changes are applied before the unmodified upstream stack is measured, later results cannot clearly show which behaviors already existed and which were introduced or removed by this project.

## Decision

The first formal experiment will characterize a fresh upstream deployment before project-specific patches or behavioral tuning are applied.

The baseline will use exact recorded upstream revisions. Project patches are not allowed. Configuration should remain at upstream defaults except for deployment-specific values required to start and access the server. Every such deviation must be recorded.

The baseline will be identified as `EXP-000 - Fresh Upstream Baseline`.

After `EXP-000` is frozen, project modifications will be introduced as explicit interventions. Shared metrics should be retained where practical so later builds can be compared with the baseline.

## Consequences

### Positive

- Default upstream behavior becomes observable instead of assumed.
- Later changes can be compared against a documented reference.
- Bugs already present upstream are easier to distinguish from project regressions.
- Other developers can compare their own fresh deployments with the published baseline.

### Cost

- The final persistent-world reset is delayed until the baseline is captured.
- Some measurements must be collected twice: before and after intervention.
- The baseline cannot serve as a causal control when later experiments change multiple variables at once.

## Important boundary

`Fresh upstream` does not mean an undocumented or generic AzerothCore installation. It means the exact upstream stack selected by this project at recorded revisions, without project patches or behavioral tuning.
