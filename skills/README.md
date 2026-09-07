# Skills

A skill is a folder of instructions an AI assistant loads before it starts a job, so the job is done the same way every time. Instead of you remembering which field to ask for and which one lies, the assistant reads the folder first and follows it. One file, `SKILL.md`, holds the whole thing: a short description of when to use it, then the steps.

These four encode the traps that only showed up when the operations were actually run — a campaign built, read back through Meta and deleted; a live account queried; a public Ad Library audit paid for and completed. That is the difference between these and a generic prompt. They know that a rate comes back as `0.025567691511131932` and not `2.56`, that the geo targeting you asked for is not the geo targeting you get, and that the field called "conversions" returned three orders of magnitude more than the real one on the same row.

To use one: copy the folder into your assistant's skills directory (in Claude Code, `~/.claude/skills/`; other clients have their own), and it will load when the job matches the description. If your assistant has no skills directory, just paste the contents of the `SKILL.md` into your prompt before you ask your question — it works the same way, you are simply doing the loading by hand.

| Skill | Use it when |
|---|---|
| **[meta-launch-campaign](meta-launch-campaign/SKILL.md)** | Building a campaign, ad set and ad from scratch |
| **[meta-weekly-report](meta-weekly-report/SKILL.md)** | Pulling last week or last month by campaign |
| **[meta-conversion-audit](meta-conversion-audit/SKILL.md)** | Checking whether the conversions being reported are real |
| **[meta-competitor-teardown](meta-competitor-teardown/SKILL.md)** | Reading a brand's live ads from the public Ad Library |

All four run on the Meta Ads connector inside the Porter Metrics MCP: `https://mcp.portermetrics.com/mcp`.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
