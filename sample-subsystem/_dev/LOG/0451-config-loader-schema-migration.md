---
entry: 451
title: "🧱 Config loader onto versioned schema v2, legacy path preserved"
timestamp: 2026-05-11 09:58 UTC
agent: "Claude Opus 4.7"
effort: refactor-config-loader
domain: data-pipeline
task: CFG-001
git: 7a4b2c1
---

# Log Entry 451: 🧱 Config loader onto versioned schema v2, legacy path preserved

2026-05-11 09:58 UTC

## Change

Added a `schema_version` field to the pipeline config and a v2 parser behind it. Files without
the field default to version 1 and route through the legacy path, so every pre-existing config
keeps parsing untouched. All 9 fixtures parse into the same in-memory shape as before.

## Findings

While wiring the parser, two fixtures were found carrying dead top-level keys the old loader had
been silently ignoring. Logged in the effort's findings log; cleaned up under CFG-002.

## Git

[7a4b2c1](../../..) – full diff for the loader change and fixtures.
