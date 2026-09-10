# Ask about Meta, Google and TikTok in one question

The client does not run "a Meta account", they run paid media — and the only question they ever ask is which channel is worth the money this month.

## Ask this

```
Compare my Meta Ads, Google Ads and TikTok Ads for the last 30 days:
spend, impressions, clicks and landing page views per platform,
plus cost per click.
Then show me the same three platforms for the previous 30 days.
```

Ask it in one message rather than one platform at a time. The columns come back aligned to the same period, so you are reading a table instead of reconciling three exports by hand.

## What comes back

One row per platform, same columns, same period.

| Platform | Spend | Impressions | Clicks | Landing page views | Cost / click |
|---|---|---|---|---|---|
| Google Ads | 118,400.00 | 15,210,000 | 194,300 | 121,400 | 0.61 |
| Meta Ads | 92,700.00 | 1,604,000 | 98,500 | 58,900 | 0.94 |
| TikTok Ads | 54,900.00 | 6,712,000 | 218,400 | 74,200 | 0.25 |

> [!NOTE]
> Invented figures. The shape — one row per platform, aligned columns, one question — is real; the numbers are not anyone's.

## How to read it

The comparison is only honest for the metrics every platform counts the same way: **spend, impressions, clicks**. Those three, plus the costs derived from them, are the safe cross-channel row.

Read cost per click as the price of traffic, not the quality of it. The cheapest clicks in the table are usually the least qualified ones; that is a reason to check what happened after the click, not a reason to move budget.

**Cross-platform fields are named differently from Meta-only fields, and this catches people out.** Everything that belongs to one connector is prefixed — `facebook_ads_spend`, `facebook_ads_clicks`. The cross-platform fields that sit above all your connectors have **no prefix at all**. Landing page views is one of them: the field is `landing_page_views`, and asking for `facebook_ads_landing_page_view` is a hard error, not an empty column. If a field is meant to line up three platforms in one row, try it without the prefix first.

If the accounts bill in different currencies, a spend column that mixes them is meaningless. Ask for spend converted to one currency, or ask for each account's currency alongside the spend so you can see the mix.

Meta's history is capped at 37 months by Meta's own API. A comparison reaching further back than that has nothing to reach for.

Meta's cost columns are precise pass-throughs and come back with six decimal places — round them for the client, not before you compare them. [The weekly report page](weekly-and-monthly-report.md) has the detail.

## The trap

> [!WARNING]
> **The cross-platform "conversions" column returns zero for Meta.**
>
> Put it in a three-platform table and Meta looks like it converted nothing, sitting next to Google and TikTok showing real numbers. It is the most expensive wrong conclusion in this repository: a channel gets defunded because a column was blank.
>
> Meta's conversions have to be asked for by their own prefixed names — `facebook_ads_offsite_conversion_fb_pixel_purchase`, `facebook_ads_offsite_conversion_fb_pixel_lead` — as a separate step, and stitched into the table by hand.
>
> Never let a blended conversions column decide a budget. Spend, impressions, clicks and landing page views are what genuinely line up across three platforms; conversions are not, and pretending otherwise is how the wrong channel gets cut.

## Go deeper

- Same three platforms, but broken down by week.
- Which platform's spend grew most versus the previous 30 days?
- Show me Meta purchases and Google conversions side by side, each named explicitly.
- Add my Shopify revenue to the same period so I can see total return.
- Publish this as a hosted report I can send to the client.

## Fields this uses

- [`facebook_ads_spend`](../../reference/all-fields.md) — and the matching spend field on each other connector
- [`facebook_ads_impressions`](../../reference/all-fields.md)
- [`facebook_ads_clicks`](../../reference/all-fields.md) · [`facebook_ads_inline_link_clicks`](../../reference/all-fields.md)
- [`facebook_ads_cpc`](../../reference/all-fields.md)
- [`facebook_ads_spend_usd`](../../reference/all-fields.md) — converted spend, for mixed-currency accounts
- [`facebook_ads_account_currency`](../../reference/all-fields.md) · [`facebook_ads_account_name`](../../reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../../reference/all-fields.md) — Meta conversions, named explicitly
- `landing_page_views` — cross-platform, **no connector prefix**

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
