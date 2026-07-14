# CLAUDE.md - sample-subsystem

Subsystem-specific rules, auto-loaded at session start for this subsystem only. This is a
synthetic sample that demonstrates the dev-system method; there is no real system behind it.
These rules complement, and never repeat, the method described in `docs/pattern-overview.md`.

## Session warm-up (read before any work)

1. The subsystem card (`sample-subsystem.md`).
2. This file (subsystem rules).
3. `_dev/SUMMARY.md` (strategic state).
4. Every active domain note under `_dev/domains/` (invariants and recurring obligations).
5. Every in-flight effort under `_dev/efforts/`.
6. `_dev/+inbox/` (local capture, triaged later).
7. The most recent `_dev/LOG/` entries.

Closed efforts, retired domains, and archived LOG entries are pulled on demand, not at warm-up.

## Hard limits (never autonomous)

- No destructive operation without explicit human confirmation.
- No live-system mutation without explicit human confirmation.
- No change to monitoring or alerting without explicit human confirmation.

Act first only when harm is imminent and the correct action is unambiguous; otherwise confirm.

## Working rules

- Acceptance criteria are written when a task is created, never retrofitted at closure.
- One LOG entry per material change, cross-linked to its effort, domain, task, and commit.
- New work is checked against active domain invariants before it starts; a hard conflict pauses
  the work and surfaces the violated rule to a human.
- An effort closes only through the closure ritual, not by flipping a status flag.
- A task is marked verified only when its validation criteria were actually exercised.
