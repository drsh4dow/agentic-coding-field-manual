# Align before autonomy

> We do our own thinking when working with a model. We explore resources, code, and prior art to truly understand the problem before the work starts.
>
> [No AI Slop manifesto](https://www.slopmanifesto.com/), resolution 4

The most expensive mistake in a long agent run happens in the first ten minutes. The agent sets off toward the wrong destination and builds well for six hours. Alignment costs me a few minutes of answers, and it is the only part of the run I can't delegate.

## The rule

An agent does not run on its own until it has a clear destination, written as a definition of done (DoD). In my words: "the agent should not go autonomously until it has a clear DoD or idea of the destination."

The destination is the *what*, not the *how*. "Having a spec with a clear DoD is crucial, but deciding on the how beforehand not." I state the outcome as a [commander's intent](https://en.wikipedia.org/wiki/Mission-type_tactics), the goal a leader gives so the people doing the work can choose their own route. The agent picks the route, and it may change the route as it learns.

## Openers, not templates

I deleted every prompt template I had, because I prefer to talk to the model directly. The same phrases recur anyway, because they work:

- **"Sharpen the premise and propose a plan."** This is the most common opener in my sessions. The agent questions what I asked for, researches, and comes back with a plan and the calls it needs from me.
- **"Restate in your own words what the task is and what the definition of done is, so I can confirm or adjust."** The restatement is the cheapest review in the whole run.
- **"Don't implement, just propose."** Or "just answer." It stops an agent that starts building when I only asked a question.
- **"Grill me until this has a plan that fits on one page."** The `grilling` skill asks one round of questions at a time, each with its own recommendation.
- **"Run reframe to pick up the expert terms."** The `reframe` skill names what I'm building in the words the experts in that field use.
- **"Gather context and diagnose. Don't fix it yet. Explain what happened, the root cause, and how to fix it."** This is my bug opener.
- **"Continue the work described in this handoff. Start by restating the objective and the current state."** This is my resume opener.

## The definition of done is a number or an observable state

A good definition of done names a measurement or a state anyone can check. One of mine was "a person spends two and a half hours a week or less on this manual task, measured in production." Another was "every site the request named, not the two easiest."

Restating catches two failures that agents commit often:

- **Shrinking the scope.** On one project the agent wrote a definition of done that covered two sites when the request named five. It happened twice in the same project.
- **Swapping the outcome for a proxy.** An agent framed a session as "get the code into production" when the goal was the weekly hours target. Code in production is a step. The hours target is the outcome. An agent that aims at the step runs into [Goodhart's law](https://en.wikipedia.org/wiki/Goodhart%27s_law), where a measure that becomes the target stops measuring the goal.

## Decisions arrive as numbered calls with a pick

The agent ends its proposal with numbered questions. Each question carries the agent's own pick and the reason. I answer in one line per number: "1. agree. 2. no, B. 3. drop it." Many rounds end with "agree on all." The pick matters because I can approve it in two words. An open question takes me a paragraph.

Four rules keep the rounds short:

- **Ask in chat.** An agent that parks questions in a file makes me go find them. "Ask me the questions in chat to answer you quicker."
- **Ask only what is mine.** A fact the agent can look up, measure, or try is not a question for me. "Drop these questions and figure it out yourself." I answer product calls and preferences. The agent settles everything else by observation.
- **Speak clearly.** When I can't parse a question, I type `/skill:wait-what` and the agent explains it again in plainer words. If I have to do that, the question was slop.
- **Don't reopen a settled call.** Once I decide, the decision goes into `STATE.md` and stays decided.

## Grill, then write the spec

For a large or tangled project, alignment takes rounds. One redesign took three grilling rounds and 17 questions. A production automation took 25 questions over four rounds. Each new term went into the glossary only after the agent tested it against concrete cases, such as "does this case count as signed off?"

Grilling produces three things:

1. Settled terms in `GLOSSARY.md`.
2. A spec written with `/skill:to-spec` that holds the destination and the definition of done.
3. The first few tickets, and no more.

I tried filing all the tickets up front. One spec produced 32 tickets, each one checked by a cold reader, a fresh agent that reads only the ticket and reports what it can't follow. Those tickets decided the *how* before anyone had learned anything. I dropped ticket-first planning the next day. Now I use [rolling-wave planning](https://en.wikipedia.org/wiki/Rolling-wave_planning), which plans near work in detail and later work roughly. The implementer files the tickets for the next slice when it gets there.

## Prototype when you can't picture it

Sometimes I can't judge a plan because I can't see it. "I still can't visualize this in my head." Then the agent builds a throwaway prototype, such as an HTML page with two or three variants, and I pick one. For a hard user experience question I run an arena. Designer agents on models from different vendors each propose a design, a judge from another vendor ranks them, and the root combines the best parts. I settle the question by looking at something, not by debating it.

## When the agent pushes back

An agent that agrees with everything is no help. I want pushback, with evidence:

- I called some infrastructure rules hallucinations from an earlier agent. The agent showed with `git blame` that a colleague wrote them. I kept them.
- I wanted phi-router shipped as a single binary. The agent measured 82 MB and argued against it. I dropped the idea.

Pushback is not license to change the task. The agent can argue about the route, but the intent is mine. When I asked an agent to design phi-router's routing, it wrote me a compliance audit of the routing policy I had already decided. "I'm not asking you to audit this. You are deviating from the task."
