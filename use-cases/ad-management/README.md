# Ad management — changing things, not reading them

> [!IMPORTANT]
> Everything in this section **writes to your ad account**. Ask for campaigns, ad sets and ads to be created paused, read back what was created, confirm the numbers with whoever owns the budget, and only then activate. Activating is a separate, deliberate instruction — never a side effect of building something.

Open this section when you want your assistant to build, edit, pause or restart something in the account instead of reporting on it.

| File | Use this when… |
|---|---|
| [launch-a-campaign.md](launch-a-campaign.md) | You want a campaign, ad set and ad built in one go, sitting paused and ready for review. |
| [edit-budgets-and-bids.md](edit-budgets-and-bids.md) | A budget needs raising or cutting, or you need to switch between a daily and a lifetime budget. |
| [pause-and-restart.md](pause-and-restart.md) | You need to stop or restart spend at the campaign, ad set or ad level. |
| [audiences-and-lookalikes.md](audiences-and-lookalikes.md) | You want a website or customer-list audience, or a lookalike built from one. |
| [upload-creative.md](upload-creative.md) | You have an image or video to get into the account, from a link or from your own machine. |

**Skill:** [skills/meta-launch-campaign/SKILL.md](skills/meta-launch-campaign/SKILL.md) — loads the six traps below automatically before your assistant builds anything.

## What has actually been run against a live ad account

You are about to let an assistant change a live account, so here is the honest split. On 2026-09-07 a full chain was built in a real ad account, read back through Meta, and deleted — everything below marked **run** comes from that. Everything marked **not run** is grounded in the connector's own field catalog and action list, which is a weaker thing.

| Job | Run against a live account? | What that means for you |
|---|---|---|
| Create a campaign | **Yes** | Created paused, read back from Meta, budget and bid strategy confirmed on the object |
| Create an ad set with targeting | **Yes** | Country, age range, Advantage+ Audience and platforms all round-tripped; the real parameter names are known |
| Upload an image from a public URL | **Yes** | The response shape is documented because it was seen |
| Create an ad | **Yes** | Confirmed which parameter names work and which are silently dropped |
| Delete, and the cascade | **Yes** | Deleting the campaign removed its ad set and ad; the follow-up list came back empty |
| Edit a budget on an existing object | **No** | Reading budgets was verified thoroughly; changing one was not |
| Pause or activate anything | **No** | The action that carries a status change is known; its response is not |
| Create a custom audience | **No** | The action and both seed types are real; no response has been seen |
| Create a lookalike | **No** | Known to require a location; nothing beyond that has been observed |
| Upload a video | **No** | Supported by the connector, never exercised here |
| Upload a file from your own machine (base64) | **No** | Supported by the connector, never exercised here |

Separately, the connector's **limits** — the bid strategy default, the Advantage+ Audience conflict, the single OR-group of interests, no post boosting, no asset deletion, no dayparting — were verified against the live connector rather than by running a write. They all trace to [what it cannot do](../../reference/what-it-cannot-do.md).

Treat the "no" rows as a reason to read every result back before you activate anything, rather than a reason to avoid the section.
