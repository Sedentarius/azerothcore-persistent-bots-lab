# Writing style guide

All public project documentation is written in English.

## Language

Use American English for consistency with most technical documentation in the project ecosystem.

Examples:

- `behavior`, not `behaviour`;
- `analyze`, not `analyse`;
- `organization`, not `organisation`.

## Main rule

Write for a developer who is technically competent but does not know this project.

Use simple words when they are precise enough. Keep domain terms when replacing them would reduce accuracy.

Prefer:

> Seven bots changed level after restart without recorded XP gain.

Avoid:

> The analysis appears to suggest the possible existence of anomalous post-restart level modifications affecting a subset of the simulated population.

## Sentence and paragraph style

- Prefer short sentences.
- Keep one main idea per paragraph.
- Use active voice when it makes the actor clearer.
- Define uncommon acronyms on first use.
- Avoid promotional language.
- Avoid academic filler.
- Avoid claiming certainty that the evidence does not support.

## Evidence labels

Use explicit labels when useful:

- **Observation**
- **Hypothesis**
- **Result**
- **Inference**
- **Decision**
- **Limitation**

Do not use these labels interchangeably.

## Numbers and units

Always include units when a value could be ambiguous.

Prefer field names such as:

- `runtime_seconds`
- `latency_ms`
- `memory_bytes`
- `money_copper`
- `bot_hours`

Report denominators for rates.

## Dates and time

Use ISO 8601 in machine-readable files. Include an explicit UTC offset or `Z`.

In prose, prefer unambiguous dates such as `2026-09-14` when exact timing matters.

## Configuration and code

Use exact configuration keys, commands, paths, IDs, and commit SHAs when they matter to reproduction. Put them in code formatting.

Do not paraphrase a configuration value if the exact value is the evidence.

## Claims

Prefer narrow claims that the published evidence directly supports.

If a result was observed only in Vanilla stage, do not generalize it to TBC or WotLK without additional evidence.

If a result was observed only on one hardware configuration, say so when hardware could affect the result.
