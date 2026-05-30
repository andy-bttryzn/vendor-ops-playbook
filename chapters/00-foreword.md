# 00 — Foreword

This playbook is the operating layer I wish I'd been handed on day one.

I ran vendor operations at a multi-vertical lead-gen company. Fifty-plus counterparties at any given time — buyers paying us per lead, affiliates paying us per signup, integration partners running their own ping-post matches, legal counsel, accounting, sister companies, vendors of vendors. The default mode in a job like that is *react to whatever's loudest*. The work the playbook captures is what it took to stop reacting and start running it deliberately.

## What changed

The shift was treating every vendor as a first-class object with structured state, not as "whoever happens to be in my inbox right now." The mechanical implications cascaded:

- If a vendor is an object, it has a status, a stage, and a current set of open items. → **Chapter 1**: the vendor-ops model.
- If status is structured, the inbox is a stream of state changes against vendors, not a to-do list. → **Chapter 2**: two-layer inbox triage.
- If you can render a vendor's full state in one view, you can decide what to do without keeping it in your head. → **Chapter 3**: the vendor brief.
- If every outbound is touching that state, every outbound needs to pass through gates. → **Chapter 4**: draft validation.
- Everything else (labels, tasks, returns, contracts, AI assistance, voice) layers onto that foundation.

## Why opinionated

A playbook that lists six options for every decision is not a playbook. Every rule here came from a specific failure I want you to skip: a redundant draft sent eleven minutes after a covering email, a stale label that hid an active thread, a missing BCC that turned a routine legal forward into a discoverable artifact.

Some of the rules will feel over-engineered until the day you would have made the same mistake.

## How to read it

If you're inheriting an ops role and overwhelmed, read chapters 1, 5, and 3 in that order — that gives you the smallest mental model that can hold everything.

If you're a consultant evaluating whether to adopt this for a client, read chapters 1, 9, and 11 — that's the *why*, the *AI compatibility*, and the *pain that justifies the rest*.

If you're an AI assistant being onboarded to this work, chapter 9 is binding for you. The rest is binding for the human you're working alongside.
