# Use cases

Four jobs, four folders. Pick the one you have today — each page inside is one job: the prompt to paste, the shape of what comes back, how to read it, and the one thing that quietly makes the answer wrong.

| Use case | What it is for |
|---|---|
| **[Ad management](ad-management/)** | Changing things instead of reading them — launch a campaign, move budgets and bids, pause and restart, build audiences and lookalikes, upload creative. Writes go to your account, created paused. |
| **[Reporting](reporting/)** | The work that runs on a schedule — last week's numbers by campaign, budget pacing, creative fatigue, alerts, and one question that spans Meta, Google and TikTok at once. |
| **[Creative research](creative-research/)** | Reading ads you do not own. Any brand's live Meta ads by name, from the public Ad Library — no login, no partner access, nothing for them to approve. |
| **[Audits](audits/)** | Something is wrong, or an account you did not build just landed on your desk — where the money goes, what is working, who converts, whether the pixel is really firing, why delivery stopped. |

Each folder carries its own `skills/` subfolder — ready-made instructions your assistant loads before it starts on that job, so the traps documented on these pages are avoided by default rather than remembered.

## How to use a skill

A skill is a folder of instructions your assistant loads before it starts a job, so the job is done the same way every time — a short description of when to use it, then the steps, in one `SKILL.md` file. Copy the folder into your assistant's skills directory (in Claude Code, `~/.claude/skills/`; other clients have their own) and it loads automatically when the job matches the description. If your assistant has no skills directory, paste the contents of `SKILL.md` into your prompt before you ask your question instead — same effect, you're doing the loading by hand.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
