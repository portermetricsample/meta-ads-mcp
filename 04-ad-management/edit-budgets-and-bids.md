# Change budgets and bids without opening Ads Manager

The client just moved money between campaigns, and you have four budget edits to make before the day's spend starts.

> [!NOTE]
> **What on this page has actually been run.** How budgets behave when you **read** them was checked against a live ad account on 2026-09-07, three separate ways, and that is the core of this page. Setting a budget **at creation** was also executed. **Editing the budget of an object that already exists was not run**, and neither was switching a campaign between daily and lifetime. The field and parameter names below are the connector's real ones; the response your account gives back to an edit is something you should read for yourself.

## Ask this

```
In my Meta ad account, for every active campaign show me the campaign daily budget,
the campaign lifetime budget, the campaign budget remaining, and the ad set daily
budget, so I can see which level the budget actually sits on.
Then raise the daily budget of "<campaign name>" to <new amount> in account currency,
and lower "<other campaign name>" to <new amount>.
Leave every status untouched and read the same columns back to me afterwards.
```

## What comes back

One row per campaign, with a budget column for each level. **The figures below are invented to show the shape** — no number here came from an account. What is real is the pattern: budgets carry decimals, and a level that does not hold the budget reads `0.0`, not blank.

| Campaign | campaign daily | campaign lifetime | campaign remaining | ad set daily |
|---|---|---|---|---|
| `<campaign A>` | 350.0 | 0.0 | 212.75 | 0.0 |
| `<campaign B>` | 0.0 | 0.0 | 0.0 | 180.0 |
| `<campaign C>` | 0.0 | 12000.0 | 4180.0 | 0.0 |

Campaign B is not a campaign without a budget. Its budget lives on its ad sets, so every campaign-level column reads `0.0`.

## How to read it

**Find the level before you edit.** Budget sits either on the campaign, shared by its ad sets, or on each ad set separately. Whichever level does not hold it tells you nothing — and it tells you nothing in two different ways depending on how you look. Edit the level that is not holding the money and the request can succeed while delivery does not change at all.

**"Remaining" is not what is left this month.** On a daily budget it is what is left **today**. A campaign created seconds earlier, which had never delivered anything, came back with its remaining exactly equal to its daily budget — that is a day's allowance, not a period balance. The same column also carries lifetime-remaining for lifetime-budget objects, with nothing in the response saying which kind you are looking at. **It cannot answer a pacing question. Pace from spend by day instead — [budget pacing](../01-reporting/budget-pacing.md) is the page for that, and it is written on top of the same finding.**

**Say the amount the way a human says it.** The creation parameter is `daily_budget_amount` and it takes the account's **major** currency unit — 30 means thirty of them, not thirty cents. Pass `5` and Meta stores `500` in minor units, converted on its side. **Never multiply by 100 yourself**; doing it lifts the budget by 100x. Anything unusually large is stopped by `confirm_large_budget`, which guards amounts over 5000x the account minimum.

**Read the edit back.** Ask for the same columns again after the change. The before/after is your only proof the amount landed on the object you meant.

Bids are a separate control from budget. If a campaign runs a bid-cap strategy, its ad sets need a bid amount; lowest cost with no cap removes that requirement. The strategy you may choose is `LOWEST_COST_WITHOUT_CAP`, `COST_CAP`, `BID_CAP` or `MINIMUM_ROAS` — and the one you get when you say nothing is not on that list. That trap is explained in full on [launch a campaign](launch-a-campaign.md). A spend cap and a target ROAS cannot be set through this connector at all; for a ROAS floor ask for `MINIMUM_ROAS` with a bid value. The rest is an Ads Manager job, listed in [what it cannot do](../06-reference/what-it-cannot-do.md).

## The trap

> [!WARNING]
> **A budget you cannot see does not mean "no budget". It means "not at this level" — and the connector says so two different ways.**
>
> - **In the reporting columns**, an empty level reads `0.0`. A campaign whose budget sits on its ad sets shows `0.0` in every campaign budget column while it spends normally, and an ad set under a campaign budget shows `0.0` in the ad set column.
> - **On the object itself, read straight back from Meta**, the field is not `0.0` — it is **absent**. An ad set created under a campaign-level budget came back with no `daily_budget` and no `bid_strategy` at all. Nothing to parse, nothing to compare, no error.
>
> Both were seen in the same live run, on top of an earlier read that showed the same thing from the other direction. So: ask for the campaign and the ad set columns in the **same** answer, decide from that which level actually holds the money, and edit only that one. Editing the empty level is the quiet failure here — no error, no change in spend.

## Go deeper

- For this campaign, show me every ad set with its own daily budget, so I can see where the money is set.
- Switch this campaign to a lifetime budget of `<amount>` running until `<date>`.
- Move this campaign from a shared campaign budget to per-ad-set budgets.
- Set this campaign to lowest cost with no bid cap so it can deliver without a bid amount.
- Compare each campaign's daily budget with what it actually spent per day over the last 7 days.

## Fields this uses

- [`facebook_ads_campaign_daily_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_lifetime_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_budget_remaining`](../06-reference/all-fields.md)
- [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md) · [`facebook_ads_bidamount`](../06-reference/all-fields.md)
- [`facebook_ads_account_currency`](../06-reference/all-fields.md) — every amount is in this currency, so confirm it before typing a number copied from another account's plan
- [`facebook_ads_balance`](../06-reference/all-fields.md)
- [`facebook_ads_spend`](../06-reference/all-fields.md) — period spend, and the only honest input to a pacing answer

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
