# Find the winners and the money pits

Budget renewal is next week and you have to say, with a straight face, which campaigns deserve more money and which ones you are switching off.

## Ask this

```
For the last 60 days, rank my Meta campaigns by spend and give me,
for each one: spend, impressions, link clicks, cost per link click,
purchases, cost per purchase, leads, cost per lead, and return on
ad spend.

Then repeat the same table at ad set level.

Sort each table by cost per purchase, cheapest first, and put every
row with spend but zero purchases and zero leads at the bottom under
a heading called "spent, produced nothing".
```

## What comes back

Two tables with the same columns, one per level. Figures are made up for illustration; the columns, the ordering and the empty cells are real.

| Campaign | Spend | Link clicks | Cost / link click | Purchases | Cost / purchase | ROAS |
|---|---|---|---|---|---|---|
| Campaign A | 12,400 | 5,900 | 2.10 | 214 | 57.94 | 3.9 |
| Campaign B | 9,800 | 4,100 | 2.39 | 121 | 80.99 | 2.4 |
| Campaign C | 7,600 | 2,050 | 3.71 | 38 | 200.00 | 0.8 |
| **spent, produced nothing** | | | | | | |
| Campaign D | 4,300 | 610 | 7.05 | 0 | — | — |
| Campaign E | 1,900 | 88 | 21.59 | 0 | — | — |

An em dash in a cost-per column means the denominator was zero, not that the cost was zero.

## How to read it

Read the table in three passes. First, the bottom block: spend with no purchases and no leads is money you can move this week without an argument. Check the objective before you cut — an awareness or engagement campaign was never asked to produce purchases.

Second, cost per purchase against ROAS. They can disagree, and when they do, ROAS wins the argument: a campaign selling a high-priced product can carry a cost per purchase that looks terrible and still be the most profitable thing in the account. Cost per purchase alone quietly rewards whatever you sell cheapest.

Third, the gap between levels. A campaign with an acceptable average almost always contains one ad set carrying it and one or two dragging it down. The campaign table tells you where to look; the ad set table tells you what to actually turn off. Do not act on the campaign row — act on the ad set row underneath it.

Anything you kill, kill by pausing, not deleting, so next month's version of this table still reconciles.

## The trap

> [!WARNING]
> Deleted campaigns still hold their spend. The connector attributes historical spend to a campaign by name even after it has been removed from the account, so a top row in this ranking can be something you cannot open, edit or scale. That is the honest answer — the money really was spent — but it means "increase the budget on the winner" is sometimes impossible. Check that each row you plan to act on still exists before you promise the client anything.

## Go deeper

- Break the top three campaigns down week by week so I can see whether the winner is still winning.
- Which ad sets have the best cost per purchase but the smallest budget right now?
- Show me quality ranking, engagement rate ranking and conversion rate ranking for every ad in the losing campaigns.
- Show the same ranking by return on ad spend instead of cost per purchase, and tell me where the two disagree.
- Compare these 60 days with the previous 60 days, campaign by campaign.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../06-reference/all-fields.md) · [`facebook_ads_cost_per_inline_link_click`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) · [`facebook_ads_cost_per_purchase`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_lead`](../06-reference/all-fields.md) · [`facebook_ads_cost_per_lead`](../06-reference/all-fields.md)
- [`facebook_ads_purchase_roas_purchase`](../06-reference/all-fields.md) · [`facebook_ads_website_purchase_roas`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_name`](../06-reference/all-fields.md) · [`facebook_ads_adset_name`](../06-reference/all-fields.md) · [`facebook_ads_objective`](../06-reference/all-fields.md) · [`facebook_ads_status`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
