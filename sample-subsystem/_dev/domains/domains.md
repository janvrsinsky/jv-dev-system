---
title: Domains – container index
type: dev-container
status: active
created: 2026-05-01
---

# domains/

Standing concerns with no end state. A domain holds the invariants a part of the system must
never violate, plus runbooks and any recurring obligations native to that area. Domains do not
close; they go active, then dormant, then retired, and retirement is a deliberate ritual.

Contrast with `efforts/`, which are bounded and archive when done.

## Index (manually maintained – stable cardinality)

- [[data-pipeline/data-pipeline|data-pipeline]] – active. Ingestion, normalization, reconciliation.

> This index is maintained by hand because a subsystem carries only a handful of long-lived
> domains. High-churn containers use a self-updating Bases query instead of a hand-maintained list.
