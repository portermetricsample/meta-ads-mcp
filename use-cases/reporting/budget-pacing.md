# Am I on track to spend what I promised?

You committed a monthly budget to a client. It is the 20th. Are you going to land on it, overshoot, or leave money unspent?

## Ask this

```
Show me my Meta ad spend day by day for this month, and the total so far.
```

## What comes back

One row per day, plus the total.

```
spend      date
3,509.81   20260831
2,416.46   20260901
2,099.64   20260902
2,151.97   20260903
1,996.19   20260904
2,077.70   20260905
2,202.14   20260906
```

> [!NOTE]
> Figures throughout this repository are invented. The **shape** is real: this is the column order and the date format the connector actually returns.

## How to read it

Three numbers give you the whole answer:

- **Spent so far** — add the column up.
- **Daily average** — spent so far ÷ days elapsed.
- **Where you land** — daily average × days in the month.

Compare that last number to what you promised. Over means pull budgets back; under means you have room, and unspent budget is the more common failure.

The day-by-day view also shows you *when* it drifted. A flat line that suddenly halves is a campaign that stopped delivering, not a pacing problem — that belongs in [why delivery stopped](../audits/why-delivery-stopped.md).

> [!WARNING]
> **The budget fields cannot tell you this, and they will quietly mislead you if you try.**
>
> There are budget fields — `facebook_ads_campaign_daily_budget`, `facebook_ads_campaign_budget_remaining`, and ad set twins of both. None of them answers "am I pacing." Three things go wrong:
>
> - **"Remaining" is not what is left this month.** On a daily-budget campaign it is what is left *today*. A campaign showing a 470 daily budget and 311 remaining has not got 311 left for the month — it has 311 left before midnight.
> - **The number is blank wherever the budget is not.** Campaign budget columns read `0.0` for every campaign whose budget sits on its ad sets, and the ad set columns read `0.0` when it sits on the campaign. A campaign with real spend and `0.0` in every budget column is normal, not broken.
> - **"Remaining" means two different things in one column.** A daily-budget object reports what is left today; a lifetime-budget object reports what is left for the whole flight. Nothing in the response tells you which one you are looking at.
>
> Pace from spend by day. It is the only number that means one thing.

> [!TIP]
> Dates come back as `20260906`, not `2026-09-06`. If you paste the column into a spreadsheet it will read as a number — format it as a date, or ask for it grouped by week or month instead.

## Go deeper

- Show me the same daily spend broken down by campaign, so I can see which one is drifting.
- Compare this month's spend so far against the same days last month.
- Which campaigns spent nothing in the last seven days?
- Show me spend by week for the last three months, so I can see the trend rather than the noise.
- What is my average daily spend over the last 30 days?

## Fields this uses

- `facebook_ads_spend` — see [all fields](../../reference/all-fields.md)
- `facebook_ads_date`
- `facebook_ads_campaign_name`

Budget fields exist and are listed in the reference, but read the warning above before using them for pacing.
