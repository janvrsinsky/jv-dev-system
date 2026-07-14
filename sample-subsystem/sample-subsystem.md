---
title: Sample subsystem
type: dev-card
status: active
created: 2026-05-01
updated: 2026-06-12
---

# Sample subsystem

> The vault-facing card. This is the only surface the outer knowledge base reads; everything
> operational lives under `_dev/` and stays private to the subsystem. All content here is
> synthetic, written to demonstrate the dev-system method. There is no real system behind it.

## What this is

A synthetic data-processing service used to illustrate the method: bounded efforts that open and
close, standing domains that hold invariants, a per-change audit LOG, and a closure ritual that
only signs off once acceptance criteria are actually exercised.

## State at a glance

- 2 active efforts: `refactor-config-loader`, `add-exchange-support`.
- 1 standing domain: `data-pipeline` (ingestion, normalization, reconciliation invariants).
- Full strategic state lives in `_dev/SUMMARY.md`; per-change history in `_dev/LOG/`.

## Where to look

- Strategic summary: `_dev/SUMMARY.md`
- Audit trail: `_dev/LOG/`
- Efforts: `_dev/efforts/`
- Domains and invariants: `_dev/domains/`
- Local capture: `_dev/+inbox/`

Nothing operational or private is exposed on this card by design; it is a pointer surface, not a
source of truth.
