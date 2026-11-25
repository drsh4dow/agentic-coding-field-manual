# Subtract

> In code, even before AI, slop proliferates when we repeatedly work around problems instead of solving them correctly. It comes from tools that lean HEAVILY toward adding rather than subtracting.
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), belief 6

Agents add. Ask for a fix, and you get the fix plus a helper, a fallback, and a doc page about the helper. Subtraction is the habit agents lack most, so I build it into the process.

## What adding looks like

From two weeks of my sessions:

- A pull request with a diff over 20,000 lines. "Is it truly needed? I seriously doubt it."
- A plugin that shipped minified bundle files to the main branch. I moved the bundle off main and turned off minification.
- An agent that redesigned a tool when a few lines of instructions would do. "Why are we reengineering the owned work tool? Isn't this more related to instructions?" The pull request shrank to five lines.
- A pull request that duplicated a feature the agents already had.
- A pull request that shrank to three lines once I asked what it was for.

## Net negative is the target

A net-negative diff deletes more lines than it adds. "Code simplification and reduction passes, so we always aim for the net negative." Every run of three or more slices gets a cut pass after each wave, done by a separate owner. A cut counts when it removes production code, and it never holds up the next wave.

Before an agent adds anything, it looks for something to delete. Dead code, redundant checks, and stub references go first. Then it builds on what is left.

## Every pull request says why it exists

I ask two questions of every agent pull request. "How much time does it save? Is it worth it?" and "Why does this PR even exist? What problem does it solve?" If the answer is weak, the pull request closes.

## Edge cases tend to infinity

An agent asked to make something robust will find edge cases forever. "Think of this issue as Zeno's Paradox." Each step looks like progress, and the work never finishes.

Now a finding counts only when it has a path a real user takes, and the line in the code that proves it. Everything else is a known limit, named once and left alone. Agents also stopped filing a ticket for every edge case. One night an agent filed seven issues for findings nobody needed. I closed them as not planned.

## Fewer, self-contained pull requests

Agents split work into many small pull requests, and each one costs a reviewer a context switch. "Why are there that many PRs? Can we consolidate into a single one or fewer?" Ten pull requests became four. On another project, ten review requests to colleagues became three.

Consolidation has a limit. When each merge deploys to production, separate pull requests can be right, and the agent said so with that reason. I accepted it. The rule is as few pull requests as the work allows, each one dense and self-contained for the person who reviews it.

## Subtract from the product, too

- In phi-router: "Nobody uses the pin command. Drop it."
- An undo feature for an automation was "a catastrophic design failure that leads to a lot of edge cases." We removed it.
- The target for phi-router is what HIPAA compliance needs: "anything more is just bloat, anything more has to be actively removed to simplify."

Subtraction needs evidence like any other change. On a different project I wanted to drop a pinning feature too, and the agent proposed measuring its use first. The numbers showed people used it. It stayed.

## Subtract from the harness

The same rule applies to the setup. I deleted every prompt template, and I cut guides that no session loads, as [chapter 09](09-fix-the-system.md) describes.
