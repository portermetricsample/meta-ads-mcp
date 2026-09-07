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

## How much of this has been verified

Being straight about it, because you are about to let an assistant change a live account:

- **Verified against a live ad account:** how the budget fields behave when you read them — the `0.0` at the level that does not hold the budget, and what "remaining" actually counts. That is why [edit-budgets-and-bids.md](edit-budgets-and-bids.md) is blunt about checking the level first.
- **Verified against the live connector, but not by running the write:** what this connector can and cannot do — the bid strategy default, the Advantage+ Audience conflict, the single OR-group of interests, no post boosting, no asset deletion. Every one of those traces to [what it cannot do](../06-reference/what-it-cannot-do.md).
- **Not tested end to end:** the write operations themselves — creating, editing, pausing, uploading and audience building. The prompts and field names are grounded, the exact responses your account returns are not.

Treat that last group as a reason to read every result back before you activate anything, rather than a reason to avoid the section.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
