---
title: LOG – audit index
type: dev-container
status: active
created: 2026-05-01
---

# LOG/

Per-change audit trail: one entry per material change to code, config, or system state worth
finding later. Each entry is a numbered, timestamped file whose frontmatter cross-links the
effort, domain, and task it touched, plus a link to the commit. The entry body stays to a few
sentences because the diff carries the detail.

The table below is a live Bases index generated from entry frontmatter, not a hand-maintained
list. Entries appear automatically when added. Columns are intentionally minimal (sequence
number plus title) because timestamp, effort, and domain are redundant with the title for a
visual sweep and only add noise to the table; they remain queryable in frontmatter.

```base
filters:
  and:
    - file.folder == "sample-subsystem/_dev/LOG"
    - file.ext == "md"
    - file.name != "LOG"
formulas:
  title_link: link(file, title)
properties:
  entry:
    displayName: "#"
  formula.title_link:
    displayName: Title
views:
  - type: table
    name: All entries
    order: [entry, formula.title_link]
    sort:
      - { property: entry, direction: DESC }
  - type: table
    name: Recent 10
    order: [entry, formula.title_link]
    sort:
      - { property: entry, direction: DESC }
    limit: 10
```

Outside Obsidian, grep is the fallback index: `grep -rn '<pattern>' _dev/LOG/`.
