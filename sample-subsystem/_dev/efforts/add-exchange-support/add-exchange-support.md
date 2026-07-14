---
title: Add exchange support
type: dev-effort
status: active
created: 2026-05-20
deadline: 2026-07-01
---

# Add exchange support

## Goal

Add a second data source (`venue-beta`) behind the existing ingestion contract, so the
pipeline can pull from more than one source without any downstream stage knowing which source a
record came from. Everything here is a synthetic build task; the sources are invented and no real
or live system is involved.

## Acceptance

- `venue-beta` records normalize to the same internal record shape as `venue-alpha`.
- No downstream stage references a venue by name; the venue is a config value only.
- Reconciliation (record counts in vs normalized out) matches for a full replayed window.
- Adding the venue required config plus one connector module, and zero edits to downstream stages.

## Tasks

### ✅ VEN-001 – define the ingestion contract as an explicit interface

**Validation:**
- The existing `venue-alpha` connector is refactored to implement the interface with no behavior
  change (reconciliation identical before and after).

Closure note: extracting the interface first meant `venue-beta` had a target to build against
instead of copying `venue-alpha` and diverging.

### ▶️ VEN-002 – implement the `venue-beta` connector

**Goal:** connector pulls `venue-beta` records and emits them through the shared contract.

**Context:**
- Related: [[../../domains/data-pipeline/data-pipeline|data-pipeline domain]] holds the
  normalization invariants this connector must satisfy.
- Constraint: connector must be pure data-in, data-out; no writes to shared state.

**Validation:**
- `venue-beta` sample payloads normalize to the internal record shape.
- Timestamps are normalized to UTC at the connector boundary, per the data-pipeline invariant.
- Malformed payloads are quarantined, not dropped silently.

**Steps:**
- [x] map `venue-beta` fields to the internal record
- [x] normalize timestamps to UTC at ingestion
- [ ] wire the quarantine path for malformed payloads
- [ ] add fixtures and connector-level tests

### ⏸️ VEN-003 – end-to-end reconciliation across both venues

**Validation:**
- Counts in equal counts out across a replayed window for `venue-alpha` and `venue-beta` combined.

[Paused: blocked on VEN-002's quarantine path. Reconciliation cannot be trusted until malformed
records route to quarantine rather than vanishing. Resumes when VEN-002 reaches verified.]

## Notes

Extracting the contract (VEN-001) before writing the new connector was the right call. It turned
"add a venue" into "implement one interface" instead of a copy-and-edit job that would have drifted.

## Findings log

- 2026-05-27 11:15 UTC – `venue-beta` emits timestamps in a local offset, not UTC. Disposition:
  normalize at the connector boundary; reinforces the existing UTC-at-ingestion invariant rather
  than proposing a new one. Live-decided.

## Closure

[Filled at the closure ritual once every task reaches a terminal state and reconciliation is
verified end-to-end. Empty while active.]
