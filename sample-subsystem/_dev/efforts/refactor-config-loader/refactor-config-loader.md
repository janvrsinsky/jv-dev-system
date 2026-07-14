---
title: Refactor config loader
type: dev-effort
status: active
created: 2026-05-03
deadline: 2026-06-20
---

# Refactor config loader

## Goal

Move the pipeline config loader onto an explicit, versioned schema so new venues and new
processing stages can be added declaratively, without editing loader code each time. Old
config files must keep parsing during the transition.

## Acceptance

Written before the work; closure verifies against these.

- Schema v2 parses every existing config fixture without error.
- Old (unversioned) config files still parse through a backward-compat path.
- Loader rejects unknown top-level keys with a clear message rather than silently ignoring them.
- Unit tests cover both schema versions and the reject path.

## Tasks

### ✅ CFG-001 – introduce a `schema_version` field and a v2 parser

**Validation:**
- All 9 config fixtures declaring `schema_version: 2` parse into the same in-memory shape
  the loader produced before.
- Missing `schema_version` routes to the v1 (legacy) path.

Closure note: shipped clean. The version field defaults to 1 when absent, which keeps every
pre-existing file valid without edits.

### ✅ CFG-002 – strict unknown-key rejection

**Validation:**
- A config with a misspelled key (`intervall` instead of `interval`) fails loudly, naming the
  offending key.
- No known-good fixture regresses.

### ▶️ CFG-003 – backward-compat path for legacy configs

**Goal:** legacy unversioned files continue to load unchanged through the v1 path while v2 is
the forward default.

**Validation:**
- Every legacy fixture parses to the identical normalized structure it did before the refactor.
- A round-trip test (load, re-emit as v2, load again) is stable.

### ❓ CFG-004 – migration helper to rewrite v1 files as v2 🚩

**Validation:**
- Helper converts a v1 file to an equivalent v2 file with no semantic change.

[Partial because: the helper handles the common shape but not configs that use the deprecated
inline-override block. Carry-forward: decide whether to support inline overrides or drop them
first, then finish the helper. Flagged for operator decision at closure.]

## Notes

The unknown-key rejection surfaced two fixtures that had been carrying dead keys for a while;
those keys never did anything. Cleaned up as part of CFG-002.

## Findings log

Append-only. Each row: datetime UTC, summary, disposition.

- 2026-05-11 09:42 UTC – two config fixtures carried dead top-level keys that the old loader
  silently ignored. Disposition: dropped the keys, noted in CFG-002. Live-decided.
- 2026-05-18 14:07 UTC – the inline-override block only appears in legacy configs and blocks the
  migration helper. Disposition: raised as an open question for operator (support vs deprecate);
  parked in the `data-pipeline` domain's parked-decisions section. Live-decided.

## Closure

[Filled at the closure ritual: what actually shipped, key decisions, deferred items, and any
lessons promoted into domain runbooks. Not filled while the effort is still active.]
