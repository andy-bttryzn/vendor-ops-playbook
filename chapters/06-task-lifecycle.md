# 06 — Task Lifecycle

## When to spawn a task

Three triggers:

1. **You said you'd do X.** Any "I'll get back to you on..." or "Let me check and circle back" in outbound mail spawns a task. The cost of forgetting is catastrophic; the cost of an extra row in the Tasks board is zero.
2. **A vendor said they'd do X.** Same logic in reverse. The task tracks the chase, not the work itself.
3. **You decided not to do X right now.** Deferred work becomes a task with status Deferred. The decision survives even though no action happens this week.

Anything that's *not* one of these three is too small for a task. A task list that captures every micro-decision is a task list nobody reads.

## Status semantics

Pick a small set and hold the line:

- **Waiting on us / Waiting on internal**: the next move is ours
- **Waiting on Client / Waiting on Vendor / Waiting on Counterpart**: we've asked, they owe
- **Waiting on Legal / Accounting / Platform-X**: third-party hold; specific enough that you know who to chase
- **Deferred**: decided not to do now, no chase
- **Done**: completed
- **Abandoned**: no longer relevant; superseded; vendor died

The discipline: *Waiting on Client* requires that we've actually told the client about the task. If we're prepping the ask but haven't sent it, that's *Waiting on us*. The status reflects who owes the next move at this moment, not who's eventually responsible.

## Task naming

Names are imperatives. *"Send Q3 contract amendment"* not *"Q3 contract amendment situation."* If the task name doesn't answer *"what do I do?"* the task isn't done thinking.

For blocker tasks linked to a specific vendor, the convention: `{Blocker text} - {Vendor name}`. So scanning the Blockers group by name shows you immediately which vendor each blocker is for.

ASCII only. No em-dashes, en-dashes, colons. Use hyphens, commas, periods. Lots of dashboard tooling treats those characters as field separators.

## Dedup before create

Before spawning a task, check whether an equivalent task already exists for this vendor with a non-terminal status. Use fuzzy name matching (Levenshtein distance 3, substring containment, normalize trailing suffixes).

If a duplicate exists, *reuse* it:
- Flip status if it's been Abandoned and the issue resurfaced
- Prepend new context to the Notes
- Do not create a parallel task

Parallel tasks are the most common form of vendor-ops tech debt. They look harmless on creation and accumulate until your Tasks board has 600 open items, most of which duplicate each other.

## Promote, don't parallel-create

When a vendor blocker matches a standard onboarding-template task, **move** the template task to the Blockers group. Don't create a new Blocker task that duplicates it. The naming and dedup follow from the template; the move signals *"this isn't a future-checklist item anymore, it's a live problem."*

## Shared blockers consolidate

When 5+ vendors share the same blocker (e.g. *"awaiting platform feature X"*), collapse them into a single task with linked-vendor relations. One row, N linked vendors. When the blocker clears, you close one task and N vendors become unblocked.

The threshold isn't magic; pick what fits your scale. The principle is *one blocker = one tracking row*, not *one blocker × N vendors = N rows*.

## Notes are forward-looking

Lead the Notes with the *next action*. Historical context goes in a `[Previous:]` block at the bottom. A task whose Notes read like a diary is one you have to read in full every time you open it; a task whose Notes lead with the action is one you can act on in 5 seconds.

## Link emails to tasks

Every task spawned from an email carries the thread URL in the Notes. This is the most-violated rule in this chapter. The urge is *"I'll remember which email"*; you won't, and tomorrow you'll spend ten minutes finding it again.

## Don't assign

For an ops team of 1–2 people, assigning tasks is theater. You know whose lane each task is in from the context. Assignment fields go stale faster than status. Skip them.

For larger teams, this changes. But default off, not default on.

## Status transitions are events

Every status change is observable. *Waiting on us → Waiting on Client* means we just sent the ask. *Waiting on Client → Waiting on us* means they responded and the ball is back. These transitions are the heartbeat of the vendor relationship; the brief should surface them prominently.
