# Upstream dependencies

This directory records external repositories used by a realm release.

Do not vendor full upstream repositories here unless there is a documented reason. A release manifest should normally record:

- project name;
- repository URL;
- exact commit SHA;
- upstream license identifier and notice location;
- local patch series applied after checkout.

Floating branch names are useful for development but are not sufficient provenance for a published result.

Initial dependency families include AzerothCore, PlayerBots, Individual Progression, and Era Talents. Exact revisions will be added from the running server before the pre-reset release is declared.
