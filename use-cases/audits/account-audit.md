# Take over an account you did not build

A new client hands you their Meta ad account on Monday, nobody who built it still works there, and you have a call on Thursday.

## Ask this

```
Audit my Meta ad account for the last 90 days.

First give me the account total: spend, impressions, reach, frequency,
link clicks and cost per link click.

Then one row per campaign, sorted by spend, with objective, status,
spend, impressions, link clicks, cost per link click, and results.

Then do the same one level down for the ad sets inside the five
campaigns that spent the most.

Finish with a short list of anything that spent money and produced
no link clicks and no results.
```

## What comes back

Three tables and a list. Numbers below are illustrative only — the shape is what matters.

**Account total**

```
spend               48,300.00
impressions      1,942,000
reach              612,400
frequency             3.17
link clicks         21,880
cost per link click   2.207495
```

**By campaign** — one row per campaign

| Campaign | Objective | Status | Spend | Impressions | Link clicks | Cost / link click |
|---|---|---|---|---|---|---|
| Campaign A | OUTCOME_SALES | ACTIVE | 21,400.00 | 780,000 | 9,900 | 2.161616 |
| Campaign B | OUTCOME_TRAFFIC | ACTIVE | 14,600.00 | 640,000 | 8,100 | 1.802469 |
| Campaign C | OUTCOME_LEADS | PAUSED | 8,900.00 | 402,000 | 3,600 | 2.472222 |
| Campaign D | OUTCOME_AWARENESS | PAUSED | 3,400.00 | 120,000 | 280 | 12.142857 |

**By ad set** — same columns, one row per ad set, nested under the top five campaigns.

> [!NOTE]
> Spend arrives with two decimal places at campaign level and six once you split it by a breakdown such as placement or device, which is why a breakdown table will not tie back to the campaign total once you round it. That is explained where it bites, in [audience-audit.md](audience-audit.md).

## How to read it

Start with frequency at the account level. It tells you whether the account is reaching new people or showing the same ads to the same list over and over. High frequency next to a rising cost per link click usually means the audience is exhausted, not that the creative got worse.

Then read the campaign table as a budget allocation, not a scoreboard. The question is not "which campaign is best", it is "does the split of spend match the split of results". A campaign holding a third of the budget and a twentieth of the link clicks is the first thing you take to the client call.

The bottom list — spend with nothing to show for it — is your fastest saving. Objective matters here: an awareness campaign is not supposed to produce link clicks, so check the objective column before you call something waste.

Anything you cannot explain at campaign level, ask for again at ad set and then ad level. The same question works at every level; only the grouping changes.

## The trap

> [!WARNING]
> There are two spend fields and only one of them answers this question. `facebook_ads_amount_spent` is a lifetime figure for the whole account and ignores your date range, so it will happily report years of history as if it were the last 90 days. Period spend is `facebook_ads_spend`. If your account total looks impossibly large next to the sum of the campaign rows, this is why.

## Go deeper

- Show me the same 90 days month by month so I can see the trend.
- Show me daily spend by campaign so I can see which ones are still live and which stopped.
- Show me every ad set whose targeting age range and countries I can read back, so I can see what was actually set up.
- Break the account's spend down by placement and by country, so I can see where the money physically goes.
- Compare this account's last 90 days against the 90 days before that.

For "how is this account pacing" or "how much budget is left", do not read the budget fields — they answer a different question than the one you are asking. See [budget pacing](../reporting/budget-pacing.md).

## Fields this uses

- [`facebook_ads_spend`](../../reference/all-fields.md)
- [`facebook_ads_impressions`](../../reference/all-fields.md)
- [`facebook_ads_reach`](../../reference/all-fields.md)
- [`facebook_ads_frequency`](../../reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../../reference/all-fields.md)
- [`facebook_ads_cost_per_inline_link_click`](../../reference/all-fields.md)
- [`facebook_ads_campaign_name`](../../reference/all-fields.md) · [`facebook_ads_adset_name`](../../reference/all-fields.md) · [`facebook_ads_objective`](../../reference/all-fields.md) · [`facebook_ads_status`](../../reference/all-fields.md)
- [`facebook_ads_account_name`](../../reference/all-fields.md) · [`facebook_ads_account_currency`](../../reference/all-fields.md) · [`facebook_ads_account_status`](../../reference/all-fields.md)

Budget fields exist and are listed in the reference, but this audit does not use them. Read [budget pacing](../reporting/budget-pacing.md) before you do.
