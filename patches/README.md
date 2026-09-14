# Patch policy

Project patches should be small, ordered, and tied to a specific upstream revision or compatible range.

Use names such as:

`0001-disable-generated-maintenance-resources.patch`

Avoid names such as `misc.patch`, `fixes.patch`, or `final.patch`.

Each behavior-changing patch should link to an issue, experiment, incident, or ADR and should have regression QA when practical.

Do not copy proprietary client code or game assets into patches.
