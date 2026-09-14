# Methodology

This project uses simple scientific rules to keep engineering claims auditable. The rules matter more than academic presentation.

## Baseline-first design

Before applying project-specific patches or behavioral configuration changes, the project must characterize a fresh upstream deployment.

The first formal experiment is `EXP-000 - Fresh Upstream Baseline`.

For this project, **fresh upstream** means the selected upstream server stack at exact recorded revisions, installed as distributed, with no project patches and no project-specific behavioral tuning. Only changes required to make the software run in the local environment are allowed. Examples include credentials, paths, ports, database connection values, and other deployment-specific values that do not intentionally change bot or world behavior.

Every allowed baseline deviation from upstream defaults must be listed in the experiment manifest.

The baseline should measure behavior before trying to improve it. At minimum, it should describe:

- bot population creation and default level distribution;
- level changes across runtime, logout, and restart;
- default XP and world rates relevant to bots;
- default bot cheats, maintenance, equipment, food, money, repair, and training behavior when observable;
- character-state persistence;
- population online behavior;
- world-loop and host performance under the tested population;
- navigation or stuck events that occur during the observation window;
- basic group and Dungeon Finder behavior if enabled by the fresh stack;
- database growth and operational failures;
- exact server runtime, bot-hours, and human presence.

The baseline is a **reference baseline**, not automatically a valid control for every later experiment. If a later intervention changes several variables at once, causal claims require a narrower comparison, ablation, or dedicated control.

After the baseline is frozen, project changes should be introduced as explicit interventions. Whenever practical, measure the same metrics before and after the intervention.

## Evidence labels

Every important statement should fit one of these categories.

### Observation

Something directly recorded during normal play or server operation.

Example: `Seven bots triggered stuck recovery in Blackrock Depths during SES-000142.`

An observation may suggest a problem. It does not establish a cause.

### Hypothesis

A testable explanation or prediction written before evaluating the relevant experiment.

Example: `Most repeated BRD stalls are caused by navigation gaps rather than combat strategy.`

### Experimental result

A result produced by a declared protocol with known configuration, exposure, data, and analysis.

### Inference

An interpretation derived from evidence. Inferences must name the evidence and remain weaker than the data allows.

### Historical evidence

External evidence used to decide era-appropriate game behavior. Record the source, date or patch context, and uncertainty. Do not silently substitute modern behavior for historical behavior.

### Design decision

A choice made because it serves the project goal. A design decision is not automatically a historical fact or experimental finding. Stable decisions belong in an ADR.

### Bug

Observed behavior that violates a defined expectation. A bug report must state the expectation source: upstream behavior, project contract, era rule, protocol, or regression test.

## Observation versus experiment

Normal recreational play is recorded under `observations/`. It can generate useful hypotheses and discover defects.

Controlled tests belong under `experiments/`. An experiment should define its question, hypothesis, protocol, primary metrics, stopping rule or exposure target, and analysis plan before the result is interpreted.

Do not relabel a surprising observation as a planned experiment after seeing the outcome.

## Three clocks

The world may run intermittently. Record:

1. **Calendar time** - real elapsed time.
2. **Server runtime** - time the world server was actually running.
3. **Bot-hours** - summed online exposure across bots.

Use the clock that matches the mechanism. Auction expiration, mail, resets, and rested XP may depend on absolute time, while autonomous progression may be better compared by bot-hours.

## Provenance rule

A publishable result should be traceable to:

`experiment -> release -> exact upstream revisions -> effective configuration -> sessions -> dataset -> analysis -> result`

If one link is unknown, state that limitation instead of guessing.

## Minimum Publishable Experiment

A controlled experiment is publishable as a project result only when it has:

- stable experiment ID;
- research question;
- hypothesis or explicit exploratory status;
- protocol;
- exact server release and relevant configuration;
- population and cohort definition;
- runtime exposure;
- primary metrics defined before interpretation;
- dataset or sufficient raw evidence;
- schema and units;
- reproducible analysis method;
- result;
- limitations;
- provenance links.

## Repetition and uncertainty

Persistent agents are not perfectly deterministic. Prefer repeated runs or repeated independent windows when practical. Report distributions and uncertainty rather than only averages.

For small samples, publish the individual observations. For larger samples, prefer medians, quantiles, rates with denominators, and confidence intervals when they answer a real question.

Do not create statistical tests merely to make a result look scientific.

## Negative and inconclusive results

Publish them when they prevent repeated work or clarify system limits.

Use result states such as:

- `supported`;
- `partially_supported`;
- `not_supported`;
- `inconclusive`;
- `invalidated`.

QA uses `PASS`, `FAIL`, or `SKIP`; research conclusions do not.

## Change control

If an experiment changes after data collection starts, record the change. If the change can affect the primary result, create a new run or experiment revision instead of hiding the modification.
