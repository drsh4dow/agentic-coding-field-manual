# Agentic Coding Field Manual

A practical, opinionated manual for running a fleet of coding agents without shipping slop.

A swarm of agents can produce more work in a day than you can review. This manual is about where your attention goes instead. You own the destination and the judgment, and agents do the work. It is grounded in two weeks of my own sessions with [pi-harness](https://github.com/drsh4dow/pi-harness) and leans on the [No AI Slop manifesto](https://www.slopmanifesto.com/).

## Who this is for

Engineers who already ship with coding agents and now run more than one at a time. It assumes you already have opinions about linting, type systems, and test strategy.

## What's inside

| Chapter | Description |
| --- | --- |
| [Introduction](src/00-intro.md) | Why the old "you drive, AI types" model broke, and the one that replaced it. |
| [The harness](src/01-harness.md) | Principles, playbooks, skills, roles, the model table, and the gates the rest of the manual assumes. |
| [The repo agents work in](src/02-the-repo.md) | Glossary, standards, ADRs, AGENTS.md, strict tooling, fast checks, and tests that test something. |
| [Align before autonomy](src/03-align.md) | Openers, a measurable definition of done, and decisions as numbered calls with a pick. |
| [Delegate the work](src/04-delegate.md) | Slicing work across owners and leaves, grants, swarms, arenas, and steering a running fleet. |
| [Verify in proportion to the stakes](src/05-verify.md) | Proof on the real system, cross-vendor verdicts, root causes, and what proof costs. |
| [Subtract](src/06-subtract.md) | Net-negative diffs, cut passes, and why edge cases tend to infinity. |
| [Write for the reader](src/07-write.md) | The manifesto applied to every pull request, status update, action item, and message. |
| [Sessions end, work doesn't](src/08-memory.md) | State folders, pause and resume, handoffs, and what compaction drops. |
| [Fix the system, not the output](src/09-fix-the-system.md) | Turning a repeated correction into a check, a type, or a gate. |
| [Anti-patterns](src/10-anti-patterns.md) | The failures I corrected most, from agents and from myself. |
| [Appendix: the manifesto, clause by clause](src/appendix-manifesto.md) | Each manifesto resolution mapped to the practice that serves it. |

## Read online

[drsh4dow.github.io/agentic-coding-field-manual](https://drsh4dow.github.io/agentic-coding-field-manual/)

## Local development

### Prerequisites

- [Bun](https://bun.sh/)
- [mdBook](https://rust-lang.github.io/mdBook/)

### Install dependencies

```bash
bun install --frozen-lockfile
```

### Quality checks

```bash
bun run lint:md
```

### Build the book

```bash
mdbook build
```

The generated site is written to `book/`.

## Repository structure

- `src/` holds the Markdown source for all chapters and the appendix.
- `book.toml` is the mdBook configuration.
- `.github/workflows/` runs CI (markdown lint, build, link check) and the GitHub Pages deployment.

## Author

[Daniel Moretti](https://github.com/drsh4dow)

## License

MIT. See [LICENSE](LICENSE).
