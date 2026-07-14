---
entry: 452
title: "🔌 venue-beta connector against shared ingestion contract, UTC normalized at boundary"
timestamp: 2026-05-27 11:31 UTC
agent: "Claude Opus 4.7"
effort: add-exchange-support
domain: data-pipeline
task: VEN-002
git: 3f9e0d2
---

# Log Entry 452: 🔌 venue-beta connector against shared ingestion contract, UTC normalized at boundary

2026-05-27 11:31 UTC

## Change

Implemented the `venue-beta` connector against the ingestion interface extracted in VEN-001.
Incoming `venue-beta` payloads carry a local offset, so timestamps are normalized to UTC at the
connector boundary, satisfying the data-pipeline UTC-at-ingestion invariant. Downstream stages
remain venue-agnostic; the venue is a config value only. Quarantine path for malformed payloads
is not wired yet, so end-to-end reconciliation (VEN-003) stays paused.

## Git

[3f9e0d2](../../..) – connector module, field mapping, and sample fixtures.
