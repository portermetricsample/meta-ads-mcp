# Work out why a campaign stopped spending

The campaign says active, the budget is sitting there untouched, and yesterday it spent nothing at all.

## Ask this

```
My Meta campaign has stopped spending. Diagnose it.

Show me daily spend, impressions and reach for the last 21 days for
every campaign, so I can see the exact day each one stopped.

For the campaign that stopped, show its status and the status of every
ad set and ad inside it, plus the daily budget and remaining budget at
both campaign and ad set level, and the bid amount if one is set.

Then show me the account balance, the account spend cap and the account
status.
```

## What comes back

**Daily spend** — the date the line goes flat is the answer to "when"

```
date       spend     impressions   reach
20260817   1,240.55     42,000     31,900
20260818   1,190.02     40,500     30,400
…
20260827   1,205.31     41,100     30,800
20260828       0.00          0          0
20260829       0.00          0          0
20260830       0.00          0          0
```

> [!TIP]
> The date comes back as `20260830`, not `2026-08-30`. Paste that column into a spreadsheet and it reads as a number, which quietly breaks the sort. There is also a bare `facebook_ads_week` field that gives the ISO week with **no year** in it — fine inside one year, wrong the moment your window crosses New Year. Ask for `facebook_ads_year_week` instead.

**The structure** — one row per level, illustrative values

| Level | Name | Status | Daily budget | Budget remaining | Bid amount |
|---|---|---|---|---|---|
| Campaign | Campaign A | ACTIVE | 0.0 | 0.0 | — |
| Ad set | Ad set A1 | ACTIVE | 400.0 | 268.14 | 12 |
| Ad set | Ad set A2 | PAUSED | 300.0 | 0.0 | — |
| Ad | Ad A1-a | ACTIVE | — | — | — |

Both zeros on the campaign row are normal: this campaign's budget lives on its ad sets, so the campaign-level columns have nothing to report. Read the trap below before you draw anything from either budget column.

**The account**

```
account status      <status>
balance             <amount>
spend cap           <amount>
```

## How to read it

Work top down and stop at the first thing that is wrong. Almost every dead campaign is one of five things.

- **Something upstream is paused.** There are three separate status fields — campaign, ad set and ad — and they can disagree. An ad can report itself active while the ad set above it is paused. Read all three columns, not just the one you clicked on.
- **The account itself is stopped, not the campaign.** Check the account status, the balance and the spend cap. If the flat line starts on the same date across every campaign in the account, the problem is the account and no amount of campaign-level digging will find it.
- **The budget is under the account minimum** for its currency, which Meta refuses rather than throttles. The exact minimums and the error text are in [errors.md](../06-reference/errors.md).

If none of those explain it, check whether the ads themselves were changed recently: a new ad set with an age cap and the Advantage+ audience flag set to on is rejected at creation, and once that combination exists it cannot be repaired by editing — it has to be rebuilt.

### Where this connector is weaker than Ads Manager

Be straight with the client about this rather than guessing.

- **There is no dayparting or ad-scheduling parameter.** Ads run continuously between their start and end times, so "it is outside its schedule" is not a diagnosis you can make or fix here. The full list is in [what-it-cannot-do.md](../06-reference/what-it-cannot-do.md).
- **The catalog documented in this repo exposes status fields, not review outcomes.** You can see that an ad is not delivering; the reference does not document a field that states a policy decision. Run `list_actions` before concluding something is missing, and use Ads Manager for anything this reference marks as unavailable.
- **History stops at 37 months**, which is Meta's retention limit rather than a connector choice. A very old comparison window will error rather than return a short answer.

## The trap

> [!WARNING]
> **"Budget remaining: 0.0" is the most common false diagnosis on this page, and it almost never means the money ran out.** A budget column reads `0.0` whenever the budget lives at the other level — campaign columns are `0.0` for every campaign budgeted on its ad sets, and ad set columns are `0.0` when the budget sits on the campaign. A campaign spending normally can show `0.0` in every budget column it has.
>
> Worse, when the column is not zero it still does not mean what it says. On a daily-budget object, "remaining" is what is left **before midnight tonight** — not what is left for the flight or the month. On a lifetime-budget object it is what is left for the whole flight. Both arrive in the same column with nothing marking which is which.
>
> So you cannot answer "did it exhaust its budget" from these fields. Answer it from daily spend instead: the day-by-day line tells you when delivery stopped, and a campaign that is still spending today has not run out. The full account of why these fields mislead is in [budget pacing](../01-reporting/budget-pacing.md).

## Go deeper

- Show me hour by hour spend for the last three days, to see whether it dies at the same time each day.
- List every ad set in this account whose parent campaign is paused.
- Show me daily spend per ad set for the last 21 days, so I can see whether one ad set died or all of them did.
- Did frequency spike in the week before delivery stopped?
- Compare this campaign's cost per link click in its last active week against the month before.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md) · [`facebook_ads_impressions`](../06-reference/all-fields.md) · [`facebook_ads_reach`](../06-reference/all-fields.md)
- [`facebook_ads_date`](../06-reference/all-fields.md) · [`facebook_ads_day`](../06-reference/all-fields.md) · [`facebook_ads_year_week`](../06-reference/all-fields.md)
- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_ad_status`](../06-reference/all-fields.md) · [`facebook_ads_adset_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_daily_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_lifetime_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_budget_remaining`](../06-reference/all-fields.md) · [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md)
- [`facebook_ads_bidamount`](../06-reference/all-fields.md) · [`facebook_ads_spend_cap`](../06-reference/all-fields.md) · [`facebook_ads_balance`](../06-reference/all-fields.md) · [`facebook_ads_account_status`](../06-reference/all-fields.md) · [`facebook_ads_account_currency`](../06-reference/all-fields.md)

The budget fields above are read here only to see **which level the budget sits on**. Do not read exhaustion or pacing from them — see the trap.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
