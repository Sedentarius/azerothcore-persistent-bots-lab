# EXP-000 - Fresh Upstream Baseline

## Purpose

Measure how the selected upstream server stack behaves before project-specific patches or behavioral configuration changes are applied.

## Final status

**Completed with limitations. Research closed after this baseline.**

EXP-000 contains two published runs:

- [`RUN-0001`](runs/RUN-0001.yaml) — initial 24-hour characterization.
- [`RUN-0002`](runs/RUN-0002.yaml) — additional exposure, continuous telemetry, two clean restarts, and closure measurements.

Final analysis: [`../../analysis/EXP-000-final-report.md`](../../analysis/EXP-000-final-report.md).

All declared exposure thresholds were met: more than 24 server-hours, more than 2,000 measured bot-hours, five sessions, two clean restarts, and a continuous session longer than four hours.

Several measurement groups remain incomplete and are preserved as explicit limitations. The experiment is not being extended to fill those gaps.

## Baseline identity

The experiment remained on one pinned upstream identity throughout both runs. Exact commits and the effective configuration are recorded in the run manifests and published data.

No project behavior patch or planned persistent-world tuning was introduced during EXP-000.

## Publication policy

The repository publishes compact normalized extracts. Raw operational evidence is retained separately and identified by SHA-256 in `RUN-0002.yaml` and the final report.

Unexpected behavior is reported as observation unless the evidence supports a stronger result.

## Project disposition

No follow-on intervention experiment is currently planned. The research program is paused after EXP-000 because project priorities changed and available resources are limited.

The baseline remains useful as a frozen descriptive reference. It should not be treated as a universal causal control.
