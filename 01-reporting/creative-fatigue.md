# Catch creative fatigue before it costs you

Same ads have been running for six weeks, nothing was changed, and the cost per click has been drifting up — this is the ten-minute weekly check, not a full creative teardown.

## Ask this

```
For my Meta ad account, show me the last 6 weeks by week and by ad:
frequency, impressions, reach, CPM, link click-through rate,
and cost per link click.
Only include ads with meaningful spend in the last week.
Point out the ads where frequency went up while link click-through rate
went down and cost per link click went up.
```

## What comes back

One row per ad per week, so you can see the direction rather than a single snapshot.

| Ad | Week | Frequency | CPM | Link CTR | Cost / link click |
|---|---|---|---|---|---|
| Ad A | W1 | 1.4 | 6.10 | 0.82% | 0.74 |
| Ad A | W3 | 2.1 | 6.80 | 0.61% | 1.11 |
| Ad A | W6 | 3.6 | 8.40 | 0.38% | 2.21 |
| Ad B | W1 | 1.2 | 5.90 | 0.55% | 1.07 |
| Ad B | W6 | 1.3 | 6.00 | 0.57% | 1.05 |

> [!NOTE]
> Illustration only — real numbers, columns and units come from your own account.

## How to read it

Fatigue has a shape: **frequency climbing, link click-through rate falling, cost per link click rising, all at once.** Ad A above is the shape. One of the three moving on its own is noise; all three moving together for two or three weeks in a row is fatigue.

Frequency is impressions divided by the people reached. It rises either because the audience is small or because the ad has been in front of the same people for weeks. If reach has flattened while impressions keep growing, you have squeezed the audience dry.

CPM rising at the same time usually means the auction is charging you more to keep showing the same thing to the same people. That is the cost of not refreshing, and it is the number to put in front of whoever approves new creative.

Ad B is the control. Flat frequency and flat cost over six weeks is an ad that still has room — do not pause it just because it is old.

The three quality rankings Meta reports on an ad are a useful second opinion when a decision is close. They are a judgement, not a measurement, so let the cost trend lead.

## The trap

> [!WARNING]
> **Plain click-through rate is not link click-through rate.** The wide `facebook_ads_ctr` field counts likes, comments and profile taps as clicks, so an ad can lose every one of its actual visits while its click-through rate looks steady — the engagement clicks hold the number up and the fatigue hides. Ask for **link** click-through rate and **cost per link click** by name, and use the same click field in every week you compare.

## Go deeper

- Show me the second-by-second retention curve for the fatiguing video ads.
- Which placements is the tired ad still cheap in, and which have gone expensive?
- Split the fatiguing ad by age and gender — is one segment burnt out and the rest fine?
- Show me the preview link and thumbnail for each ad in this list.
- Pause the ads I name and tell me what the account spend looks like without them.

## Fields this uses

- [`facebook_ads_frequency`](../06-reference/all-fields.md) — impressions per person reached
- [`facebook_ads_reach`](../06-reference/all-fields.md) · [`facebook_ads_impressions`](../06-reference/all-fields.md)
- [`facebook_ads_cpm`](../06-reference/all-fields.md)
- [`facebook_ads_inline_link_click_ctr`](../06-reference/all-fields.md) — link clicks only
- [`facebook_ads_cost_per_inline_link_click`](../06-reference/all-fields.md)
- [`facebook_ads_quality_ranking`](../06-reference/all-fields.md) · [`facebook_ads_engagement_rate_ranking`](../06-reference/all-fields.md) · [`facebook_ads_conversion_rate_ranking`](../06-reference/all-fields.md)
- [`facebook_ads_ad_name`](../06-reference/all-fields.md) · [`facebook_ads_week`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
