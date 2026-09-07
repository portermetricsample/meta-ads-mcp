# Pause and restart campaigns, ad sets and ads

It is 6pm on Friday, the promo is over, and everything for that offer has to stop spending tonight.

## Ask this

```
In my Meta ad account, list every campaign, ad set and ad whose name
contains "<promo name>", with its configured status and its delivery status.
Then pause all of them, starting at the campaign level,
and show me the status of each one after the change.
```

## What comes back

One row per object, at all three levels, with the status before and after. Names and ids below are placeholders.

| Level | Name | Id | Before | After |
|---|---|---|---|---|
| campaign | `<promo campaign>` | 120250000000000011 | ACTIVE | PAUSED |
| ad set | `<promo ad set A>` | 120250000000000012 | ACTIVE | PAUSED |
| ad set | `<promo ad set B>` | 120250000000000013 | PAUSED | PAUSED |
| ad | `<promo ad 1>` | 120250000000000014 | ACTIVE | PAUSED |
| ad | `<promo ad 2>` | 120250000000000015 | ACTIVE | PAUSED |

## How to read it

Ask for all three levels in one answer. Each level carries its own status field, and reading one of them alone does not tell you what the other two are doing.

Pause the ad level instead of the campaign when only one creative is the problem and the rest of the ad set should keep running.

To restart, say the same sentence with "activate" in place of "pause", and be explicit about the level you mean. Each object keeps its own status, so bringing a campaign back does not decide anything for an ad set that was paused separately.

Use the "before" column as your record of what to restore. Take that list before you pause anything, not after.

## The trap

> [!WARNING]
> **The status you set and the status that decides delivery are two different columns.** The catalog carries `facebook_ads_campaign_configured_status` — what someone set on the object — separately from `facebook_ads_status`, `facebook_ads_adset_status` and `facebook_ads_ad_status`. An ad can carry ACTIVE as its own configured status while nothing above it is running. Ask for all three levels together, as in the table above, and treat "it says ACTIVE" as an answer about one object only — never as proof that it is spending.

> [!NOTE]
> You cannot schedule the stop. Dayparting and ad scheduling are not parameters on this connector: ads deliver continuously between their start and end time, so a promo that must end tonight ends when someone actually pauses it. Set an end time when you build the ad set, or put the pause in someone's calendar.

## Go deeper

- Show me every campaign, ad set and ad in this account with the status of all three levels side by side.
- Restart only the ad sets I paused on `<date>`, and leave the rest alone.
- Pause every ad in this ad set except `<ad name>`.
- List the ads under `<campaign name>` with their status and their spend over the last 7 days.
- Show me which campaigns have spent nothing in the last seven days.

## Fields this uses

- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_adset_status`](../06-reference/all-fields.md) · [`facebook_ads_ad_status`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_name`](../06-reference/all-fields.md) · [`facebook_ads_adset_name`](../06-reference/all-fields.md) · [`facebook_ads_ad_name`](../06-reference/all-fields.md)
- [`facebook_ads_spend`](../06-reference/all-fields.md) — period spend, the honest check on whether something actually stopped

Budget fields look like a shortcut for "what is still running" and are not one — see [change budgets and bids](edit-budgets-and-bids.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
