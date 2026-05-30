# 03 — The Vendor Brief

## What it is

A single rendered view that answers *"what's the state of this vendor right now, and what should I do next?"*

Ten sections, fixed order:

1. **Header** — name, side, status, rating, primary URL
2. **Summary** — verticals, modalities, sourcing, notes (a one-screen scan of who they are)
3. **Contacts** — active and inactive subsections; current humans you can actually reach
4. **Inbox matrix** — every live thread, with subject, last activity, owner, labels, one-line summary
5. **Helpful Links** — contracts, dashboards, portals, tracking URLs
6. **Tasks** — Blockers / Ongoing / Upcoming / Completed
7. **Reference** — free-form k/v: internal IDs, payment terms, return semantics, anything you'd otherwise have to look up
8. **Synthesis** — analyst prose tying it together
9. **Open Items** — every outstanding question, tagged with what we're waiting on, sourced to evidence
10. **Recommended Actions** — concrete imperatives, tagged with assignee, sourced to evidence

Sections 1–7 render mechanically from your data store + inbox. Sections 8–10 are interpretive — written by a human (or an AI assistant with citation support), grounded in the data above them.

See [vendor-brief-renderer](../../vendor-brief-renderer/) for a reference implementation.

## When to render

- **Before any vendor-facing reply.** The cost of a reply that contradicts current state (a contract just signed, an invoice just paid, an open question already answered) is higher than the cost of rendering a brief.
- **On any new inbound from the vendor.** Even short responses change state.
- **As prep for a check-in.** Before you write the weekly review or pop into a meeting.
- **On request.** Anyone in the org asking *"where are we with X?"* gets a rendered brief, not a verbal summary that decays the moment it's spoken.

You should be rendering briefs ten times a day. They're cheap to render (a script call) and the cost is dominated by reading them.

## What makes a good brief

**Show your work.** Every Open Item and Recommended Action ends with a `Sources:` line citing the thread, task, or document that supports it. If you can't cite it, you don't know it.

**Be honest about gaps.** If the contact list is stale, say so. If a label hasn't been swept in 14 days, flag it. A brief that pretends to be complete is worse than one that flags its own holes.

**Lead with what's actionable.** Open Items are sorted with technical / operational issues first, business items after. Recommended Actions are imperatives, not options. If the right action is *"do nothing, wait for X,"* that's still an action — write it that way.

**Stay scoped.** A single-thread brief (rendered to decide one specific item) should cut everything not relevant to that decision. Cluttering it with the rest of the vendor's history is noise.

## The brief is the deliverable

When an AI assistant renders a brief, the brief itself is the output. Not *"here's a brief, would you like me to also...?"* Just the brief. The human reads it and decides. Anything else dilutes the artifact.

## What it isn't

- Not a vendor profile / data sheet — those are static and don't help you decide today.
- Not a meeting agenda — agendas live in the meeting tool.
- Not a contract summary — contracts live in your document store; the brief links to them.

The brief is the *state of play right now*. Everything else is a different document.
