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
| Campaign A | 4,120.35 | 512,300 | 2,410 | 0.00470427 | 1.709689 | 38 |
| Campaign B | 2,880.16 | 366,900 | 1,120 | 0.00305260 | 2.571571 | 11 |
| Campaign C | 940.09 | 88,400 | 610 | 0.00690045 | 1.541131 | 9 |

| Campaign | Spend Δ | Link clicks Δ | Cost / link click Δ | Purchases Δ |
|---|---|---|---|---|
| Campaign A | +12% | +6% | +6% | −3% |
| Campaign B | −4% | −22% | +23% | −40% |
| Campaign C | +180% | +150% | +12% | +125% |

> [!NOTE]
> Every number on this page is invented. The **shape** is real: this is the precision the connector actually returns — long decimals on the rates, six decimal places on the cost columns, cents on campaign spend.

## How to read it

Spend tells you where the money went. Cost per link click tells you what happened to the price of traffic. Purchases tell you whether the traffic was worth buying. Read them in that order and the report writes itself.

**The cost columns are trustworthy.** Cost per link click matches spend ÷ link clicks exactly, out to six decimal places — nothing is rounded on the way to you. In a repository that is mostly warnings, this is the part you can lift straight into the report. If a cost number looks wrong, it is the click field underneath it that changed, not the arithmetic.

A campaign where spend is flat and cost per link click is climbing is getting more expensive at the same volume — that is the paragraph the client cares about, and it usually points at [creative fatigue](creative-fatigue.md).

A campaign that grew 180% is almost always a campaign that was switched on mid-period. Check the dates before you present it as a win.

Reach counts people, not events, so it deduplicates. Ask for it over the exact period you are reporting rather than adding four weekly numbers together.

## The trap

> [!WARNING]
> **Rates come back as decimal fractions, not percentages — paste one into a report and you are wrong by 100x.**
>
> A link click-through rate of **2.56%** arrives as `0.025567691511131932`. Not 2.56. Not 2.5567. A long decimal beginning with a zero.
>
> This applies to every rate field: `facebook_ads_ctr`, `facebook_ads_inline_link_click_ctr`, `facebook_ads_unique_ctr`, `facebook_ads_outbound_CTR` and the rest. Campaign A above shows `0.00470427`, which is **0.47%**.
>
> Two things go wrong in practice. A number pasted raw into a client deck reads as *0.0047%* and looks like a catastrophe. A number formatted as a percentage by a spreadsheet that already treats it as one reads as *0.47*, and looks like a rounding error rather than a rate.
>
> Multiply by 100 before anyone sees it, and say in the report that you did. Every other page in this section shows rates in this same raw form for the same reason.

## Go deeper

- Break last month's spend down by placement and tell me the cheapest per link click.
- Show the same campaigns split by age and gender.
- Give me last month by week so I can see the trend inside the period.
- Which ads inside the top-spending campaign drove the purchases?
- Show me the same table with revenue and return on ad spend instead of purchases.

## Fields this uses

- [`facebook_ads_spend`](../../reference/all-fields.md) — spend for the period you asked for
- [`facebook_ads_impressions`](../../reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../../reference/all-fields.md) — clicks to your destination
- [`facebook_ads_inline_link_click_ctr`](../../reference/all-fields.md) — a decimal fraction, see the trap above
- [`facebook_ads_cost_per_inline_link_click`](../../reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../../reference/all-fields.md)
- [`facebook_ads_purchase_roas_purchase`](../../reference/all-fields.md)
- [`facebook_ads_campaign_name`](../../reference/all-fields.md) · [`facebook_ads_year_week`](../../reference/all-fields.md) · [`facebook_ads_month`](../../reference/all-fields.md)

Ask for `facebook_ads_year_week` rather than `facebook_ads_week` — [creative fatigue](creative-fatigue.md) explains why the short one breaks.
