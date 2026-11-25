# Appendix: the manifesto, clause by clause

The [No AI Slop manifesto](https://www.slopmanifesto.com/) was written by the speakers and attendees of AIE Code Summit 2026. This table maps each of its resolutions to the practice in this manual that serves it.

| Resolution | Practice | Chapter |
| --- | --- | --- |
| 1. Human time and attention is incredibly valuable, so we optimize for using it wisely. | Numbered calls with a pick, one-minute pull request bodies, action items only for calls that are mine | [03](03-align.md), [07](07-write.md) |
| 2. We fight slop because AI should make our work better, not just easier. | Cut passes, net-negative diffs, `/skill:unslop` | [06](06-subtract.md), [07](07-write.md) |
| 3. We optimize systems, tools, and products for efficient elicitation of human intent and for efficient human understanding. | Restate, sharpen the premise, grill, prototype | [03](03-align.md) |
| 4. We do our own thinking when working with a model. | I set the destination and correct the premise before any agent runs alone | [03](03-align.md) |
| 5. We own the intent, taste, and consequences of what we ship, however much AI helps us make it. | Grants are explicit, and the human keeps the controls | [04](04-delegate.md), [10](10-anti-patterns.md) |
| 6. When an agent wrote something we're sending, we make that clear, and we check the parts that matter before it goes out. | Every message to a person passes through my read. I don't yet disclose agent drafts in chat messages | [07](07-write.md) |
| 7. When someone sends us slop, we tell them, kindly, and ask them to review it first. | Reviews of colleagues' pull requests | [05](05-verify.md) |
| 8. There will always be alpha in reviewing something. | I review the plan, the design, the result, and the code when stakes call for it | [05](05-verify.md) |
| 9. Agent reviews, linters, and verifiers are useful but not sufficient. | Cross-vendor verdicts plus my own review, scaled to the stakes | [05](05-verify.md) |
| 10. What shipped, who's using it, and how it's helping them matters FAR MORE than lines of code, prs merged, tokens spent, or the number of agents running in parallel. | Done means a measured outcome | [03](03-align.md), [04](04-delegate.md) |
| 11. Unreviewed output isn't always necessarily bad. | Prototypes skip code review and verification because they get thrown away. I still look at each one and pick | [03](03-align.md) |
| 12. When a mistake shows up twice, we scale ourselves and our team by improving the system and its guardrails. | Twice means structure, retros, gates in code | [09](09-fix-the-system.md) |

The manifesto ends with this:

> None of us has this figured out. We're each relearning what we will and won't accept, and there's no single right answer.

Neither have I. This manual describes two weeks of practice in late 2026. Some of it will be wrong by the next rewrite.
