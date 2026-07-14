---
title: Sample subsystem – strategic summary
type: dev-summary
status: active
created: 2026-05-01
updated: 2026-06-12
---

# SUMMARY – sample-subsystem

> Strategic state, kept short (target: under 30 lines). This is the first thing read at
> session warm-up after the subsystem card and CLAUDE.md. It answers "where are we and
> what matters right now," not "what changed" (that is the LOG's job).

**What this subsystem is.** A synthetic data-processing service used here to demonstrate the
dev-system method. Everything below is invented; there is no real system behind it.

## Current focus

- Migrating the config loader onto a versioned schema so new venues can be added declaratively.
- Standing up a second data-source connector behind the same ingestion contract.

## Active efforts (2)

- `refactor-config-loader` – active. Schema v2 parses; backward-compat path under verification.
- `add-exchange-support` – active. Connector for `venue-beta` drafted; reconciliation check pending.

## Standing domains (1 shown)

- `data-pipeline` – ingestion, normalization, and reconciliation invariants. Never closes.

## Open risks

- Backward-compat for the old config schema is the highest-risk seam; both active efforts touch it.
- One deferred decision parked in `data-pipeline`: whether to hard-fail on schema drift (re-open
  trigger noted in the domain note).

## What is deliberately not here

No live numbers, no per-change detail, no task lists. Numbers live in the LOG; tasks live inside
their parent effort. This file stays a strategic sketch so it does not drift.
