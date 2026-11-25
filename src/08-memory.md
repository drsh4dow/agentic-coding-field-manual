# Sessions end, work doesn't

The old manual said to never compact and to start a fresh session instead. That advice fit sessions of an hour. My runs now last days, and they survive reboots, harness upgrades, and many compactions. The work lives on disk, not in the context window.

## The state folder

Each piece of work keeps a folder at `~/.local/state/pi-agent/<project>/<work>/`:

| File | Holds |
| --- | --- |
| `STATE.md` | The destination, my standing instructions in my words, the decisions in force, the status, and the next step. |
| `facts.md` | Project facts every delegate needs, such as commands, conventions, and hazards. |
| `owner.md` | Rules only owners follow, such as how a slice ships. |
| `TODO.md` | The steps of each playbook the root runs, checked off or skipped with a reason. |
| `decisions.tsv` | The decision trail: one row per decision with its reason, evidence, and result. |
| `USER_ACTION_ITEMS.md` | What waits on me. |

`STATE.md` is capped at 16 KB, because the root reads it back whole after every compaction. Dated history goes to the decision trail. One project's `STATE.md` grew to 125 KB before the cap existed. The rewrite cut it to 11 KB.

## Standing instructions survive in my words

Instructions I gave once got lost in later sessions. "Use the auto-approver" and "use the model table" each disappeared after a handoff, and I had to repeat them. `STATE.md` now keeps my standing instructions as I said them, word for word, so a new session reads the same sentence I typed.

## Pause and resume

"Pause the work, I'm going to reboot" is a normal message. The root cancels its delegates, pushes unpushed branches, and writes a resume note. Background jobs such as watches and the auto-approver die with the machine, so the note lists which ones to start again. After the reboot, "continue" picks it up, and the root asks before it restarts the jobs.

## Handoff to a fresh session

When the harness changes, or a session has carried too much, I run `/skill:handoff`. The note lists the files to read in order, the questions to ask me first, and the mistakes to avoid. The new session opens with "Continue the work described in the handoff. Start by restating the objective and the current state."

The old session must stop. After one handoff, the old session kept posting its periodic status reports, and I had to ask where the handoff was.

## Compaction drops the rules

Compaction keeps the task and loses the guides. In two long sessions I had to say the same thing four times: "Again you have no principles or skills in your context, read them again." Each reload found real slips that had happened without the rules: merges on a verdict without reading the diff, numbers reported without an explanation, and searches skipped.

The root first answered with a note at the top of `STATE.md`. That didn't hold. Then it wrote a script that blocked merges until the rules were reloaded. Now the harness writes its own compaction summary, and the summary lists the guides that were in context so the agent reloads them. [Chapter 09](09-fix-the-system.md) covers why a fix in code beats a note.

## The decision trail

Every decision with a reason and evidence goes into `decisions.tsv`. I read it when I come back from hours away and want to know why the run went where it went. A reviewer from another vendor also audits it, as [chapter 05](05-verify.md) describes.
