# 08 — Contract Intake

## Where signed contracts live

One canonical store. Pick one — Box, Drive, SharePoint, whatever your shop uses — and treat it as the source of truth for *signed* paper.

The naming convention matters less than the discipline of *every signed contract gets a file there with a predictable name*. We use `{Vendor Name} {Doc Type} {YYMMDD}.pdf`. You can pick differently; just pick.

Helpful Links on the vendor record points at the Box/Drive file. Briefs surface the link in section 5. When someone asks *"what does our contract say about X with Vendor Y,"* the answer is one click from the brief.

## Where unsigned contracts live

A separate tracker for *paper in flight*. We use an Airtable base; you can use whatever supports per-row attachments, status, and assignee. The tracker handles:

- Counterparties whose paper we're redlining
- Counterparties on whose paper we're on the redline (their paper, our redlines)
- Doc Type (NDA / MSA / IO / Amendment / DPA / etc.)
- Vertical (which line of business)
- Sister Co (which entity is on our side)
- Notes (relevant context, sticky points, deadlines)
- Attachment (the live draft)

**Status is left null on intake.** Your legal team owns the Status field. If you set it on creation, you're stepping on their workflow.

**Required at intake:** Doc Type, Contract Owner, Whose Paper, Vertical, Sister Co, Notes, Attachment. Missing any of these means the legal team has to ping you for context — bottleneck.

## The forwarding rule

Every contract forwarded to your legal team **also** gets a row in the tracker with the contract attached. The forward and the tracker entry happen at the same time. Skipping the tracker entry means legal opens an inbox-driven task instead of a tracker-driven one, and their queue starts to drift.

## Don't update tracker when paper is signed

When a contract that was in the tracker gets signed, the right move is **email legal** with the signed file + link to the Box/Drive location. Do not flip the tracker entry to "Signed" yourself — legal owns that transition, and updating it yourself can mask a downstream sync gap.

If you notice the tracker shows a contract in-flight but you know it's signed and in Box, that's a *drift signal* to surface to legal, not a thing to silently fix.

## Attach when you reference

If an email references a specific contract by name (*"per our MSA, section 4.2..."*), attach the actual file. Don't make the reader hunt. This is the highest-value low-effort rule in this chapter.

## The e-sign mention

Choose your e-sign tool, document it in the playbook for your shop, and use the same name every time externally. If you've moved from DocuSign to Box Sign to Dropbox Sign, externally say "e-sign" generically; internally, name the tool. Inconsistency externally reads as scattered process internally.

When you tell a vendor *"go ahead and use your e-sign"*, append your full signer block — name, title, email, mailing address. The vendor's tool will ask for it; saving them the round-trip is one email's worth of relationship goodwill.

## Legal is "them" externally

Your in-house counsel and your external counsel are referred to as *"our legal team"* / *"them"* / *"they"* in vendor-facing comms. Never by name. Never by firm.

The exception is when legal explicitly tells you to introduce a specific lawyer on a deal. Even then, the introduction is by name once; subsequent references go back to "they."

## Internal honorifics

If your shop uses honorifics for senior internal recipients (suffix, prefix, regional convention), use them consistently. Inconsistency reads as carelessness.

## The compliance carve-outs

When the reason for a rewrite or new contract is compliance-driven (a regulator, a new data law, a customer's new requirement), capture that in the vendor record's notes. Six months later when the next amendment lands, the person doing it (you, your replacement, your AI assistant) needs to know whether the original change was driven by compliance or by tech-debt cleanup. The scope decision is different in each case.
