# Pause and restart campaigns, ad sets and ads

It is 6pm on Friday, the promo is over, and everything for that offer has to stop spending tonight.

## Ask this

```
In my Meta ad account, list every campaign, ad set and ad whose name 
contains "<promo name>", with its current status. 
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

Pausing the campaign is enough to stop the money. Everything under it stops delivering with it, and each child keeps its own status, so restarting the campaign brings back exactly what was running before — including anything you had deliberately paused. That is usually what you want.

Pause the ad level instead when only one creative is the problem and the rest of the ad set should keep learning.

To restart, say the same sentence with "activate" in place of "pause", and be explicit about the level: activating a campaign does nothing for an ad set you paused separately.

Use the "before" column as your record of what to restore. Take that list before you pause anything, not after.

## The trap

> [!WARNING]
> **The status you set and the status that decides delivery are two different things.** An ad can read ACTIVE while its ad set or campaign is paused above it — nothing spends, and the ad still says ACTIVE. When you check whether something is really running, ask for the effective status, or ask for all three levels together as in the table above. Reading one level alone is how "it's live" turns into a week of zero delivery.

## Go deeper

- Which of my campaigns, ad sets and ads are actually delivering right now?
- Restart only the ad sets I paused on `<date>`, and leave the rest alone.
- Pause every ad in this ad set except `<ad name>`.
- Show me all paused campaigns that still have budget remaining.
- List everything in this account by effective status, so I can see what is stopped and at which level.

## Fields this uses

- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_adset_status`](../06-reference/all-fields.md) · [`facebook_ads_ad_status`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_name`](../06-reference/all-fields.md) · [`facebook_ads_adset_name`](../06-reference/all-fields.md) · [`facebook_ads_ad_name`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_budget_remaining`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
