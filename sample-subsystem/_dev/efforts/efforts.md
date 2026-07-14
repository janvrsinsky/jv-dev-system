---
title: Efforts – container index
type: dev-container
status: active
created: 2026-05-01
---

# efforts/

Bounded, goal-shaped work that opens, runs, and closes. Each effort carries a Goal, an
Acceptance section written before the work, a set of tasks with upfront validation criteria,
and a Closure note filled only at the closure ritual. Closed efforts move to
`_dev/_archive/YYYY-MM-DD-<slug>/`.

Contrast with `domains/`, which never close and hold invariants rather than deliverables.

## Index (manually maintained – low churn)

- [[refactor-config-loader/refactor-config-loader|refactor-config-loader]] – active
- [[add-exchange-support/add-exchange-support|add-exchange-support]] – active

> Soft cap: at most 4 active efforts at once. Drafting and blocked do not count against the cap.
> This index is maintained by hand because effort count rarely exceeds a handful; high-churn
> containers (LOG, inbox) use a self-updating Bases query instead.
