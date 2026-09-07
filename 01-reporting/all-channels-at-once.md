# Ask about Meta, Google and TikTok in one question

The client does not run "a Meta account", they run paid media — and the only question they ever ask is which channel is worth the money this month.

## Ask this

```
Compare my Meta Ads, Google Ads and TikTok Ads for the last 30 days:
spend, impressions and clicks per platform, plus cost per click.
Then show me the same three platforms for the previous 30 days.
```

Ask it in one message. It is one call across the connected accounts, not three questions stitched together afterwards.

## What comes back

One row per platform, same columns, same period.

| Platform | Spend | Impressions | Clicks | Cost / click |
|---|---|---|---|---|
| Google Ads | 118,400 | 15,210,000 | 194,300 | 0.61 |
| Meta Ads | 92,700 | 1,604,000 | 98,500 | 0.94 |
| TikTok Ads | 54,900 | 6,712,000 | 218,400 | 0.25 |

> [!NOTE]
> Illustration only. The shape — one row per platform, aligned columns, one query — is real; the numbers are not anyone's.

## How to read it

The comparison is only honest for the metrics every platform counts the same way: **spend, impressions, clicks**. Those three, plus the costs derived from them, are the safe cross-channel row.

Read cost per click as the price of traffic, not the quality of it. The cheapest clicks in the table are usually the least qualified ones; that is a reason to check what happened after the click, not a reason to move budget.

If the accounts bill in different currencies, a spend column that mixes them is meaningless. Ask for spend converted to one currency, or ask for each account's currency alongside the spend so you can see the mix.

Anything past three years is gone — Meta keeps roughly three years of history, so a five-year comparison will fail rather than come back short.

## The trap

> [!WARNING]
> **The generic cross-platform "conversions" column returns zero for Meta.** Put it in a three-platform table and Meta looks like it converted nothing, next to Google and TikTok showing real numbers — the most expensive wrong conclusion in this whole repo. Ask for Meta's conversions by their own names (purchases, leads, messaging conversations) as a separate step, and never let a blended conversions column decide a budget.

## Go deeper

- Same three platforms, but broken down by week.
- Which platform's spend grew most versus the previous 30 days?
- Show me Meta purchases and Google conversions side by side, each named explicitly.
- Add my Shopify revenue to the same period so I can see total return.
- Publish this as a hosted report I can send to the client.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md) — and the matching spend field on each other connector
- [`facebook_ads_impressions`](../06-reference/all-fields.md)
- [`facebook_ads_clicks`](../06-reference/all-fields.md) · [`facebook_ads_inline_link_clicks`](../06-reference/all-fields.md)
- [`facebook_ads_cpc`](../06-reference/all-fields.md)
- [`facebook_ads_spend_usd`](../06-reference/all-fields.md) — converted spend, for mixed-currency accounts
- [`facebook_ads_account_currency`](../06-reference/all-fields.md) · [`facebook_ads_account_name`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) — Meta conversions, named explicitly

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
