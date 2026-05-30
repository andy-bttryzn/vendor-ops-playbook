# 02 — The Two-Layer Inbox

## The problem

A vendor-ops inbox sees four categories of mail:

1. **Vendor-facing live threads** — the actual work
2. **System notifications** — invoices auto-generated, dispo reports, deletion digests, monitoring pings
3. **Cross-talk** — internal forwards, sister-company chatter, accounting CCs
4. **Noise** — newsletters, marketing, calendar spam

A single-layer inbox treats all four the same. You scroll, you triage, you lose 20 minutes you weren't going to get back. By Wednesday you have 400 unread.

The two-layer model says: **automate categories 2, 3, and 4 out of the inbox entirely; the inbox is reserved for category 1**.

## Layer 1: Gmail filters

Build filters that catch the patterns and dump them into per-category labels. Examples:

- `from:noreply@* OR list:* → skip Inbox, apply 03.noInbox`
- `subject:"Daily Disposition Report" → skip Inbox, apply 03.noInbox/dispo`
- `from:billing@yourplatform.com → skip Inbox, apply 03.noInbox/billing`
- `from:*@yoursistercompany.com -to:vendor-ops@yourco → skip Inbox, apply 03.noInbox/sister`

The convention: anything under `03.noInbox/*` is *out of your inbox* but *still reachable* if you need it. You're not deleting; you're moving the noise out of the way.

Filters are conservative by design. They only catch patterns you've *seen* trigger noise. New senders default to Inbox until you've decided whether to filter them.

## Layer 2: triage shortcuts

When you sit down to work the inbox, you're working only category 1 (live vendor threads). For each thread, you have a small finite set of moves:

- **Reply** — draft + send + label-swap to waiting-customer
- **Brief** — render the vendor's brief, decide from the brief
- **Bury** — close the thread (strip INBOX + status labels), it's done
- **Snooze** — re-surface on a specific day
- **Forward** — route to the right human, then bury
- **Ingest** — extract the substance into a task, then bury

A shortcut layer (keyboard binding, slash command, AI prompt, whatever your tooling allows) makes each move one keystroke. The point isn't speed for its own sake; the point is that decision and execution stop being separate steps.

## Why this matters

The cost of an undrained inbox isn't the time spent draining it. It's the cognitive overhead of *not knowing what's in there*. Every unread thread is a potential surprise; the only way to know is to scroll.

A drained inbox is the working definition of *"I know what's happening across my vendors today."* That's also what makes the [vendor brief](03-the-vendor-brief.md) reliable — if the inbox is current, the brief reflects the actual state.

## Don't filter what you can't trust

A filter that incorrectly moves a live vendor thread out of your inbox is worse than no filter. Two safeguards:

1. **Edge-case confirmation.** When you add a new filter, run it manually against the existing inbox first. If it catches 1–3 threads, eyeball each one before activating. If it catches 10+, the rule is broad enough to trust.

2. **Paired rules.** Many automation rules have a happy-path version and a reply-arrived version. The happy-path version auto-archives one-shot system mail; the reply-arrived version catches *"someone replied to that auto-mail, restore it to Inbox."* Both have to exist or you'll lose the reply.
