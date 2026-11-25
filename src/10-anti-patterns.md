# Anti-patterns

These are the failures I corrected most in two weeks of sessions. Each entry names what the agent did and what it should do instead. Most of them became a rule or a check in the harness, as in [chapter 09](09-fix-the-system.md).

## Agent anti-patterns

Earlier chapters tell these in full:

- Building when asked to propose, and reading a question as an order. See [chapter 04](04-delegate.md).
- Shrinking the scope, or swapping the outcome for a proxy. See [chapter 03](03-align.md).
- Calling a project "at risk" from projected dates. See [chapter 04](04-delegate.md).
- Verification that outgrows the change. See [chapter 05](05-verify.md).
- Writing as if the reader shared the agent's context. See [chapter 07](07-write.md).

The rest:

**Inventing stakeholders.** An agent planned sign-offs from a manager and a colleague on a project I lead alone. "There would be no signoff, I'm the new project leader." Don't add people to a process.

**Escalating what is already decided.** An agent wanted to rotate a password I had already judged safe, after I had told it to drop the matter. Raise a risk once, with evidence, and then respect the decision.

**Locking the human out.** A safety control in phi-router stopped me from switching models in my own session. "If I choose to break the seal, that is something I choose." A control that guards against agents must not overrule the human.

**Asking what it could find out.** Credentials sat in the vault. A meeting about a user's workload sat transcribed in the evidence folder, and the agent asked me about it anyway. "It is transcribed and in your evidence already."

**Caution that kills the value.** The first version of phi-router sent so many requests to the compliant account that it cut costs by only 18%. The target was 80% or more. A fail-closed default is right only when it leaves the product useful.

**Heartbeats with nothing in them.** A "nothing changed" report every few hours is noise. Report when something changes, and slow the reports down when nothing will.

**Idling in a self-made wait.** An agent gave itself a ten-minute hold before a merge and sat in it. "What are you waiting for?"

**Stopping at the first blocker.** An agent that hit a login problem proposed asking the customer to change their email, on the account they could not reach. "We cannot tell the customer to change his email if he cannot access his own account." Try the next path.

**A stalled delegate nobody stopped.** An owner spent a whole day producing a demo video. The root checks on long jobs and restarts or stops the ones that stall.

## My anti-patterns

**Bulk approval without reading.** I answered "agree on all six picks," and those picks filed issues I closed as noise the same night. I had fallen for [automation bias](https://en.wikipedia.org/wiki/Automation_bias), the habit of trusting a machine's suggestion without checking it. A one-line "agree" is a review, so I read the picks before I type it.

**The acceptance spiral, at fleet scale.** The old manual warned about accepting one diff after another until you are a passenger. With a fleet, the spiral is approving plans, merges, and messages faster than I understand them. [Chapter 05](05-verify.md) describes what I review now. I still don't approve what I don't understand.

**Leaving a mistake in my own docs.** Twice an agent followed my own wrong instruction, once a misnamed term and once a wrong line in a requirements doc. When the source is wrong, I fix the source, not only the output.

## What replaced the three-attempt rule

The old manual said to write the code yourself after three failed attempts. Now the rule is about the premise. When two fixes that rest on the same belief both fail, the belief becomes the suspect. The agent rechecks the premise, the design, and the requirement before it tries a third patch. In one review, the agent stopped after its second failed patch and redesigned the change.
