# Agentic coding field manual

I started using coding agents after I hurt my hand. The first version of this manual described the setup I built then: one agent in one terminal, plan mode, a diff I read before every commit. Its thesis was "you drive, AI types."

That stopped describing my work. Today one chat at my terminal coordinates a fleet of agents. They build in their own git worktrees, review each other across model vendors, merge their own pull requests when I grant it, and check the result in staging and production. Some runs last days. I type little code, and I don't read every diff.

My part is narrower and harder. I decide where the work goes, and I judge what comes back. This manual is about spending my attention on those two jobs and on nothing else.

I rewrote it from evidence. I read two weeks of my own sessions: 84 working sessions across my agent setup, two projects at work, and phi-router, an open source project of mine. Every practice here is something I did, or a correction I had to make more than once.

## The new problem

With one agent, the risk was loss of agency. You stop thinking and become a passenger in your own codebase. That risk is still here, but the volume of agent work changed it. The [No AI Slop manifesto](https://www.slopmanifesto.com/) says so in its first belief:

> AI is the most useful tool most of us have ever worked with, but a swarm of agents can produce more work in a single day than a person can review in our lifetime.

And it defines slop:

> Slop is when we put less effort into producing something than we ask the consumer to spend understanding it.

With one agent, typing was the bottleneck. With a fleet, I am the bottleneck, because my reading time runs out first. An agent that sends me a 25-item action list, a 20,000-line pull request, or a status update full of its own invented terms has moved its work onto me. That is slop, even when every line in it is correct.

## The mental model

The manifesto lists five values. Each one maps to a rule I hold agents to.

| Value | What it means in my setup |
| --- | --- |
| Outcomes over output | Every task starts with a definition of done I can measure. Lines, PR counts, and agent counts don't matter. |
| Understanding over speed | Agents restate the goal and question the premise before they build. |
| Our own thinking over a model's first draft | I set the destination and correct the premise. The agent proposes the route. |
| Better work over easier work | Proof on the real system, a reviewer from another vendor, and a pass that deletes code. |
| Improving the system over patching the output | A mistake I correct twice becomes a rule, a check, or a gate. |

**I own the destination and the judgment, and agents do the work.** The rest of this manual is about keeping my attention on the first part.

## What is in this manual

- [The harness at work](01-harness.md) follows one real project through my setup, start to finish.
- [The repo agents work in](02-the-repo.md) covers the shared documents, checks, and tests a repo needs before agents touch it.
- [Align before autonomy](03-align.md) is how a task gets a destination before any agent runs alone.
- [Delegate the work](04-delegate.md) is how the work gets split across agents and how far they may go.
- [Verify in proportion to the stakes](05-verify.md) is what proves a change works, and what that proof costs.
- [Subtract](06-subtract.md) is the habit agents lack most.
- [Write for the reader](07-write.md) is the manifesto applied to every word an agent produces.
- [Sessions end, work doesn't](08-memory.md) is how work survives restarts, compaction, and handoffs.
- [Fix the system, not the output](09-fix-the-system.md) is how a correction becomes structure.
- [Anti-patterns](10-anti-patterns.md) lists the failures I corrected most often.
- [The manifesto appendix](appendix-manifesto.md) maps each clause of the manifesto to the practice that serves it.
- [The harness appendix](appendix-harness.md) lists the parts of my setup for reference.

## Who this is for

This manual is for engineers who already ship with coding agents and now run more than one at a time. If you are still deciding whether to use agents at all, read the manifesto first. This manual assumes you already have opinions about linting, types, and tests.
