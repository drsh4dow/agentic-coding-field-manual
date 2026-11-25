# The harness at work

My setup is [pi-harness](https://github.com/drsh4dow/pi-harness). It is an open source config folder for the [pi](https://github.com/earendil-works/pi) coding agent, plus panels for the [Herdr](https://herdr.dev/) terminal app. You don't need it to use this manual. This chapter follows one real project through it, start to finish. [The harness appendix](appendix-harness.md) lists every part for reference.

## The project

[phi-router](https://github.com/drsh4dow/phi-router) is my open source router for the coding agents pi, Claude Code, and Codex. It sends each model request to one of two accounts. A request that holds patient data goes to a HIPAA-compliant account. Everything else goes to an ordinary account. Later chapters come back to it.

An earlier planning session had already written the spec as GitHub issue #1, with 32 sub-issues as tickets. Filing every ticket up front is an approach I dropped the next day, and [chapter 03](03-align.md) explains why. The run below still started from those tickets.

## Restate before anything runs

The agent in my terminal is the root. It talks to me, plans, hands out the work, and reports back. I told it to build issue #1 and all its sub-issues, and to bring me the tickets that needed my input. Then I asked for one thing before any work: "gather the necessary context and restate in your own words what are we doing here."

The root read the spec, the 32 tickets, the glossary, and the state folder that the planning session left behind. A state folder is a directory at `~/.local/state/pi-agent/<project>/<work>/`. It holds the destination, my standing instructions, and the decision trail, so the work outlives any one session.

The restatement exposed a wrong belief. The agent asked me for an API key to the compliant Anthropic account. I don't have one, because that account signs in through a browser login. The spec carried the same mistake, so I had it fixed first: "update the spec and the respective tickets so we are aligned on the truth." Then I asked for a fresh restatement. It matched what I wanted, and I gave the grant in one line: "Excellent, proceed with implementation, operate autonomously."

Until that line, the agent proposes and asks. After it, the agent works alone inside what the restatement covered. Restating has its own skill in my harness, `in-your-own-words`, a guide the agent loads when the task matches.

## One owner per ticket

The root doesn't write the code. It starts delegates, other agents that each get one task and report back to it. Each ticket went to an owner, a delegate that built the ticket, tested it, and committed it. Each owner worked in its own git worktree, a separate checkout of the repo, so no two owners edited the same files.

Smaller jobs went to leaves, delegates that do one bounded task and start nothing. Before the root filed a new ticket, a leaf acted as a cold reader, an agent that sees only the ticket and none of the run. It reported what it couldn't follow.

## A verifier from another vendor

Each pull request got a verifier, a leaf that reviewed it. The verifiers ran on GPT, and the owners ran on Claude. A checker from the writer's family risks a [common-mode failure](https://www.adelard.com/media/vfngprxq/divchap.pdf), where one shared cause makes the writer and the checker miss the same bug. A reviewer from another vendor removes that shared cause.

The verifier checks the pull request at its exact head commit. A wrapper around `gh`, the GitHub command line tool, refuses to merge unless a verifier passed that commit. When a pull request failed review twice, the root sent four adversaries, agents on different models whose only job was to break the change. The root merged only after a review passed. Partway through I made merging a standing instruction: "you merge the open PRs that are ready." The root recorded it in `STATE.md`, the state folder's main file.

In Toyota's terms the wrapper is [jidoka](https://global.toyota/en/company/vision-and-philosophy/production-system/). Under jidoka a machine stops itself on a defect, so one person can run many machines without watching each one. Gates like this let me run a fleet without reading every diff.

## Decisions by number

The root batched its questions, and each question carried its own pick. At first it parked them in `USER_ACTION_ITEMS.md`, a file of items that wait on me. I pulled them back: "ask me the questions in chat to answer you quicker."

I answer by number. "1. yes. 2. yes. 3. agree." When a question made no sense, I said so: "I don't understand this, speak clearly." The agent explained it again with a worked example. A little over two days after the grant, I answered a batch with "agree on all 7, make the repo public and release it."

## Using it myself

The verifiers checked correctness. After the release I installed phi-router and used it, and I found problems with the experience.

- The installer was a wall of text. "The experience is awful."
- Setup demanded two accounts up front. A second subscription helps, but it is not the default path.
- Setup cloned the repo into my home folder. "That is disgusting."
- The README stopped letting me copy its prompt block.
- Setup accepted only an Anthropic key, when any compliant account should work. "That is a regression."

Each problem went back through the loop this chapter describes. For the installer I asked for an arena, where four designers on models from different vendors each proposed a design and a judge ranked them. I added "Propose the changes. Don't implement yet." For setup I asked: "Restate in your own words what would be a better UX." The setup redesign that followed had its own spec, a prototype I opened in my browser, an owner per phase, and a verifier at each pull request.

My part of the run was the restatement, the grant, the numbered answers, three pauses to reboot my machine, and using the product. At each pause the root saved the run to its state folder and picked it up after the reboot, as [chapter 08](08-memory.md#pause-and-resume) describes. The agents did the rest.
