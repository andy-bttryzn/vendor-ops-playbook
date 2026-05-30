# 12 — 30-Day Adoption Guide

A week-by-week implementation plan for adopting this playbook in a new shop.

This isn't aspirational. Every step has a concrete artifact you should have at the end of it. If you finish a week without the artifact, that week didn't happen. Re-do it before moving on.

## Before you start

**You should already have:**
- A list of every active vendor relationship (rough; you'll clean it as you go)
- Read/write access to your email, your CRM or vendor store (monday/Notion/Airtable/spreadsheet), your contract store (Box/Drive/SharePoint), and your task tracker
- Authority to make process changes in your own work; this playbook assumes you can adopt new rules without checking with anyone

**You should NOT need:**
- Any new SaaS purchase
- An engineering team
- A formal kickoff or stakeholder approval

The playbook can be adopted by one person, in their own work, without telling anyone. The visible outputs (briefs, better-routed emails, cleaner contract handoffs) will sell themselves.

## Week 1 — Make the vendor record

**Goal:** Every active vendor has exactly one record in a structured store.

**Days 1–2.** Pick a tool (monday, Notion, Airtable; pick whatever you already pay for). Create a single "Vendors" base with columns for:
- Name, side (Buyer / Affiliate / Both), status, rating, URL, sourcing
- Verticals (live + other), modalities (live + other)
- Notes (free text)

**Days 3–5.** List every active vendor relationship. Add them to the base with whatever data you can pull from memory in 30 seconds per vendor. Don't try to make it perfect; the goal is *exists*, not *complete*.

**End-of-week artifact:** A "Vendors" base with at least one row per active relationship. Doesn't matter if half the fields are blank.

## Week 2 — Set up the inbox

**Goal:** Layer 1 (filters) and Layer 2 (shortcuts) from [chapter 2](02-the-two-layer-inbox.md) are running.

**Days 1–2.** Audit your current inbox for noise. Sort by sender, identify the top 10 noise sources (system notifications, accounting auto-emails, dispo reports, newsletters). Build Gmail filters for each, dumping to `03.noInbox/{category}`.

**Days 3–4.** Build the vendor-scoped label set. For each vendor in the base, create `zzzVendors/{Name}`. (Most stores support a CSV export → bulk-create-labels via Gmail API.)

**Day 5.** Define your shortcut set for triage. At minimum: reply / brief / bury / snooze / forward. Bind them to keyboard shortcuts or AI commands you can fire quickly.

**End-of-week artifact:** Inbox drops to <50% of where it was. The vendor label list covers every active relationship.

## Week 3 — Make briefs render

**Goal:** You can render a working brief for any vendor in <10 seconds.

**Days 1–2.** Define the `vendor.json` data contract for your shop. Decide which fields matter; check the renderer's schema in [vendor-brief-renderer](../../vendor-brief-renderer/).

**Days 3–4.** Wire a fetcher that, given a vendor record ID, pulls the data from your store and outputs `vendor.json`. This is the most adapter-heavy step; expect a day per data source.

**Day 5.** Connect the fetcher to the renderer. `node fetcher.js {id} | node vendor-brief-renderer/index.js -` should produce a clean brief.

**End-of-week artifact:** A one-command brief render for any vendor in the base. Use it for the next 5 vendor decisions you make and notice the difference.

## Week 4 — Discipline layers

**Goal:** Draft validation, label semantics, and task lifecycle are habits, not aspirations.

**Days 1–2.** Stand up draft validation. If you're sending via Gmail API: integrate `gworkspace-helper` (or equivalent) with your env vars set. If you're sending manually: write the closing pair, the forbidden-closings list, and the legal-BCC criteria on a sticky note. Train yourself for 2 days; the muscle memory is faster than you think.

**Days 3–4.** Migrate every Open Item across all active vendors into your task tracker. Spawn them with proper status (Waiting on us / Waiting on them / etc.). Resist the urge to do work; the goal is *captured*, not *done*.

**Day 5.** Run the audit query for the first time. *Show me tasks with status `Waiting on Client` whose last outbound was more than 7 days ago.* Whatever that returns is your dunning queue.

**End-of-week artifact:** Three observable changes: (a) you sent at least one draft that was blocked at the validation gate and you fixed it, (b) you can run an audit query that returns real follow-ups, (c) at least one vendor has been moved through a status transition this week with the labels swapped correctly.

## What you have at day 30

A working vendor-ops system that:

- Renders briefs on demand
- Catches your own mistakes at the staging gate
- Surfaces what's owed and by whom
- Lives in tools you already had

You did not buy new SaaS. You did not run a process-change project. You did not block on anyone else's adoption.

The next layer (wiring an AI assistant into this, automating the repetitive triage, expanding to a team) is [chapter 9](09-ai-assistant-discipline.md) territory, and it's cleaner to add after day 30, not before.

## When this fails

Three common failure modes:

1. **You skip week 1.** You start with inbox triage because email is what's screaming. By week 3 you have no record of who you're triaging *for*, and the briefs can't render. → Always do week 1 first, even if email is screaming.

2. **You over-engineer the data contract.** Week 3 turns into a month because you're trying to model every edge case. → Ship the minimum schema that lets the brief render. Add fields as you hit the cases that need them.

3. **You don't change your own behavior.** The base is built, briefs render, but you keep replying to email the way you always did. → The point of the system is that *you read briefs before deciding*. If you skip that, the rest is theater.

## For consultants standing this up at a client

- **Week 0 is data audit.** Before day 1, understand what stores the client already has and which one becomes the vendor base. Don't introduce new tooling unless absolutely needed; adoption is the bottleneck, and new SaaS is friction.
- **Get the brief working before evangelizing the playbook.** A rendered brief is the artifact that sells the system. The chapters are post-hoc explanation, not pre-adoption material.
- **The first 5 briefs you render in front of the client are the persuasion.** Pick vendors with active drama. The brief should reveal something they didn't know.
- **Don't write the draft-validation rules until you've seen them ship one bad email.** The rules feel pedantic until you have a fresh example.

The system survives because every rule was justified by a specific failure mode. The fastest way to make a client believe is to wait for the failure mode, not to argue from first principles.
