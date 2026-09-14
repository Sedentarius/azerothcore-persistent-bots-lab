# Quality assurance

QA protects the realm contract and catches regressions. QA is not the same as a research experiment.

Initial pre-reset areas:

- build and clean startup;
- era/race/class gating;
- level-1 bot creation and level persistence;
- cohort addition without rewriting earlier bots;
- x1 rates;
- no unexplained generated gold, food, gear, or repair;
- trainer and profession persistence;
- Dungeon Finder smoke test;
- restart persistence;
- backup and restore checks;
- navigation/stuck telemetry;
- seasonal-event leakage checks;
- transport smoke tests.

Tests should report `PASS`, `FAIL`, or `SKIP` with a reason.
