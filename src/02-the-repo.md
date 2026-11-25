# The repo agents work in

An agent reads the repo before it reads your prompt. Whatever it finds there, it copies. Set the repo up so the thing it copies is what you want.

## Three shared documents

Every repo I work in has three documents that agents must read before they name anything or write code:

- `GLOSSARY.md` says what words mean. When an agent misreads a term, I add the term: "add it to the glossary so agents understand what it is." Agents use glossary terms in code, tickets, and replies, so one concept keeps one name everywhere.
- `CODING_STANDARDS.md` holds the mechanical rules that code must follow.
- `docs/adr/` records why the code is the way it is. An ADR earns its place with a real decision. I stopped an agent that planned one ADR per module: "ADRs should not be created mechanically nor per modules."

## AGENTS.md

`AGENTS.md` is still the repo's system prompt. Three rules from the old manual hold. Write it by hand. Keep it short. Add a rule only when an agent makes the same mistake twice.

Two rules are new:

- **Dense words.** Cut every no-op line, such as "write clean code," that changes no behavior. [Chapter 07](07-write.md) covers writing for agents.
- **Progressive disclosure.** `AGENTS.md` holds what applies everywhere and points to the document that holds the rest. It never points at a spec or a ticket, because those change and `AGENTS.md` doesn't.

When a repo's `AGENTS.md` has grown into a mess, I run the `writing-for-agents` skill over it and ask for three passes, each from a separate agent and each more radical than the last.

## Guardrails at maximum strictness

This part of the old manual still holds. Set the linter and the type checker to their strictest settings, then loosen a rule only on purpose and only where it must be loose. An agent can't merge what the linter rejects.

Two additions:

- **Lint rules aimed at agent habits.** My harness repo runs oxlint with the [anti-slop rules](https://github.com/dmmulroy/anti-slop). Two examples are `no-module-mocking`, which enforces the no-mocks rule below, and `no-chained-type-assertions`, which stops an agent from casting its way past the type checker.
- **No code comments.** An agent narrates its code in comments, and the next agent changes the code without changing the comment. The `no-comments` skill moves each comment to a better home: a name, a type, a test, an ADR, or a commit message. Documentation comments on a public API are fine. Comments that narrate code are not.

## One check command, and make it fast

Wrap linting, formatting, and type checking in one command that agents run before every push. That rule is unchanged.

What changed is the cost of a slow check. With six owners, a ten-minute check runs six times, on one machine. I asked the same question in three repos within two weeks: "how long does the check take? What can we do to cut that number down to the minimum?" The answers were the same each time:

- Run the full check once per pushed head, not after every edit.
- Run independent checks in parallel.
- Move slow proofs, such as formal models and evals, out of the routine check. They run as a final gate on the change they cover.
- Share check results across agents, so two agents never check the same commit twice.

## Tests that test something

The no-mocks stance from the old manual still holds. Test real behavior against real dependencies. If you can't test something without a mock, the boundary sits in the wrong place.

Agents added two habits since:

- **Write the failing test first.** For a bug, the regression test fails before the fix and passes after it. That failing run is the proof that the test catches the bug.
- **Watch the test volume.** One agent PR had four lines of test for every line of new code, with the same schema copied into 31 test files. I called it slop, and the agent agreed after counting. A test earns its place by catching a regression that nothing else would catch.

## A verification skill per project

Each project I work on gets a `verify-<project>` skill that drives the app the way a user does. It signs in, clicks through a flow, and reads the result. The `create-verification-skill` skill writes the first version. Once a project has one, every agent can prove a change works on the real app, and so can I. I built one for an internal tool to review a colleague's pull request on staging, and agents reused it a few days later to check production.
