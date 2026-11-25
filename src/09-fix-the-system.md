# Fix the system, not the output

> When a mistake shows up twice, we scale ourselves and our team by improving the system and its guardrails. Anything a linter, type checker, or automated check can catch, we let it catch.
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), resolution 12

Correcting an agent fixes one output, and the next session makes the same mistake. The manifesto puts "improving the system over patching the output" among its five values. I run dozens of sessions a week, so a correction in chat reaches one of them while a fix in the harness reaches all of them.

## Twice means structure

When I catch myself giving the same correction a second time, it stops being a correction and becomes a change to the harness. The fix goes as deep as it can, in this order:

1. Change the architecture so the mistake can't happen.
2. Change a type so the mistake doesn't compile.
3. Add a lint rule or a check that fails on it.
4. Add a test.
5. Only then, write a rule in prose.

Steps 1 and 2 make the mistake impossible, so no agent has to remember to avoid it. The `correct` skill runs this order. Prose comes last because agents forget prose after a compaction.

## Two weeks of fixes

The `wait` tool shows why the order matters. Agents waited for their jobs with `sleep`. One night I sent an agent a screenshot of my process list and asked "what are all those processes running?" They were twelve `sleep` alarms it had set for itself. The first fix was a pull request that added a check to refuse `sleep` calls. I worried that agents would then burn CPU in a loop to fake a sleep, so the agent rebuilt the pull request around a new tool instead. The new `wait` tool blocks until results arrive and returns them in its reply, and with nothing left to sleep for, no agent has to remember the rule.

Three more from the same two weeks:

| Repeated mistake | Fix |
| --- | --- |
| Agents wrote action items in any format they liked | A format check rejects a write that breaks the item format |
| Agents merged without an independent review | A `gh` wrapper refuses a merge without a verdict on the latest commit |
| Agents said a skill didn't exist when it was hidden from the list | `/skill:<name>` finds any skill on disk |

## Retros

After a run that went wrong, I run `/skill:retro`, a [blameless postmortem](https://sre.google/sre-book/postmortem-culture/) that asks what let the mistake through, not who made it. The agent reads the transcript and finds where each mistake came from. I bring hypotheses for it to test, and I say why I ask: "I'm not judging, I'm trying to understand where it comes from so we can avoid it in new sessions."

Each retro ends in pull requests to the harness, not in a list of lessons. My runs used to end unpredictably. "Sometimes it opens a PR, other times it opens 6 PRs, other times it doesn't open and left the work on a worktree." I ran a retro on the harness itself, and half an hour later the harness changed so that every run ends in one handoff pull request, which the agent opens without asking me. A lesson nobody encodes is gone by the next compaction.

## Prompts are code

System prompt changes go through the same process as code: a pull request, a short eval on the behavior the change targets, and a review. When I port a guide from upstream, I keep the wording, because the exact words shape what the agent does. I tune only the trigger and the description.

## Measure what loads

A guide that never loads still costs a line in every prompt. The harness records which guides each agent loads, and an audit compares that record to the full list. Guides that nothing loads get cut. Guides that should load and don't get a better trigger.
