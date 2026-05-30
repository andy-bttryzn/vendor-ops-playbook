# 10 — Voice and Tone

## The shape

Direct. Plain. Compressed. No filler.

A vendor reading your email should be able to tell what you want from them in the first sentence. The second sentence is context if they need it; otherwise it's noise.

## The closing

Every outbound is signed with a consistent pair: a one-word greeting followed by your name, each on its own line. The pair is your signature. Inconsistency reads as carelessness.

If you ever try to swap "Thanks," for "Best," in a moment of varied politeness, just don't. Pick one and stay.

## No em-dashes

LLM-generated text leaks em-dashes (`—`) constantly. If your house style doesn't use them, the validator in [chapter 4](04-draft-validation.md) catches them at staging. The substitute is commas, periods, parentheses, or hyphens. Almost always one of those works.

The reason this rule exists is that the *presence of em-dashes is the single strongest tell that text was machine-generated*. If your voice is built on directness, leaking AI tells corrodes it fast.

## No "I hope this finds you well"

And no "I hope you're doing well." And no "I wanted to circle back." Cold opens that telegraph "this is going to be a long ask" make the reader brace.

The replacement is just *say the thing*. "Quick question on X." "We need a decision on Y by Z." "Following up on the thread from 5/22."

## No offering to "jump on a call"

Don't proactively offer calls. If the vendor wants a call, they'll ask. Offering one telegraphs that you've given up on resolving the thing async.

The exception is when you actually need a call (real-time problem-solving, high-context handoff, relationship recovery). Then schedule one. But don't default-offer.

## No apologies for being slow

A draft that opens with *"Sorry for the delay"* concedes ground you don't need to give. The recipient already knows the delay; you don't need to draw attention to it. Open with the substance.

If the delay genuinely affected them, acknowledge it once and move on. *"Got delayed on this. Here's the answer:"* Done.

## Adverbs, not adjectives, when modifying verbs

"Run cleanly" not "run clean." "Ship smoothly" not "ship smooth." The `-ly` is doing work; don't drop it. This sounds pedantic; it's the difference between sounding like you wrote the message and sounding like a Slack message got copy-pasted.

## Pronouns

Don't default to he/she/his/her for a contact you've never met. Default to they/them, or use the name. The cost of a misgendered email is real; the cost of "they" reading slightly formal is zero.

## Internal vs external honorifics

If your culture uses honorifics for senior internal recipients, use them. Externally, default to first name only. Pick the convention for your shop and stay.

## No internal names externally

Sister-company staff names, internal affiliate names, internal channel URLs, internal stage-direction comments: none of these appear in external comms. The exception is when the external party is being introduced to a specific named internal contact, in which case it's intentional.

## No vendor abbreviations

In chat, brief, or email, refer to vendors by their full canonical name. "BR" might be Blue Raven internally; externally it's just confusing. Internally, when in doubt, full name. The cost of typing four extra characters is less than the cost of a misroute.

## Direct verbs

"Can you confirm" > "Can you please kindly confirm." "We need" > "It would be greatly appreciated if." Hedging is friction.

The exception is when you're asking a favor or pushing back on someone with leverage over you. Then softer is fine. The default is direct.

## Attach when referenced

If your email mentions a specific document by name, attach it. Don't link to a folder and let them find it. Don't reference "the contract" and assume they'll dig it up.

## Calendar links inline

Any email that says *"grab time on my calendar"* includes the actual URL inline. Asking the recipient to figure out which URL is friction.

## The final scan

Before any draft ships, scan for:

1. **LLM tells:** em-dashes, *"in conclusion,"* *"furthermore,"* triple-clause sentences with the rhetorical *"not just X, but Y."*
2. **Mojibake:** `â€"`, `â€™`, anything that decoded wrong upstream
3. **Forbidden closings:** the list in [chapter 4](04-draft-validation.md)
4. **Stale recipients:** the To/Cc/Bcc that came from a thread that's drifted in subject. Does it still make sense?

This is the gate before send. Two seconds of scanning is much cheaper than one wrong send.
