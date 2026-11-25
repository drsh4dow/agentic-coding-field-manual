# Delegate the work

> AI cannot replace human judgement, it can only amplify our judgement (or lack thereof).
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), belief 4

Delegation multiplies whatever the root does, mistakes included. A vague destination sent to six owners comes back as six pull requests built toward the wrong goal.

## The shape of a run

A typical run in my sessions goes like this:

1. The root aligns with me, as in [chapter 03](03-align.md).
2. The root sends read-only scouts to research, often one per area.
3. The root cuts the work into slices by what depends on what, not by the order features go live.
4. One owner per slice builds in its own git worktree, on the `judgment` model.
5. A verifier from another vendor checks each pull request at its exact head commit.
6. The root merges what passed, deploys when I granted it, and uses the result on the real system.
7. After each wave of slices, a cut pass deletes what the wave did not need. See [chapter 06](06-subtract.md).
8. I get one handoff pull request, or as few as the work allows.

## Size the work to a session, not a calendar

I used to plan in dated milestones. Then I grouped work into waves, each one sized to a single session of the harness. By the end of the two weeks I gave a whole project to one session.

Dates hurt agent work, because agents underestimate their own speed. One agent marked a project "at risk" by projecting dates that were not part of our plan, while the pace we had measured said otherwise. My instruction now is to "give tasks and owners and let them run, don't mandate dates, the key is to have a clear DoD." Measure the pace you have, not the pace a human team would have.

## Grants are explicit and end with the session

An agent works alone only when I say so, in words, in that session:

> Operate autonomously, work end to end. The DoD is the 2.5-hour target. Don't stop until that is reached.

A grant names what it covers. In two weeks my grants included opening pull requests without asking, merging once a verifier passed, writing to production, and running an infrastructure apply. A grant written in an old handoff note is history. A new session needs my word again.

Some things wait for me even under a grant, such as force-pushes to shared branches, data deletion, and messages to people. Amazon calls these [one-way doors](https://s2.q4cdn.com/299287126/files/doc_financials/annual/2015-Letter-to-Shareholders.PDF), decisions you can't undo, so they get care instead of speed. A pull request is a two-way door, because a revert undoes it. [Chapter 07](07-write.md) covers how messages to people work.

## Don't make me the relay

An agent that stops to ask me for a password prompt, a login, or a file it could fetch has made me its relay. I set up the tools so it doesn't have to:

- A 1Password auto-approver runs as a background job, so agents read the secrets they need without me clicking approve. "I don't want to approve them for you, feel free to access anything you need."
- A shared browser profile holds my logins. The agent drives the flow, and I type only a password or a code.
- For a step only I can take, the agent writes a guided script with the `wizard` skill, and I run it.

Access is not permission to get past every check a site puts up. In my shared browser one agent kept clicking through a CAPTCHA and account recovery screens, and it captured a recovery code on the way. "Dude, what are you doing?" When a site asks for proof that a human is present, the agent stops and asks me.

## Swarms, arenas, and adversaries

Three patterns cover most fan-out:

- A **swarm** splits one job into slices, gives each slice to a leaf, and merges the reports. This manual came from one. Ten leaves read 84 sessions, one leaf mapped the harness, and the root merged the eleven reports.
- An **arena** races several candidates on one brief, has a judge from another vendor rank them, and combines the best parts into one result. I use it for designs where a single attempt could settle on the wrong shape.
- **Interrogate** sends adversaries on several models to break a change. A finding counts only if they prove it with a run. It runs after a second failed review of the same pull request, not on every change.

## Respect the model table

The model table in [the harness appendix](appendix-harness.md) is a rule, not a hint. Early on, a root running my most expensive model started every helper on that model too, because its briefs named no model. "Don't use that model, it is only allowed for yourself." Now every delegate names a model from the table.

## Steering a running fleet

I steer while the run goes. The messages are short:

- "Report progress." "Why is this taking so long?" Both ask for the current state and what blocks it.
- "Pause the work, I'm going to reboot." [Chapter 08](08-memory.md) covers what the root does next.
- "Kill the last child, it runs a task that will take days." The root owns every job it starts and can stop any of them.

A question from me is not an order. Once I asked "what about the seven open issues?" The agent read it as a go-ahead and started six owners to fix them. I had asked why it filed them. "I didn't ask you to implement them, I was asking why you filed those." When a message from me ends in a question mark, the agent answers it.

## Keep the hard writing at the root

Some work doesn't delegate well. Prose that needs the whole context of the run, such as a system prompt rewrite or a design decision, stays with the root. "As this is prose that requires deep knowledge, I want you to write them, not delegates." A delegate sees only its brief, and the root has the whole conversation.
