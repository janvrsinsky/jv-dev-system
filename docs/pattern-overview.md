# Pattern overview

A distilled, sanitized description of the dev-system method. This is the reference the sample
under `sample-subsystem/` illustrates. Every name here is generic; the private instance that
validated the method is not described.

The method exists because when you direct AI to build and operate real software, generating code
is the easy part. The discipline around it is the hard part: what gets validated before it is
called done, what can never be violated, what every change is logged against, and what the AI is
never allowed to do alone. The pattern is that discipline, expressed as plain markdown files and
git, with no framework to install.

## Two shapes for work: efforts and domains

Work takes one of two shapes, kept in separate folders with deliberately different names from the
outer knowledge base so the two layers never blur.

**Efforts** are bounded and goal-shaped. An effort carries a Goal, an Acceptance section written
before the work, a set of tasks each with upfront validation criteria, and a Closure note filled
only at the closure ritual. Efforts open, run, and then archive. A soft cap of four active efforts
keeps focus from scattering.

**Domains** are standing and invariant-shaped. A domain holds the rules a part of the system must
never violate, plus runbooks and any recurring obligations native to that area. Domains do not
close; they go active, then dormant, then retired, and retirement is its own deliberate ritual
with an audit entry.

The distinction is the point. An effort answers "what are we building and when is it done." A
domain answers "what must always hold, regardless of what we are building."

## The LOG: per-change audit trail

Every material change gets one LOG entry: a sequence-numbered file with a UTC timestamp to the
minute, frontmatter cross-references to the effort, domain, and task it touched, and a link to
the commit. The body stays to a few sentences because the diff carries the detail. The result is
a trail you can replay forensically months later: scan the LOG, find a change, jump to git for
the full diff. The LOG index renders straight from frontmatter, so there is no hand-maintained
table to drift.

## Acceptance is written before the work

Every non-trivial task carries its validation criteria at the moment it is created, not
retrofitted at the end. A task is marked verified only when those criteria are actually
exercised; otherwise it becomes partial, with the carry-forward stated in plain text. This closes
the most common failure of agentic work: marking something a success when the checks were never
run. Before a closure is put in front of a human, the AI reconciles each task's status against
its evidence and downgrades anything that does not hold, so the human catches what the self-check
missed rather than rubber-stamping it.

## Invariants are a gate, not a wish list

Before new work starts, it is evaluated against the active domain invariants. A soft overlap is
flagged and the work proceeds; a hard conflict blocks the work, which is parked in a paused state
with the violated rule cited inline and surfaced to a human. Invariants grow from real incidents,
not from a theoretical ceiling of rules, so the list stays short and load-bearing.

## A few actions are permanently off-limits to autonomy

Destructive operations, live-system mutations, and any change to monitoring or alerting always
require a human, even when the AI could act faster. Acting first is allowed only when harm is
imminent and the correct action is unambiguous; anything short of that is confirmed first, because
the cost of a wrong irreversible move dwarfs the cost of one extra turn. These three categories
are fixed at the pattern level; a subsystem may add concrete examples but may not remove them.

## Seven-state task palette

Terminal states are honest. A seven-glyph palette makes partial, failed, and killed first-class
outcomes, so the record reflects what actually happened rather than an optimistic flag flip.

| Glyph | State | Meaning |
|---|---|---|
| ▶️ | active | work in motion |
| ✅ | verified | objective met, all validation exercised |
| ⏸️ | paused | transient block, will resume |
| ❓ | partial | shipped but incomplete, carry-forward stated |
| ❌ | failed | objective not achieved, accepted as a known limit |
| 🪦 | killed | explicit decision to abandon, with rationale |
| 🔁 | recurring | standing obligation, never terminal |

Pick the terminal status from the end state, not from effort expended. Recurring is structurally
different from the other six: it never reaches a terminal state and lives inside its parent
domain rather than an effort.

## No finding disappears silently

An out-of-scope observation the AI makes mid-work is handled with three channels together: a flag
in the task heading, a row in the effort's findings log, and a live surface to the operator when
present. When the operator is absent, the AI applies narrow auto-decision rules (it may append to
an existing runbook or drop an ephemeral note, but it may not create a new runbook, propose a new
invariant, or spawn a new effort) and then re-surfaces every autonomous decision at the next
session start. Defense in depth: a live channel, a persistent flag, and a session-start digest,
so an insight never falls through a crack.

## Closure is a ritual

An effort closes only after every task reaches a terminal state, an optional integration-level
check runs when the effort touched shared state, the goal and acceptance criteria are reviewed
against evidence with a human in the loop, and the durable lessons are distilled into domain
runbooks. Closure is a sign-off, not a status change. Working notes are dropped unless durable;
memory-grade observations are promoted into the relevant domain so the next effort inherits them.

## Session warm-up

Before any work, an AI session reads a fixed sequence: the subsystem card, then the
subsystem-specific rules, then the strategic summary, then every active domain note (invariants
and recurring obligations), then every in-flight effort, then the local capture inbox, then the
most recent LOG entries. This loads the invariants that gate new work and the state that closure
will verify against, before the first request is acted on. Closed efforts, retired domains, and
archived LOG entries are not loaded by default; they are pulled on demand.

## What the method deliberately is not

Scope discipline is part of the design. It is not a multi-agent orchestration: one operator, one
AI, one thread, no personas or message bus. It is not a packaged framework or CLI: it is a working
method over markdown and git, framework-agnostic on purpose. It is not a machine-enforced schema:
the checking is cognitive and a human owns the boundary, with no linting gates pretending to be
judgment. And it is not branch-per-task machinery: a single branch, one source of truth per task,
no orchestration layer to maintain.
