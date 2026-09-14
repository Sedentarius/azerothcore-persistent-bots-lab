# Research questions

The project is an engineering study of persistent rule-based game agents in a long-running virtual world. The goal is practical knowledge that can improve configuration, testing, debugging, and PlayerBots development.

## RQ0 - Fresh upstream behavior

How does a fresh upstream deployment behave before this project applies its own patches or behavioral configuration changes?

This is the reference question for the rest of the project. It establishes what the selected upstream stack already does, which behaviors are defaults, which problems already exist, and which later changes are actually caused by this project.

Useful measurements include bot creation, default level distribution, level changes, persistence, resource generation, equipment changes, population activity, world-loop performance, memory use, database growth, navigation failures, group behavior, Dungeon Finder behavior, and operational errors.

The baseline must record exact upstream revisions and every deployment-specific deviation from default configuration.

## RQ1 - Persistent progression

Can bots start at level 1 and progress over long periods without artificial level redistribution while preserving character state across logouts and server restarts?

Useful measurements include level distribution, XP provenance, unexplained level changes, deaths, play exposure, and persistence failures.

## RQ2 - Organic resource economy

Can bots remain viable when money, food, equipment, repairs, trainer costs, reagents, and profession materials must come from normal game systems?

The important question is not whether bots become rich. It is whether their resource state can be explained by valid in-world causes and whether resource shortages create useful failure signals.

## RQ3 - Cohort dynamics

What happens when new level-1 cohorts enter a world that already contains older bots?

The project will track cohort exposure using server runtime and bot-hours, not calendar age alone.

## RQ4 - Virtual market behavior

Can bots participate in an Auction House economy using legitimate inventory and gold, and what server-side liquidity is required when thousands of absent human players are not present?

Server-supplied goods and server purchasing must be measured separately because they create different economic effects.

## RQ5 - Navigation and autonomous travel

Where do bots fail to reach goals, and how often is the root cause navigation data rather than decision logic?

Repeated path failures should be localized by map, position, destination, and path state before adding AI-specific workarounds.

## RQ6 - Group autonomy

How reliably can autonomous parties complete dungeons and later raid encounters under era-appropriate class mechanics?

Metrics should include completion, wipes, deaths, manual interventions, stalls, and encounter-specific failure modes.

## RQ7 - Reliability and scale

How do bot population size and long-running sessions affect world-loop latency, memory, database behavior, and failure rates?

Long continuous soak tests are separate experiments. Normal recreational sessions do not need to run 24/7.

## RQ8 - Transferable engineering value

Which fixes, tests, telemetry, configuration rules, and documented failure modes are general enough to help other AzerothCore or PlayerBots users?

A result is more valuable when another developer can reproduce it without this project's private database or hardware.

## Out of scope unless explicitly added later

- claiming PlayerBots are machine-learning agents;
- measuring human social behavior from a single private player;
- reproducing every historical detail of original retail WoW;
- treating anecdotal play experience as causal evidence.
