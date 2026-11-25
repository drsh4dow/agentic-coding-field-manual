# Verify in proportion to the stakes

> Agent reviews, linters, and verifiers are useful but not sufficient. For now, we still review at least some subset of the outputs. What subset depends on the stakes.
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), resolution 9

A common rule is to read every diff before you commit. I kept it when I ran one agent. At fleet scale I can't, and pretending I do would be its own kind of slop. My rule now has two halves. A change works only when a run on the real system shows it. The amount of proof matches what a mistake would cost.

## Proof means a run on the real system

"It compiles" and "tests pass" are claims. These runs count as proof:

- **Use it like a user.** Agents dogfood the change in staging, then in production once it ships. A walkthrough includes the actions a user takes, such as uploading a file or adding a document, not only reading screens.
- **Look at the output.** For an email feature, the agent renders the email, screenshots it in real mail clients, and checks it reads like one person writing to another.
- **Watch after deploy.** After a production release the agent reads logs and production data. It keeps a switch ready to turn the feature off if errors appear.
- **Drive it with the project's verification skill.** See [chapter 02](02-the-repo.md).

## A verdict from another vendor, on the exact commit

Every pull request gets a verifier from a different model family than the one that wrote it. The verifier records its verdict against the exact head commit. A merge wrapper refuses to merge without that verdict. A new push needs a new verdict, unless it is a rebase that left the patch unchanged.

A cross-vendor review also runs over the decision trail. In one run it caught the root claiming a fix that had not landed, and the root reopened the ticket.

## Root cause or nothing

When I review a fix, mine or a colleague's, my first question is whether it fixes the cause or patches a symptom. "My main question here is if we are handling the root cause or patching here."

Agents state causes with more confidence than they have. One blamed a failure on memory and wrote a change to raise the heap. I asked: "Are you 1000% sure this is due to an OOM? And not something else?" The agent admitted about 75% confidence. It measured before it opened the pull request.

Numbers get the same treatment. Before an agent reports a number, it explains what produced it.

## What I review myself

> There will always be alpha in reviewing **something**. As models improve, we may stop reading most of the code. We may still review a plan, design, or result, because if we don't, we just get the same output as everyone else.
>
> resolution 8

I read these myself:

1. The restatement and the definition of done.
2. The calls the agent brings me, with its picks.
3. Prototypes and designs.
4. Every message that goes to another person.
5. Pull request bodies.
6. The code, when the stakes call for it. Harness changes alter the agent setup I run on, so I read that code. On one such change I told an agent to skip the cold reader that checks the pull request body. "Just open the PR, I'm more interested in the code."

For a long run on a product, I read the plan, the result in production, and the diffs that a verifier or I flagged. I don't read every line.

## Proof has a cost

Agents over-verify as readily as they under-verify. These corrections come from two weeks:

- "Stop running all gates again on every small change."
- "Evals should be short and precise and not be run like crazy. They are the final gate, not a check to run every single action."
- "Only verify the things we are improving. I don't care about formal proof of everything. Don't hog my CPU."
- "Just answer, I don't want you to run a benchmark."
- One pull request went through six verifier rounds. Another project averaged three to five review rounds per pull request.

Those corrections produced the check rules in [chapter 02](02-the-repo.md), plus two more. Adversarial review runs only after a second failed review. Verification covers what the change touches, and no more.

Both directions are true at once. In the same week I said "without skipping verification, of course" and "skip verification, I will test drive it myself." The difference is who does the proof. I cut repeated checks and extra review rounds, but never the proof that the change works. When I skip the agent's verification, I take it on myself.

## Reviewing other people's pull requests

When a colleague asks me for a review, the agent does the legwork and I make the call:

1. I ask for a binary verdict and name my worry: "Check if we need changes or approve. I'm concerned about hardcoding a value there."
2. The agent runs the change on staging with the project's verification skill, and it runs interrogate when the change is risky.
3. It brings back the verdict in plain words: "should we request changes or approve? Be clear."
4. It drafts the review comment. I post it, or I tell it to.

I check the agent's claims before they reach a colleague. One review claimed that merging to the main branch deployed the app. It didn't. "From where did you come to that conclusion?" The agent fixed the stale doc that had misled it.

The manifesto has a line for the other direction too:

> When someone sends us slop, we tell them, kindly, and ask them to review it first.
>
> resolution 7
