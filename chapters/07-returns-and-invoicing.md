# 07 — Returns and Invoicing

## The structural problem

Returns in a per-lead / per-impression / per-transaction model are messy because every counterparty wants them done their own way. Some accept a Google Sheet with a row per returned lead. Some require entries in their portal. Some take an email and trust you. Some refuse to acknowledge returns at all and apply a blanket haircut to the invoice.

The structural fix is a **per-counterparty Return Type** field, a single lookup on the vendor record that tells you which protocol to run.

Common types:

- **Google Sheet / Worksheet**: you compile a per-lead matrix, send to your accounting team, they apply credits
- **Vendor portal**: log into their tool, mark each lead returned, hope it syncs
- **Email-to-accounting**: you email their AP with the disputed leads
- **Disposition ping-back**: automated; your system pings their API with the dispo, no human in the loop
- **Invoice haircut**: they apply a fixed percentage reduction; you reconcile but don't request line-item credits
- **No returns**: you eat the bad leads; built into the price

## The Returns Worksheet pattern (Google Sheet flavor)

When a counterparty uses the worksheet flow:

1. **Per-vendor tab.** D2 = invoice number. A through H rows 5+ = per-lead data: email subject, date, publisher, buyer:campaign, lead email, publisher cost, total cost, *"bigger?"* (whether this is a high-value loss).
2. **Auto-built email body.** Columns I and J onward have formulas that assemble the credit-ask email body. Don't touch the formulas; they encode the format your accounting team expects.
3. **Credit-ask is a reply.** You do not compose a fresh email. You reply to the original invoice email thread, paste the matrix from columns I/J into the body, with a stamp block (vendor / invoice # / date+time), the matrix rows, then a totals row, then *"Please update and (re)send invoice to buyer. Thanks!"*
4. **Pub $ stays blank to accounting.** The per-lead matrix and the totals row send to accounting with `Pub $` column blank. Only `TTL $` is filled. The publisher cost is internal margin; accounting doesn't need it.
5. **Override `--to` to accounting.** The credit-ask reply goes to your internal accounting alias, with sales BCC. Never let reply-all include the buyer.

## The non-worksheet flavors

- **Vendor portal.** Just do it. No email needed unless something fails to register. Document the URL in Helpful Links.
- **Email-to-accounting (vendor's accounting).** Direct email with the per-lead matrix; don't loop your own accounting in.
- **Dispo ping-back.** Automated; your platform pushes the dispo via API. Your role is monitoring that the integration runs, not composing emails.
- **Invoice haircut.** When the invoice arrives, expect the cost to be ~X% lower than your internal pub total. Reconcile; if the gap is significantly off, send a clarification ask.

## Invoice payment tracking

Every accounting invoice you encounter gets a tracked task. Subject + invoice number + vendor in the task name; payment link in the Notes. Status moves through:

- **Waiting on Client**: invoice sent, payment due
- **Waiting on Client (partial)**: partial payment received, balance outstanding
- **Done**: paid in full
- **Abandoned**: uncollectible

Partial-paid is not Deferred. Partial-paid is active dunning.

Auto-invoices snooze until *day-after-due*. When they resurface, that's the payment-chase trigger, not a "review". Start the chase that day.

## Small-balance threshold

Counterparties with a minimum payment threshold (we'll only invoice once total crosses $X) get that threshold in the vendor record. Saves you the embarrassment of sending three $40 invoices to someone who's batching until $200.

## Reconcile before paying

Inbound invoices (someone billing *you*) get the inverse treatment: pull the reporting from your platform for the invoice timeframe, sum what you owe, match totals to the invoice line. Don't pay first and reconcile later; once the money's gone, the leverage to fix a billing error evaporates.

## What to write down

Per-vendor, capture in the record:

- Return Type (lookup)
- Payment terms (Net-X)
- Min payment threshold (if any)
- Standard invoice cadence (weekly / monthly / per-transaction)
- Any haircut percentage applied to invoices
- Whether the vendor accounts on calendar month or another period

All of this is friction-removal. Every time you have to re-derive one of these from old emails, you've paid for not having written it down.
