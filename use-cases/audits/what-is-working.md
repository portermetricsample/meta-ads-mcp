# Find the winners and the money pits

Budget renewal is next week and you have to say, with a straight face, which campaigns deserve more money and which ones you are switching off.

## Ask this

```
For the last 60 days, rank my Meta campaigns by spend and give me,
for each one: spend, impressions, link clicks, cost per link click,
purchases, cost per purchase, leads, cost per lead, and return on
ad spend.

For purchases and leads use the named pixel events, not the
all-conversions total.

Then repeat the same table at ad set level.

Sort each table by cost per purchase, cheapest first, and put every
row with spend but zero purchases and zero leads at the bottom under
a heading called "spent, produced nothing".
```

## What comes back

Two tables with the same columns, one per level. Figures are made up for illustration; the columns, the ordering, the decimal places and the empty cells are real.

| Campaign | Spend | Link clicks | Cost / link click | Purchases | Cost / purchase | ROAS |
|---|---|---|---|---|---|---|
| Campaign A | 12,400.00 | 5,900 | 2.101695 | 214 | 57.9439 | 3.9 |
| Campaign B | 9,800.00 | 4,100 | 2.390244 | 121 | 80.9917 | 2.4 |
| Campaign C | 7,600.00 | 2,050 | 3.707317 | 38 | 200.0000 | 0.8 |
| **spent, produced nothing** | | | | | | |
| Campaign D | 4,300.00 | 610 | 7.049180 | 0 | — | — |
| Campaign E | 1,900.00 | 88 | 21.590909 | 0 | — | — |

An em dash in a cost-per column means the denominator was zero, not that the cost was zero.

> [!TIP]
> **The cost columns are exact, and you can hand them straight to a client.** They arrive with more decimal places than you want — six on cost per link click, four on cost per lead — but they are honest pass-throughs, not rounded summaries. Checked against the raw inputs, `facebook_ads_cost_per_lead` matched spend ÷ leads to the fourth decimal, and `facebook_ads_cost_per_inline_link_click` matched spend ÷ link clicks to the sixth. There is no rounding drift to correct for. Round them yourself for the slide; do not recompute them because you distrust them.

## How to read it

Read the table in three passes. First, the bottom block: spend with no purchases and no leads is money you can move this week without an argument. Check the objective before you cut — an awareness or engagement campaign was never asked to produce purchases.

Second, cost per purchase against ROAS. They can disagree, and when they do, ROAS wins the argument: a campaign selling a high-priced product can carry a cost per purchase that looks terrible and still be the most profitable thing in the account. Cost per purchase alone quietly rewards whatever you sell cheapest.

Third, the gap between levels. A campaign with an acceptable average almost always contains one ad set carrying it and one or two dragging it down. The campaign table tells you where to look; the ad set table tells you what to actually turn off. Do not act on the campaign row — act on the ad set row underneath it.

## The trap

> [!WARNING]
> **Ask for "conversions" instead of naming the event, and this ranking sorts on the wrong number.** `facebook_ads_conversions_all` counts every action — video views, likes, comments — not business results. On one real campaign over one 30-day window it returned a figure larger by three orders of magnitude. A ranking built on it does not rank sales. It ranks engagement, and it will hand the budget to whichever campaign got the most video views. Name the event you actually sell — `facebook_ads_offsite_conversion_fb_pixel_purchase` or `facebook_ads_offsite_conversion_fb_pixel_lead` — every time you ask. The proven numbers are in [conversion-tracking-audit.md](conversion-tracking-audit.md).

## Go deeper

- Break the top three campaigns down week by week so I can see whether the winner is still winning.
- Which ad sets have the best cost per purchase but the lowest spend over the window?
- Show me quality ranking, engagement rate ranking and conversion rate ranking for every ad in the losing campaigns.
- Show the same ranking by return on ad spend instead of cost per purchase, and tell me where the two disagree.
- Compare these 60 days with the previous 60 days, campaign by campaign.

Before you move money onto a winner, read [budget pacing](../reporting/budget-pacing.md) — the budget fields do not tell you how much room a campaign has left.

## Fields this uses

- [`facebook_ads_spend`](../../reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../../reference/all-fields.md) · [`facebook_ads_cost_per_inline_link_click`](../../reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../../reference/all-fields.md) · [`facebook_ads_cost_per_purchase`](../../reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_lead`](../../reference/all-fields.md) · [`facebook_ads_cost_per_lead`](../../reference/all-fields.md)
- [`facebook_ads_purchase_roas_purchase`](../../reference/all-fields.md) · [`facebook_ads_website_purchase_roas`](../../reference/all-fields.md)
- [`facebook_ads_campaign_name`](../../reference/all-fields.md) · [`facebook_ads_adset_name`](../../reference/all-fields.md) · [`facebook_ads_objective`](../../reference/all-fields.md) · [`facebook_ads_status`](../../reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
