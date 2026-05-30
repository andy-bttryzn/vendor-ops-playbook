# 04 — Draft Validation

## The rule

Every outbound email passes through a validation gate before it's staged as a draft. No exceptions.

This is the single most-violated rule in the playbook and the one whose violation is most expensive. A sent email is harder to take back than almost any other action you take.

## What gets validated

### Body content

- **Em-dashes.** LLM-generated drafts leak `—` constantly. If your house style doesn't use them, block at staging time. Forces a rewrite, not a "send anyway" override.
- **Forbidden closings.** "Best," "Best regards," "Sincerely," "Cheers," "Regards." Pick what you don't write and reject those at the gate. The point isn't that they're wrong; the point is that *your* style is your signature, and inconsistency is noisier than the reader notices.
- **Required closing pair.** If your style is `Thanks,\n[Name]`, the validator enforces both lines present and in that order. Catches the case where you (or the AI) generated a body that just ends.
- **Empty subject.** Never send an email with a blank subject. Easy to validate, impossible to recover from.
- **Mojibake / encoded-word leakage.** `â€™` and `=?UTF-8?B?` in a subject line means something double-encoded upstream. Catch at staging time.

### Recipients and routing

- **Required BCC on legal-flavored threads.** When the body or subject contains contract / NDA / MSA / amendment / e-sign keywords, require your in-house counsel BCC. Configurable; defaults off; opt in by setting an env var.
- **Sister-domain handling.** If your shop has multiple internal domains (parent, sister companies, dev team), routing should default to *coworkers on Cc, vendor on To*, not reply-all-flatten.
- **Prior outbound check.** Before staging a fresh-thread send to anyone, glance at recent sent mail to the same recipient. If you sent them something different in the last 48 hours on another thread, surface it. Catches the case where two stale self-notes generated two parallel emails.
- **Ownership pre-flight.** On reply, if a coworker has more outbound on this thread than you, throw; the thread is theirs, you're parallel-drafting. Override only with explicit reason (OOO, explicit handoff, vendor asked for you).

### Render quality

After Gmail accepts the draft, fetch it back and lint the *rendered* HTML:

- 3+ consecutive `<br>` tags in new content
- Empty `<p></p>` blocks
- 4+ consecutive newlines in plain text
- Encoded-word leak into the decoded Subject

If any check fails, **delete the draft and throw**. A broken draft that survives reaches the user with an "ok" URL and gets sent.

## Stage, lint, send

The three-step pattern:

1. **Stage:** create the draft (with all validation above)
2. **Lint:** post-create read-back validation; delete on failure
3. **Send:** explicit human approval gate; the same word every time

"Send it" means **one** specific email: the one in the immediately prior message. Not *"start sending stuff."* Not *"work through the queue."* One.

The AI assistant doing the drafting does not get to interpret "looks good" or "lgtm" as send authority. The explicit word is the gate.

## Why this is non-negotiable

The cost of a wrong send compounds:

- A duplicate redundant send burns trust with the vendor *and* makes you look uncoordinated internally.
- An LLM-toned cold-open ("I hope this finds you well!") in your house style breaks the voice consistency you've spent years building.
- A legal-flavored email missing the BCC creates a discoverable artifact the lawyer needed to be in the loop on.
- A reply-all that picked up an internal stage-direction message ("draft this for me") and forwarded it to the vendor is a career-defining moment.

Every gate above exists because someone hit the failure mode it catches.
