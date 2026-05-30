# 05 — Label Semantics

## The mental model

Labels are not folders. Labels are independent *dimensions* of a thread's state. A given thread can carry several at once because each label answers a different question.

The four core dimensions:

1. **INBOX**: is this thread visible in your inbox right now?
2. **00.received**: is there outstanding substance on this thread? (i.e. not fully closed out)
3. **01.priority**: is this thread important / active enough to surface above background?
4. **02.waiting/{who}**: who owes the next move?

Each is independent. A thread can be 00.received + 01.priority + 02.waiting/customer (you're chasing them on something important). Or 00.received only (you remember it exists but it's not active). Or no labels at all (fully closed).

## Why independent dimensions matter

The naïve approach is a single status field: *Open / Waiting / Closed*. That breaks the moment you have a thread that's *closed for now but resurrectable*, or *active but blocked on someone we can't chase*, or *low-priority but still owed*.

Independent dimensions let each axis carry its own truth. The combined state is the union.

## The two key verbs

**Archive** = remove INBOX. Keep 00.received and priority. The thread is no longer in the way of new mail, but it's still in the open-items pool. You can `label:00.received -is:inbox` to find everything not actively triaged but still live.

**Bury** = remove INBOX **and** 00.received **and** any 01.priority and 02.waiting labels. The thread is *done*. Comes back only if a new message arrives.

The mistake to avoid: archiving a thread you meant to bury, or burying one you meant to archive. The first leaves stale items in the pool; the second loses track of work that wasn't actually done.

## Status-transition labels

Layer one more dimension: when the thread state changes (you sent a reply, they replied to you, you're now waiting on accounting), swap the `02.waiting/*` label without touching `00.received`. The transition is observable in label history; the underlying open-item flag stays on until you bury.

Common waiting sub-labels: `waiting/me`, `waiting/customer`, `waiting/vendor`, `waiting/legal`, `waiting/accounting`, `waiting/internal`. Pick the set that maps to your routing.

## Vendor-scoped labels

In addition to the workflow labels above, every thread carries a vendor label: `zzzVendors/{Vendor}` (the `zzz` prefix is so the alphabetical list of labels doesn't get cluttered by them; not material to the logic).

This lets you scan a vendor's whole history with one label query without relying on domain matching (which fails when a vendor uses multiple domains or sends from personal addresses).

When a thread is identified as belonging to a vendor mid-conversation, apply the label *before* drafting any reply. Tooling downstream (briefs, audits, vendor reports) reads the label as truth.

## Hygiene rules

- **Outbound always gets 01.priority.** If you sent it, it's important enough to track.
- **Don't strip 00.received until full bury.** Status transitions (we're waiting on X now) only change the `02.waiting/*` label, not the underlying flag.
- **Post-send reconciliation.** After a send, the thread should land with `00.received + zzzVendors/{Vendor} + 02.waiting/{whoever}`. Never `03.noInbox` on live outbound.
- **Gmail label index is stale.** Label changes are visible to the API immediately, but Gmail's *search index* (the thing that backs `label:xyz` queries) lags by minutes. Don't rely on a search query running 30 seconds after a label change.

## The audit query

If you can describe the labels as independent dimensions, you can write audit queries. *Show me everything labeled 02.waiting/customer where the last inbound is more than 7 days old* is a single query. *Show me threads where I'm waiting on customer but never sent the chase nudge* is another. The labels enable the audits; without them you're back to scrolling.
