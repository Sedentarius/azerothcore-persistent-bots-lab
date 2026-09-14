# Contributing

Contributions should improve reproducibility, correctness, measurement, or practical PlayerBots behavior.

## Before opening a pull request

1. State the problem in concrete terms.
2. Link the affected experiment, observation, incident, or issue when one exists.
3. Keep code and configuration changes narrow enough to review.
4. Add or update QA when behavior changes.
5. Do not claim a causal result from an uncontrolled observation.
6. Do not commit credentials, private infrastructure data, proprietary game files, or live database dumps.

## Pull request evidence

A behavior-changing pull request should normally include:

- expected behavior;
- observed behavior before the change;
- exact test configuration;
- QA or experiment used to evaluate the change;
- observed behavior after the change;
- known limitations and rollback path.

Negative results are useful. A patch that does not work should be documented when the failure teaches something reusable.
