# Write for the reader

> Slop is when we put less effort into producing something than we ask the consumer to spend understanding it.
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), belief 2

Many of my corrections in two weeks were about writing, not code. Agents write status updates, pull request bodies, action items, tickets, messages to colleagues, and notes for other agents. Each of these is cheap for the agent and costs the reader. That asymmetry is the whole problem.

## Two readers, two rules

**Humans** get short, plain, self-contained text. A human reader has none of the agent's context and little time.

**Agents** get dense text, in `AGENTS.md`, prompts, and briefs alike. "Words should be dense, carrying as much meaning as possible." An agent reads every word, and a dead word in a prompt costs on every run. I treat the system prompt as code, not prose: "the system prompt is the agent infrastructure, so I consider it the most critical piece of code."

## What I correct most

**Assumed context.** This is the most common failure by far. An agent spends hours inside a task and starts writing as if I had been there. "Nobody but you understands what step 1 is. Talk with context and make this self-contained." "Stop talking like I have the same context as you." The agent invents terms, such as "wave 1," "base defect," or "signs the case off," and uses them as if they were common words. The fix is plain words or a glossary entry, never a private term.

**Length.** On one Slack draft I asked for a shorter version three times in a row. The third time I added "humans don't talk like that."

**Machine rhythm.** "The first paragraph and the second one feel too symmetric, not like something a human would write." Balanced paragraphs, lists of three, and a summary line at the end mark the text as generated.

**Overcorrection.** A one-pager for leadership first assumed too much context. When I asked for more, the next draft explained what the readers already knew, and I had to ask it to get to the point.

## Tools

- `/skill:unslop` rewrites text against a catalog of AI tells. The catalog bans long dashes, colons used to join clauses, AI vocabulary such as "delve" and "crucial," and any sentence that could appear unchanged in another project's docs.
- `/skill:bro` restates a reply in plain, casual words. For a message that goes out under my name, the agent first reads my real messages and matches my voice.
- `/skill:wait-what` explains a reply again in a different way when I can't parse it.
- The `technical-writing` skill covers docs. It keeps a tutorial, a how-to guide, a reference, and an explanation on separate pages, and one idea in each sentence.

## Pull requests are one-minute briefings

A pull request body has six headings: Why, What changed, Scope, Tradeoffs, Blast Radius, and Verification. It stays under 40 lines. It links logs instead of pasting them. It describes the change as it stands, not the story of how agents produced it. "The PR should be a short read brief." The code is the content. The body tells a reviewer where to look and why to trust it.

## Status updates

A status update to a project's stakeholders follows four rules I learned the hard way:

- State facts, without names or dependencies on named people.
- Measure pace from what shipped, not from projected dates.
- Include only what readers need. "They don't want to read, so make it so it only contains the essentials and the others can be discovered."
- Make it readable without the project's history.

## Action items

When an agent needs me, it writes an action item. Each item is one call, and it says what the call is, the agent's pick, what the pick changes, the evidence, the risk, and why only I can make it. "Don't keep adding action items for the sake of adding them." An agent that sends me 25 items has not done its job. In one case most of the 25 were bullets inside drafted messages that the Actions panel in Herdr counted as items, so the format check now prevents that.

## Messages to people

Agents draft messages to colleagues in my voice, into a text file. I read each one, edit it, and send it myself. Two rules came from mistakes:

- Search the conversation history before drafting. One draft referred to three pull requests the recipient had never heard of, because it leaked our internal state.
- Every reference carries a link. A name or a number alone sends the reader searching.

The manifesto asks two things of a message an agent wrote:

> When an agent wrote something we're sending, we make that clear, and we check the parts that matter before it goes out.
>
> resolution 6

Nothing leaves without my read, so I meet the second half. I don't yet say when an agent drafted a chat message, so I miss the first half.

## Slop compounds

> The more slop sits in our knowledge base, in chat, in code, the more of it the next agent reads and copies.
>
> belief 8

Agents read what agents wrote, such as `STATE.md`, the glossary, tickets, handoff notes, and old pull requests. A vague ticket today becomes a vague plan next week, so careful writing for agents improves the next run.
