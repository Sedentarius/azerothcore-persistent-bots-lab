# EXP-000 - Fresh Upstream Baseline

## Purpose

Measure how the selected upstream server stack behaves before this project applies its own patches or behavioral configuration changes.

This experiment establishes a reference point for later work. It is descriptive first. It should not be used as a universal causal control when later changes modify several variables at once.

## Research question

How does a fresh upstream deployment behave under a documented local test population and runtime window?

## Primary outputs

The experiment should publish a compact baseline report covering:

- exact upstream revisions and deployment environment;
- all deviations from upstream default configuration;
- bot population creation and level distribution;
- level changes and persistence across restart;
- default resource-generation or maintenance behavior that can be directly observed;
- money, inventory, equipment, food, repair, and training state where measurable;
- bot online population and exposure;
- server runtime and bot-hours;
- world-loop or host performance summaries;
- database growth;
- navigation/stuck events;
- basic group and Dungeon Finder behavior when available in the default stack;
- crashes, errors, and other operational incidents.

## What this experiment does not do

It does not test the project's proposed organic-progression configuration. It does not disable default PlayerBots systems merely because they conflict with the final design. Those changes belong to the intervention phase after this baseline is frozen.

## Publication rule

No baseline statistic should be published without its denominator, exposure window, and provenance.

Unexpected behavior should be reported as an observation unless the protocol supports a stronger conclusion.
