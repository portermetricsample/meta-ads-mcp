# Send the weekly or monthly report

It is Monday morning, the client wants last week's numbers by campaign, and they will ask "is that better or worse than the week before?" in the first reply.

## Ask this

```
For my Meta ad account, give me last week by campaign: spend, impressions,
link clicks, link click-through rate, cost per link click, and purchases.
Then show me the same campaigns for the week before, and the change for each.
Sort by spend, highest first.
```

Swap "last week" for "last month" and "the week before" for "the month before" — nothing else changes.

## What comes back

One row per campaign, then the same set for the earlier period, then a change column.

| Campaign | Spend | Impressions | Link clicks | Link CTR | Cost / link click | Purchases |
|---|---|---|---|---|---|---|
| Campaign A | 4,120 | 512,300 | 2,410 | 0.47% | 1.71 | 38 |
| Campaign B | 2,880 | 366,900 | 1,120 | 0.31% | 2.57 | 11 |
| Campaign C | 940 | 88,400 | 610 | 0.69% | 1.54 | 9 |

| Campaign | Spend Δ | Link clicks Δ | Cost / link click Δ | Purchases Δ |
|---|---|---|---|---|
| Campaign A | +12% | +6% | +6% | −3% |
| Campaign B | −4% | −22% | +23% | −40% |
| Campaign C | +180% | +150% | +12% | +125% |

> [!NOTE]
> Every number on this page is an illustration. It shows the columns, units and ordering you get back, not anyone's real account.

## How to read it

Spend tells you where the money went. Cost per link click tells you what happened to the price of traffic. Purchases tell you whether the traffic was worth buying. Read them in that order and the report writes itself.

A campaign where spend is flat and cost per link click is climbing is getting more expensive at the same volume — that is the paragraph the client cares about, and it usually points at [creative fatigue](creative-fatigue.md).

A campaign that grew 180% is almost always a campaign that was switched on mid-period. Check the dates before you present it as a win.

Deleted campaigns still carry their spend and still appear by name. If a row looks unfamiliar, it may be something that was removed during the period — the money was real, so leave it in the total.

## The trap

> [!WARNING]
> **Reach and frequency cannot be added up across periods.** They count people, not events, and the same person shows up in week 1 and week 2. Four weekly reach numbers added together will be larger than the month's real reach. Spend, impressions and clicks add up fine; reach and frequency have to be asked for over the exact period you want to report.

## Go deeper

- Break last month's spend down by placement and tell me the cheapest per link click.
- Show the same campaigns split by age and gender.
- Give me last month by week so I can see the trend inside the period.
- Which ads inside the top-spending campaign drove the purchases?
- Show me the same table with revenue and return on ad spend instead of purchases.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md) — spend for the period you asked for
- [`facebook_ads_impressions`](../06-reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../06-reference/all-fields.md) — clicks to your destination
- [`facebook_ads_inline_link_click_ctr`](../06-reference/all-fields.md)
- [`facebook_ads_cost_per_inline_link_click`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md)
- [`facebook_ads_purchase_roas_purchase`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_name`](../06-reference/all-fields.md) · [`facebook_ads_week`](../06-reference/all-fields.md) · [`facebook_ads_month`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
