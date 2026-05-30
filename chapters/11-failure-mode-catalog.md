# 11 — Failure Mode Catalog

A non-exhaustive list of the pain points that justify the rules in the rest of the playbook. Read this when a rule feels over-engineered and you're tempted to skip it.

## Inbox and labels

**Gmail search index lag.** Label changes are visible to the API immediately, but the *search index* that backs `label:xyz` queries lags by minutes. A script that changes a label and then queries the new label state will often see stale results. Always re-verify with `messages.get` or `threads.get` if state matters.

**Mass-trash on a label includes labels that match by substring.** `label:zzzVendors` matches `zzzVendors/Acme`, `zzzVendors/Beta`, and so on. Anything that bulk-operates on a label name needs to either exact-match or paginate-and-verify per-thread.

**`label:"name with spaces"` silently fails.** Gmail label queries don't handle quoted names with spaces well. Use the hyphenated form: `label:name-with-spaces`. This is a recurring footgun.

**Stale filters compound.** A filter set up for last quarter's noise pattern keeps firing after the pattern stops. Audit filters quarterly; delete the ones that haven't fired in 30 days.

## Drafts and sends

**LLM-generated em-dashes are the dominant AI tell.** They will leak into every draft an AI assistant writes unless explicitly blocked at the validation gate. Don't trust "I'll just remember to not use them". Block at staging.

**Prior outbound on a different thread.** A vendor with two parallel threads (one technical, one billing) gets two emails from you in 11 minutes, both addressing the same overdue question but worded differently. The vendor reads both, notices the contradiction, loses confidence. Prior-outbound check at staging catches this.

**Coworker-owned threads.** If a coworker has more outbound on a thread than you, parallel-drafting on that thread produces a redundant reply from your domain. The vendor doesn't know which one to act on; the coworker is annoyed. The ownership pre-flight catches this. Override only with explicit reason.

**Reply-all preserves include lists.** If you set up the original thread with Sales BCC'd, reply-all keeps Sales BCC'd. If you reply-all to a forward-from-internal, you'll send the internal stage-direction back outside. Always check the recipient block before pressing send.

**Forward is a send.** A forward is functionally identical to a send. Same validation gate, same approval requirement. The mental category "I'm just forwarding this" is not a license to skip checks.

**The Subject is part of the message.** Subjects without explicit override on a reply-draft sometimes inherit from a bounce notification or a system message, not the original thread. Always pass `--subject` explicitly when in doubt.

## Tasks and tracking

**Duplicate tasks compound.** Without dedup, every recurring touchpoint spawns a fresh task. After 60 days you have 600 open items, most of which duplicate each other, and the task list stops being read. Dedup before create is the only way to keep the list trustworthy.

**Status drift.** *Waiting on Client* on a task we've never told the client about is a lie that compounds. The recurring audit *"who have we asked recently?"* catches this; without it the list rots.

**Abandoned tasks pile up.** A vendor re-engages, you flip the task to active without checking, and create a new one because the old Abandoned status got filtered out of the dedup query. Now you have two tasks for the same thing, different statuses, different histories. The fix: reuse Abandoned tasks on re-engagement; flip status and prepend new context.

## Contracts

**The drift between unsigned tracker and signed store.** Signed paper goes to Box/Drive; unsigned paper is tracked in Airtable. The handoff is a silent gap unless someone explicitly closes the tracker entry when paper is signed. The legal team owns that transition, not vendor-ops; if vendor-ops "helpfully" updates the tracker, the legal sync breaks. Surface drift, don't fix it.

**Missing attachment on intake.** Every contract row needs the actual file attached. A row with no file is a row legal can't act on, and they have to ping you for context. Bottleneck.

## Returns and money

**Pub margin leaks to accounting.** The credit-ask sheet has columns for both publisher cost and total cost. Only total cost goes to accounting. Sending pub cost exposes internal margin information accounting doesn't need.

**Partial-paid invoices read as Deferred.** Partial payment with a balance is active dunning, not deferred. Misclassifying these means the chase doesn't happen.

**Per-vendor return type.** Returning a lead to a vendor that doesn't accept returns burns a real cost (you ate the bad lead and now you also burned cycles). The Return Type field on the vendor record is the gate.

## AI-assistant specific

**"Likely / probably" when verification is cheap.** An AI saying *"the daemon is probably running"* when the daemon's status is one tool call away is shipping uncertainty it should have resolved. Verify when cheap.

**Empty result mistaken for absence.** A query that returns zero rows is a claim, not a fact; it could be a genuinely-empty result, or a malformed query, or a stale index. When you expected non-zero, suspect the query before reporting *"none exist."*

**Same-turn deliverable that's actually backgrounded.** An AI that says *"I'll check on that"* and then ends the turn without checking has lost the work. Same-turn deliverables run inline, never backgrounded.

**Mutation followed by no read-back.** State change that posts 200 OK but doesn't actually apply (because the API quietly dropped a required field, or the auth was scoped wrong) gets reported as success and downstream work proceeds on wrong state. Always read-back.

**Subagent says "DONE" without writing the file.** A subagent dispatched to produce an output file that returns "done" without the file having been written on disk is a known failure mode. Orchestrator verifies the file exists before relaying.

## The pattern

Every entry above has the same shape: *a small carelessness that compounds over time.* The rules in the rest of the playbook are mostly about catching the carelessness before it compounds. They're not about clever architecture; they're about discipline that survives a bad week.
