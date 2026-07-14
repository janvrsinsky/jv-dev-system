---
title: Data pipeline
type: dev-domain
status: active
created: 2026-05-01
updated: 2026-06-12
---

# Data pipeline

Ongoing concern covering how records enter the system, how they are normalized to a single
internal shape, and how ingestion is reconciled against output. This domain never closes; it
accumulates invariants and runbooks as the system meets real edge cases. All content here is
synthetic, written to demonstrate the pattern.

## Invariants

Operator-readable rules that must hold. One per line, active-verb opening for skimmability.
These are a gate, not a wish list: new work is checked against them before it starts, and a
hard conflict blocks the work until a human resolves it. Invariants grow from real incidents,
not from a theoretical ceiling of rules.

- Normalize every timestamp to UTC at the ingestion boundary, never downstream.
- Quarantine malformed payloads; never drop a record silently.
- Keep connectors pure data-in, data-out; a connector must not write shared state.
- Reference a venue only through config; no downstream stage may name a venue in code.
- Reconcile counts in against counts out for every replayed window before calling ingestion done.

## Runbooks

Flat notes promoted from effort closures and known-issue records live here alongside this note
(for example, a `reconciliation-procedure.md` or a `known-issues.md`). None are included in this
sample; the section is shown so the shape is clear.

## Parked decisions / re-open triggers

Decisions deliberately deferred, each with a trigger to revisit. Distinct from invariants
(rules that hold now) and from the inbox (untriaged captures).

- Whether to hard-fail on config schema drift instead of warning. Re-open trigger: when a schema
  mismatch causes a second real incident, or when the migration helper in `refactor-config-loader`
  ships. Context: raised from that effort's findings log 2026-05-18.
- Whether to keep supporting the legacy inline-override block in configs. Re-open trigger: decide
  before the config migration helper (CFG-004) can be finished.

## Recurring tasks

Cadence-bound obligations native to this domain would live here as Tasks-plugin list items
(for example, a weekly reconciliation review). None are defined in this sample.
