# 01 — The Vendor-Ops Model

## The shift

The default operating mode in a vendor-heavy role is "respond to what's in front of me." Email comes in, you reply. Invoice lands, you forward it. Contract gets edited, you pass it on. Whoever is loudest gets your attention.

The shift is to stop treating the inbox as the system of record. The inbox is a *stream of events* about a vendor; the vendor itself is the object whose state matters.

## One vendor = one item

Every active relationship gets exactly one record in a structured store (whether that's monday.com, Notion, Airtable, a spreadsheet, or your own database). That record carries:

- **Identity:** name, side of the relationship (you're buying / you're selling / both), the URL of their portal or website
- **Status:** Prospecting / In Negotiation / Signed Pre-Launch / Onboarding / Live / Paused / Dead
- **Configuration:** verticals they cover, modalities they operate in, sourcing channel that brought them in
- **Counterpart contacts:** who's the GM, who's AP, who's tech ops, who's been replaced
- **Linked artifacts:** open tasks, recent threads, signed contracts, helpful links

Nothing about the vendor's state lives only in your head. Everything is queryable.

## The brief is the daily artifact

Once the vendor object exists, the daily question becomes: *what's the current state of vendor X?* The answer is the **brief**: a single rendered view that pulls together the configuration, the current open items, the recent thread activity, the tasks in flight, and a recommended next action. See [chapter 3](03-the-vendor-brief.md).

Briefs are cheap to render and expensive to read. You should be rendering them constantly and reading them only when you're about to act on the vendor.

## Stages, not just statuses

A status field on its own gives you *Live / Paused / Dead*. That's necessary but not sufficient. Layer in stage semantics:

- **Prospecting:** they don't know we exist yet (or barely)
- **In Negotiation:** active back-and-forth, no contract
- **Signed Pre-Launch:** paper done, technical/onboarding work in flight
- **Onboarding:** technical work in flight, vendor engaged
- **Pre-Onboarding:** we kicked off our side, vendor hasn't responded; promote to Onboarding when they reply (don't fake the progress)
- **Live:** active flow
- **Paused:** flow stopped but relationship live (returns, capacity, seasonal)
- **Dead:** door open, no flow, no active work
- **Do Not Restart:** burned bridge, blacklist marker

Stage transitions are observable events. The brief shows the stage; the rules around the stage gate what you're allowed to do.

## What the model buys you

Two things:

1. **Decisions become legible.** *"Should I send Vendor X an invoice?"* used to require remembering whether they're live, paused, returning, or behind on payment. Now you render the brief and the answer is there.

2. **Work compounds.** Every email you read, every contract you forward, every payment you chase: all of it updates the vendor record. Tomorrow's brief is richer than today's because today's work fed it. Compare to the default mode where every email is a one-off and nothing accumulates.

## What this requires

You have to be willing to keep the vendor record current. The discipline of *"every state change touches the record"* is what makes the whole thing work. The rules in chapters 5 and 6 are mostly about that discipline.
