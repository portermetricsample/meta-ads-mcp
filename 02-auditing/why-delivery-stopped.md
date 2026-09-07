# Work out why a campaign stopped spending

The campaign says active, the budget is sitting there untouched, and yesterday it spent nothing at all.

## Ask this

```
My Meta campaign has stopped spending. Diagnose it.

Show me daily spend, impressions and reach for the last 21 days for
every campaign, so I can see the exact day each one stopped.

For the campaign that stopped, show its status and the status of every
ad set and ad inside it, plus each ad set's daily budget, the campaign's
remaining budget, and the bid amount if one is set.

Then show me the account balance, the account spend cap and the account
status.
```

## What comes back

**Daily spend** — the date the line goes flat is the answer to "when"

```
day        spend   impressions   reach
-14        1,240      42,000     31,900
-13        1,190      40,500     30,400
…
-4         1,205      41,100     30,800
-3             0           0          0
-2             0           0          0
-1             0           0          0
```

**The structure** — one row per level, illustrative values

| Level | Name | Status | Daily budget | Budget remaining | Bid amount |
|---|---|---|---|---|---|
| Campaign | Campaign A | ACTIVE | — | 0 | — |
| Ad set | Ad set A1 | ACTIVE | 400 | — | 12 |
| Ad set | Ad set A2 | PAUSED | 300 | — | — |
| Ad | Ad A1-a | ACTIVE | — | — | — |

**The account**

```
account status      <status>
balance             <amount>
spend cap           <amount>
```

## How to read it

Work top down and stop at the first thing that is wrong. Almost every dead campaign is one of five things.

- **Something upstream is paused.** An active ad inside a paused ad set delivers nothing, and the ad still reports itself as active. Read all three status columns, not just the one you clicked on.
- **The money ran out.** A lifetime budget that has been fully spent shows as zero remaining. An account-level spend cap or an empty balance stops every campaign at once — if the flat line starts on the same day across the whole account, it is the account, not the campaign.
- **The bid cap is strangling it.** If the campaign runs on a bid-cap strategy and the bid is set below what the auction currently costs, it will simply stop winning impressions. Spend goes to zero with no error anywhere.
- **A bid strategy was set without a bid.** A campaign created on the bid-cap strategy with no bid amount cannot deliver at all. This is the most common way a newly created campaign never starts — see the bid-amount error in [errors.md](../06-reference/errors.md).
- **The budget is under the account minimum** for its currency, which Meta refuses rather than throttles. The exact minimums and the error text are in [errors.md](../06-reference/errors.md).

If none of those explain it, check whether the ads themselves were changed recently: a new ad set with an age cap and the Advantage+ audience flag set to on is rejected at creation, and once that combination exists it cannot be repaired by editing — it has to be rebuilt.

### Where this connector is weaker than Ads Manager

Be straight with the client about this rather than guessing.

- **There is no dayparting or ad-scheduling parameter.** Ads run continuously between their start and end times, so "it is outside its schedule" is not a diagnosis you can make or fix here. The full list is in [what-it-cannot-do.md](../06-reference/what-it-cannot-do.md).
- **The catalog documented in this repo exposes status fields, not review outcomes.** You can see that an ad is not delivering; the reference does not document a field that states a policy decision. Run `list_actions` before concluding something is missing, and use Ads Manager for anything this reference marks as unavailable.
- **History stops at 37 months**, which is Meta's retention limit rather than a connector choice. A very old comparison window will error rather than return a short answer.

## The trap

> [!WARNING]
> An empty result is not the same as a zero. When a query comes back with no rows, that means the question could not be answered — not that the campaign spent nothing. Diagnose a dead campaign off an empty response and you will "confirm" an outage that never happened. Before you believe it, widen the date range as far as it will legally go and drop the breakdowns one at a time until rows appear; if the aggregate has spend and the detailed cut does not, the problem is your query, not the campaign.

## Go deeper

- Show me hour by hour spend for the last three days, to see whether it dies at the same time each day.
- List every ad set in this account whose parent campaign is paused.
- Show me the daily budget on every active ad set, and the total of those budgets.
- Did frequency spike in the week before delivery stopped?
- Compare this campaign's cost per link click in its last active week against the month before.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md) · [`facebook_ads_impressions`](../06-reference/all-fields.md) · [`facebook_ads_reach`](../06-reference/all-fields.md)
- [`facebook_ads_date`](../06-reference/all-fields.md) · [`facebook_ads_day`](../06-reference/all-fields.md)
- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_ad_status`](../06-reference/all-fields.md) · [`facebook_ads_adset_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_daily_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_lifetime_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_budget_remaining`](../06-reference/all-fields.md) · [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md)
- [`facebook_ads_bidamount`](../06-reference/all-fields.md) · [`facebook_ads_spend_cap`](../06-reference/all-fields.md) · [`facebook_ads_balance`](../06-reference/all-fields.md) · [`facebook_ads_account_status`](../06-reference/all-fields.md) · [`facebook_ads_account_currency`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
