# Pause and restart campaigns, ad sets and ads

It is 6pm on Friday, the promo is over, and everything for that offer has to stop spending tonight.

> [!IMPORTANT]
> **This page has not been run end to end.** Nobody on this repo has pushed a status change through to a live ad account and read the result back. Everything below is grounded in the connector's own field catalog and action list — the field names, the action that carries a status change, and the scheduling limit are all real and checked. **What your account returns when it pauses something is not documented here, because it has not been seen.** Read every status back yourself and confirm from spend, not from the response.

## Ask this

```
In my Meta ad account, list every campaign, ad set and ad whose name
contains "<promo name>", with its configured status and its delivery status.
Then pause all of them, starting at the campaign level,
and show me the status of each one after the change.
```

Pausing is not its own action. `facebook_ads.campaign_update` is documented as changing name, status, budget and bid strategy. `facebook_ads.adset_update` and `facebook_ads.ad_update` exist, but the catalog does not spell out what they accept, and none of the three was run while writing this page.

## What comes back

Expect one row per object, at whichever levels you asked for, carrying its status. **The table below is a layout, not a result** — every value in it is a placeholder, and no run has confirmed the column set your account will return.

| Level | Name | Id | Before | After |
|---|---|---|---|---|
| campaign | `<promo campaign>` | `<campaign id>` | ACTIVE | PAUSED |
| ad set | `<promo ad set A>` | `<ad set id>` | ACTIVE | PAUSED |
| ad set | `<promo ad set B>` | `<ad set id>` | PAUSED | PAUSED |
| ad | `<promo ad 1>` | `<ad id>` | ACTIVE | PAUSED |
| ad | `<promo ad 2>` | `<ad id>` | ACTIVE | PAUSED |

## How to read it

Ask for all three levels in one answer. Each level carries its own status field, and reading one of them alone does not tell you what the other two are doing.

Pause the ad level instead of the campaign when only one creative is the problem and the rest of the ad set should keep running.

To restart, say the same sentence with "activate" in place of "pause", and be explicit about the level you mean. Each object holds its own status, so bringing a campaign back does not decide anything for an ad set that was paused separately.

Use the "before" column as your record of what to restore. Take that list **before** you pause anything, not after.

The listing actions — `facebook_ads.campaign_list`, `adset_list`, `ad_list` — can filter on `effective_status`, which is the faster way to ask "what is actually live right now" than pulling everything and reading it.

## The traps

> [!WARNING]
> **Four separate status fields exist and this page does not claim to know how they differ.** The catalog carries `facebook_ads_campaign_configured_status` alongside `facebook_ads_status`, `facebook_ads_adset_status` and `facebook_ads_ad_status`. Which one governs delivery was not tested — ask for all of them and compare rather than trusting one.

> [!WARNING]
> **Do not reach for delete when you mean pause.** Deleting a campaign takes its ad sets and ads with it — that cascade was confirmed on a live account, and afterwards the list came back empty. Pausing is reversible; deleting is not.

> [!NOTE]
> **You cannot schedule the stop.** Dayparting and ad scheduling are not parameters on this connector: ads deliver continuously between their start and end time, so a promo that must end tonight ends when someone actually pauses it. Set an end time when you build the ad set, or put the pause in someone's calendar.

## Go deeper

- Show me every campaign, ad set and ad in this account with the status of all three levels side by side.
- Restart only the ad sets I paused on `<date>`, and leave the rest alone.
- Pause every ad in this ad set except `<ad name>`.
- List the ads under `<campaign name>` with their status and their spend over the last 7 days.
- Show me which campaigns have spent nothing in the last seven days.

## Fields this uses

- [`facebook_ads_status`](../../reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../../reference/all-fields.md)
- [`facebook_ads_adset_status`](../../reference/all-fields.md) · [`facebook_ads_ad_status`](../../reference/all-fields.md)
- [`facebook_ads_campaign_name`](../../reference/all-fields.md) · [`facebook_ads_adset_name`](../../reference/all-fields.md) · [`facebook_ads_ad_name`](../../reference/all-fields.md)
- [`facebook_ads_spend`](../../reference/all-fields.md) — period spend, the honest check on whether something actually stopped

Budget fields look like a shortcut for "what is still running" and are not one — see [change budgets and bids](edit-budgets-and-bids.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
