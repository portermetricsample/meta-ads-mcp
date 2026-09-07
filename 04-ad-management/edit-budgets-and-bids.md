# Change budgets and bids without opening Ads Manager

The client just moved money between campaigns, and you have four budget edits to make before the day's spend starts.

## Ask this

```
In my Meta ad account, show me each active campaign with its daily budget, 
lifetime budget and budget remaining. Then raise the daily budget of 
"<campaign name>" to <new amount> in account currency, and lower 
"<other campaign name>" to <new amount>. 
Leave every status untouched and show me the before and after.
```

## What comes back

A before/after table plus the ids that were edited. Amounts below are invented for illustration.

| Campaign | Level | Budget before | Budget after | Status |
|---|---|---|---|---|
| `<campaign A>` | daily | 120,000 | 180,000 | unchanged |
| `<campaign B>` | daily | 90,000 | 60,000 | unchanged |
| `<campaign C>` | lifetime | 2,400,000 | 2,400,000 | not edited |

A refused edit comes back as a refusal, not a silent success:

```
Budget Is Too Small — below the account minimum for this currency
amount converts to over 5000x the account daily minimum — resend with the large-budget confirmation if intended
```

## How to read it

Budget lives at one of two levels. If the campaign holds the budget, its ad sets share it; if the ad sets hold their own, the campaign shows none. Ask for both the campaign budget and the ad set budget in the same answer, and edit whichever one is actually populated — editing the empty one changes nothing you can see.

Switching a campaign between a daily and a lifetime budget is one instruction: "switch this campaign to a lifetime budget of X ending on date Y". The same instruction can move a campaign between shared (campaign-level) and per-ad-set budgets.

Two guardrails sit in front of you. A budget below the account minimum is rejected with the minimum named. A budget more than 5,000× the account's daily minimum is also rejected — a typo catcher. If the enormous number was deliberate, say so explicitly in your follow-up and it will go through.

Bids are a separate control from budget. If a campaign runs a bid cap strategy, its ad sets need a bid amount; asking for "lowest cost with no bid cap" removes that requirement entirely.

## The trap

> [!WARNING]
> **Every budget is in the ad account's own currency, and the minimum changes with it.** The documented floors are 3,076/day for COP accounts, 100/day for USD and 9,615/day for INR — so the same number is a rounding error in one account and a rejected edit in another. Before you type an amount, confirm which account and which currency you are in; a number copied from another client's plan is the most common cause of a refused or wildly oversized edit.

## Go deeper

- Show me every ad set under this campaign with its own daily budget and how much of it is left today.
- Switch this campaign to a lifetime budget of `<amount>` running until `<date>`.
- Move this campaign from a shared campaign budget to per-ad-set budgets.
- Set this campaign to lowest cost with no bid cap so it can deliver without a bid amount.
- Compare each campaign's daily budget with what it actually spent over the last 7 days.

## Fields this uses

- [`facebook_ads_campaign_daily_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_lifetime_budget`](../06-reference/all-fields.md) · [`facebook_ads_campaign_budget_remaining`](../06-reference/all-fields.md)
- [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md) · [`facebook_ads_bidamount`](../06-reference/all-fields.md) · [`facebook_ads_spend_cap`](../06-reference/all-fields.md)
- [`facebook_ads_account_currency`](../06-reference/all-fields.md) · [`facebook_ads_balance`](../06-reference/all-fields.md)
- [`facebook_ads_spend`](../06-reference/all-fields.md) — period spend, for checking an edit against reality

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
