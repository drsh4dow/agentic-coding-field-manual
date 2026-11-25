# Appendix: the harness, for reference

[pi-harness](https://github.com/drsh4dow/pi-harness) is a config folder for the [pi](https://github.com/earendil-works/pi) coding agent, plus panels for the [Herdr](https://herdr.dev/) terminal app. [Chapter 01](01-harness.md) shows it at work on one run.

The old manual asked for a tool with plan mode, LSP access, and conversation forking. Those still help. Running a fleet needs more:

- Agents that start other agents and wait on them, without me relaying messages.
- Instructions that load when they apply, so the prompt stays small.
- State that outlives a session.
- Gates that hold when an agent would rather skip them.
- A live view of what every agent is doing.

## Roles

- The **root** is the agent in my terminal. It talks to me, plans, delegates, integrates the results, and reports. It never pushes to a shared branch.
- An **owner** builds, verifies, and commits one slice of the work in its own git worktree. It can start helpers of its own.
- A **leaf** does one bounded task, such as a search, a review, or a measurement. It starts nothing.

## Guides

The harness has three kinds of guides. Each guide has a trigger that says when it applies. The prompt lists every guide by name and trigger, and the agent reads a guide in full only when its trigger matches.

- **Principles** are hard rules for how an agent thinks and decides. There are 27, such as `fix-root-causes`, `prove-it-works`, `subtract-before-you-add`, and `explain-the-number`. A principle outranks a skill and the agent's own habits.
- **Playbooks** are workflows, one per kind of work. There are 31, such as `bug-fix`, `feature`, `investigation`, `align`, `babysit`, and `autonomous-run`. The agent copies each playbook's steps into a `TODO.md` and checks them off, so I can see which step it skipped and why.
- **Skills** are tools for one job. There are 55. `grilling` interviews me until a plan settles. `arena` races several candidates at one task. `interrogate` sends adversaries on several models to break a change. `unslop` strips AI tells from prose. Some skills run only when I type them, such as `/skill:handoff` and `/skill:retro`.

## The model table

A delegate picks its model by alias, never by name. Every model runs at high reasoning effort.

| Alias | Model | Used for |
| --- | --- | --- |
| `judgment` | Claude Opus 5.5 | Implementation, design, and prose |
| `worker` | Claude Opus 5.5 | Research, scouting, verification runs, and the workers in a swarm |
| `investigator` | GPT 6.1 | Review and audit from another vendor |
| `fable` | Claude Fable 5.2 | One of the adversaries in `interrogate` |
| `divergent` | GLM 5.3 Flash | The extra runner in an arena, and nothing else |

The model that checks a pull request never comes from the family that wrote it. [Chapter 01](01-harness.md) explains why, and [chapter 04](04-delegate.md) explains why every delegate must name its model.

## Owned work

The root starts work with tools that return a handle at once:

- `delegate` starts an agent on one task.
- `serve` starts a long-running process, such as a dev server or my 1Password auto-approver.
- `watch` starts a command that wakes the agent when it exits, such as a CI poll or a timer.
- `wait` blocks until results arrive and returns them in its reply.

Each job gets its own Herdr terminal, nested under the agent that started it. Jobs run in systemd user slices, so cancelling a parent stops its children too.

## State folders

Work that outlives a turn keeps a folder at `~/.local/state/pi-agent/<project>/<work>/`. [Chapter 08](08-memory.md) lists its files.

## Gates in code

Some rules live in code, because agents skipped the prose version:

- A `gh` wrapper refuses to merge a pull request unless a verifier passed its exact head commit.
- A format check rejects a write to `USER_ACTION_ITEMS.md` that breaks the item format.
- `STATE.md` is capped at 16 KB, because the agent reads it back whole after every compaction.
- A machine-wide queue limits how many check runs go at once, and a recorded pass for a commit lets the next agent skip the rerun.

## Panels

Herdr shows the fleet in these panels:

- The Agents list nests every helper under its parent.
- The Skills panel shows which guides each agent loaded, in order.
- The Trace panel shows each playbook step and each decision with its evidence.
- The Actions panel shows what waits on me.
- The status bar shows what the session has spent.

## Prompt size

The old manual warned that every MCP server and skill bloats the prompt. That is still true, but the answer changed. Guides load by trigger, so 55 skills cost one line each until one applies. I also measure which guides load and cut the ones that never do, as [chapter 09](09-fix-the-system.md) describes.

## Credits

Most of this started as other people's work. The playbooks, the three roles, and the pull request format follow Lauren Tan's [pstack](https://github.com/cursor/plugins/tree/main/pstack). Several alignment skills, such as `grilling`, `to-spec`, and `to-tickets`, started as [Matt Pocock's skills](https://github.com/mattpocock/skills). Fifteen playbooks started as [Addy Osmani's agent skills](https://github.com/addyosmani/agent-skills). When I port a guide, I keep the upstream wording where I can, because the exact words shape what the agent does.
