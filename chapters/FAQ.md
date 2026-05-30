# Common Questions

Questions a prospective adopter (or consulting client) tends to ask before committing. Answered honestly, not promotionally.

## "Why not just use [vendor management SaaS]?"

Three answers, in increasing depth.

**Surface:** vendor management SaaS solves vendor *procurement*, not vendor *operations*. Procurement is upstream — vetting, onboarding, contracting. Operations is what happens after the contract is signed and the work has to actually run. The SaaS market hasn't filled that gap yet because it's hard to template.

**Working:** even the SaaS that does cover ops (Vendr, Tropic, Zip, etc.) is built for an IT / procurement org with hundreds of vendors and a finance lens. That's a different shape than a lead-gen or channel-partner org with fifty vendors and a revenue lens. Different unit of work, different decisions per week.

**Honest:** the SaaS market may catch up. Until then, your inbox + structured store + this playbook is more responsive to what your specific shop actually needs.

## "Will this work for X type of business?"

Sweet spot:
- Lead-gen agencies, exchanges, aggregators
- Channel-partner organizations (re-selling, white-labeling)
- Marketplace operations (any side of a two-sided market)
- Affiliate networks
- Anywhere with 30+ counterparties pushing email, contracts, invoices, returns

Borderline:
- Software vendors selling to a small number of enterprise accounts (the brief shape works; the volume doesn't)
- Customer-success orgs (the brief is more about *transactions* than *relationships*; CS is heavier on relationships)
- Procurement / supplier-management orgs (procurement-specific SaaS is probably a better fit)

Doesn't fit:
- Direct-to-consumer (no vendor relationships in the sense this playbook means)
- Single-vendor partnerships (overkill)
- Internal team management (this is about *external* counterparties)

## "How long until I see ROI?"

Honest answer: **30 days for the operator, 90 days for the org.**

- Day 7: vendor record exists, inbox is partially triaged. You start feeling lighter.
- Day 30: briefs render, drafts pass through the gate, no more accidental dupes. Your output looks more consistent.
- Day 60: status questions get answered in seconds, not minutes. Other people in the org notice and start asking *"can I see the brief on X?"*
- Day 90: the system has paid back the adoption cost in saved hours and prevented errors. You can scale to 2x the vendor count without hiring.

If you're 30 days in and don't feel it, you skipped a chapter. Most often: week 1 (vendor record) or week 3 (briefs).

## "What if I'm on Outlook instead of Gmail?"

The label model is Gmail-flavored but generalizes. Outlook calls them *categories* and *folders*; same underlying concept. The two-layer inbox model works because of *automatic routing rules* + *manual triage discipline*, neither of which is Gmail-specific.

The `gworkspace-helper` is Gmail-specific. For Outlook, you'd write a Graph API equivalent. Most ops shops can adopt the playbook on Outlook and skip the helper.

## "Can a small team adopt this incrementally?"

Yes, but order matters.

**Solo operator → small team:** start solo. Adopt all 12 chapters yourself. Once your work is visibly faster and more consistent, the team will adopt the parts they need without you having to push them.

**Team-first adoption:** doesn't work. You'll spend three months socializing the labels, building consensus on the brief format, getting buy-in on the draft-validation rules. Half the team will be selectively complying. The system never becomes load-bearing.

The play is *demonstrate, then invite*. Not *propose, then negotiate*.

## "Does this work without AI assistance?"

Yes. The chapters that mention AI are 9 (operating discipline) and the AI-specific bits in 4 (draft validation gates). Everything else is human-only operable.

That said: the system gets *much* more leverage with an AI assistant doing the rendering, the validation, and the triage. The shape of the playbook was finalized after wiring Claude Code into the loop; without AI, expect to do more work yourself for the same output.

## "What stack do you actually recommend?"

If you're starting fresh and have the freedom to pick:

- **Email:** Gmail. The label model + filters + search + API maturity is unmatched.
- **Vendor store:** monday.com if you want the visual interface to be load-bearing; Airtable if you want the schema flexibility; Notion if you're already there; a Postgres table if you can write a small UI.
- **Tasks:** same store as vendors (cross-board relations matter).
- **Contracts (signed):** Box or Google Drive. Pick the one your legal team already uses.
- **Contracts (in flight):** Airtable's a good fit. Standalone trackers like SpotDraft or Ironclad work too if budget allows.
- **AI assistant:** Claude Code (this is what the playbook is tuned for); Aider works too.

If you have existing tools you can't move off:

- The playbook works on any stack. The chapter-by-chapter adoption is what matters; the specific tools are interchangeable.
- The biggest constraint is *unified labels across email*. If your email tool doesn't support a label system, you'll work harder.

## "How is this different from a CRM?"

A CRM tracks the *relationship* (deals, pipeline, accounts, opportunities). The vendor-ops layer tracks the *operation* (current state, open items, recommended actions today).

They overlap. In practice:
- Your CRM stores the static-ish view (who they are, what they buy)
- The vendor-ops layer stores the dynamic view (what's open right now)

Many shops conflate the two and end up with a stale CRM and an ad-hoc ops layer in their inbox. The split is the fix.

## "What's the failure case where this gets abandoned?"

Three patterns:

1. **Adopt the labels but not the briefs.** You end up with a more-organized inbox that's still answering the same status questions verbally. → Push through to chapter 3.
2. **Adopt the briefs but not the validation gates.** You catch yourself sending a redundant or off-tone email and shrug. → The gates exist because of the failure mode. Wire them in.
3. **Adopt for a quarter, then drift.** Q4 happens, holiday crunch hits, you skip a few briefs, the labels get behind. By Q1 you're back to scrolling inbox. → The system has to survive a bad week. Build the simplest possible version of each layer first; you can elaborate later.

The system survives because every rule was earned. Trust that, and rebuild from the simplest version when you drift.

## "Is the playbook prescriptive or descriptive?"

Both, by design.

- **Descriptive** for what we found works: the 10-section brief order, the four-dimension label model, the closing-pair voice rule.
- **Prescriptive** for the discipline: the draft validation gate, the dedup-before-create, the verify-after-mutation.

The shapes are findings. The discipline is the price of keeping the shapes load-bearing.

## "Can I see this running?"

The `vendor-brief-renderer/examples/csv-adapter/` pipeline is an end-to-end demo: CSV in, structured JSON in the middle, rendered brief out. Five minutes to run. That's the smallest possible working example.

A real working installation is harder to share publicly (vendor data is sensitive). If you're seriously evaluating, a paid pilot is the right shape.

## "What's not in the playbook?"

A few things deliberately out of scope:

- **Vendor selection.** This is for vendors you already have. Picking them is a different problem.
- **Pricing and negotiation.** Mentioned in passing; not the focus.
- **Team scaling.** The playbook is single-operator-oriented. The team version is a follow-on.
- **Industry-specific compliance.** Generic principles; your vertical's compliance rules (HIPAA, FCRA, GLBA, TCPA, etc.) are yours to layer on.
- **Reporting / dashboards.** The brief is the daily artifact. Weekly / monthly aggregations are out of scope.

If your shop needs one of these, the playbook isn't enough on its own. It's still the starting point.
