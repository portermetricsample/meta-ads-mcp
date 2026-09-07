# Change budgets and bids without opening Ads Manager

The client just moved money between campaigns, and you have four budget edits to make before the day's spend starts.

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

One row per campaign, with a budget column for each level. Figures below are invented; the format is the one the connector returns — budgets carry decimals, and an empty budget reads `0.0`, not blank.

| Campaign | campaign daily | campaign lifetime | campaign remaining | ad set daily |
|---|---|---|---|---|
| `<campaign A>` | 350.0 | 0.0 | 212.75 | 0.0 |
| `<campaign B>` | 0.0 | 0.0 | 0.0 | 180.0 |
| `<campaign C>` | 0.0 | 12000.0 | 4180.0 | 0.0 |

Campaign B is not a campaign without a budget. Its budget lives on its ad sets, so every campaign-level column reads `0.0`.

## How to read it

**Find the level before you edit.** Budget sits either on the campaign, shared by its ad sets, or on each ad set separately. Whichever level does not hold it reads `0.0` in every budget column. Edit the level reading `0.0` and the request can succeed while nothing about delivery changes — you have set a budget on an object that is not the one spending.

**"Remaining" is not what is left this month.** On a daily budget it is what is left today. That column also carries lifetime-remaining for lifetime-budget objects, with nothing in the response saying which kind you are looking at, so it cannot answer pacing — pace from spend by day instead. Full explanation in [budget pacing](../01-reporting/budget-pacing.md).

**Read the edit back.** Ask for the same columns again after the change. The before/after is your only proof the amount landed on the object you meant.

Switching a campaign between a daily and a lifetime budget is one instruction: "switch this campaign to a lifetime budget of X ending on date Y". The same instruction can move a campaign between a shared campaign budget and per-ad-set budgets.

Bids are a separate control from budget. If a campaign runs a bid cap strategy, its ad sets need a bid amount; asking for lowest cost with no bid cap removes that requirement. A spend cap and a target ROAS cannot be set through this connector at all — for a ROAS floor, ask for the `MINIMUM_ROAS` bid strategy with a bid value. Everything else in that shape is an Ads Manager job, listed in [what it cannot do](../06-reference/what-it-cannot-do.md).

## The trap

> [!WARNING]
> **A `0.0` budget does not mean "no budget". It means "not at this level".** Campaign budget columns read `0.0` for every campaign whose budget sits on its ad sets, and the ad set column reads `0.0` when the budget sits on the campaign — while both campaigns spend normally. Ask for the campaign and ad set columns in the same answer, decide from that which level actually holds the money, and edit only that one. Editing the level showing `0.0` is the quiet failure here: no error, no change in spend.

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
- [`facebook_ads_spend`](../06-reference/all-fields.md) — period spend, for checking an edit against reality

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
