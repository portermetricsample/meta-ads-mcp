# Catch creative fatigue before it costs you

Same ads have been running for six weeks, nothing was changed, and the cost per click has been drifting up — this is the ten-minute weekly check, not a full creative teardown.

## Ask this

```
For my Meta ad account, show me the last 6 weeks by year-week and by ad:
impressions, reach, frequency, CPM, link click-through rate,
and cost per link click.
Only include ads with meaningful spend in the last week.
Point out the ads where frequency went up while link click-through rate
went down and cost per link click went up.
```

Ask for **year-week**, not week. The reason is the trap at the bottom of this page.

## What comes back

One row per ad per week, so you can see the direction rather than a single snapshot.

| Ad | Week | Impressions | Reach | Frequency | CPM | Link CTR | Cost / link click |
|---|---|---|---|---|---|---|---|
| Ad A | 31 | 210,000 | 150,000 | 1.4 | 6.10 | 0.00820000 | 0.743902 |
| Ad A | 33 | 231,000 | 110,000 | 2.1 | 6.80 | 0.00609957 | 1.114833 |
| Ad A | 36 | 252,000 | 70,000 | 3.6 | 8.40 | 0.00380159 | 2.209603 |
| Ad B | 31 | 96,000 | 80,000 | 1.2 | 5.90 | 0.00550000 | 1.072727 |
| Ad B | 36 | 104,000 | 80,000 | 1.3 | 6.00 | 0.00570192 | 1.052277 |

> [!NOTE]
> Invented numbers, real shape. The week column is a bare integer and the click-through rate is a decimal fraction because that is what the connector hands back.

**Link CTR is a decimal fraction, not a percentage.** Ad A's `0.00820000` in week 31 is **0.82%**, and its `0.00380159` in week 36 is **0.38%**. [The weekly report page](weekly-and-monthly-report.md) covers this in full.

## How to read it

Fatigue has a shape: **frequency climbing, link click-through rate falling, cost per link click rising, all at once.** Ad A above is the shape. One of the three moving on its own is noise; all three moving together for two or three weeks in a row is fatigue.

Frequency is impressions divided by the people reached. It rises either because the audience is small or because the ad has been in front of the same people for weeks. Ad A's reach falls from 150,000 to 70,000 while impressions climb — that is a squeezed audience, not a growing one.

CPM rising at the same time usually means the auction is charging you more to keep showing the same thing to the same people. That is the cost of not refreshing, and it is the number to put in front of whoever approves new creative.

Ad B is the control. Flat frequency and flat cost over six weeks is an ad that still has room — do not pause it just because it is old.

Ask for **link** click-through rate by name every time. The wide `facebook_ads_ctr` field counts likes, comments and profile taps as clicks, so an ad can lose its actual visits while that number holds steady — see the click fields in [all fields](../06-reference/all-fields.md).

The three quality rankings Meta reports on an ad are a useful second opinion when a decision is close. They are a judgement, not a measurement, so let the cost trend lead.

## The trap

> [!WARNING]
> **`facebook_ads_week` has no year in it, and this page is the one that breaks.**
>
> Week 31 comes back as `31`. A bare integer. Nothing in the value says which year it belongs to, and nothing in the response adds it.
>
> For six weeks inside one year that is merely ugly. Run the same check across New Year and it is wrong: you get `50, 51, 52, 1, 2, 3`, and every tool that sorts numbers puts January first. Your fatigue curve now reads back to front — the tired ad looks like it is recovering, and the fresh one looks like it is dying.
>
> Ask for **`facebook_ads_year_week`** instead. It carries the year, it sorts correctly, and it costs you nothing.
>
> `facebook_ads_date` has the same rawness in a different form: `20260906`, not `2026-09-06`. A spreadsheet reads it as a number.

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
- [`facebook_ads_inline_link_click_ctr`](../06-reference/all-fields.md) — link clicks only, returned as a decimal fraction
- [`facebook_ads_cost_per_inline_link_click`](../06-reference/all-fields.md)
- [`facebook_ads_quality_ranking`](../06-reference/all-fields.md) · [`facebook_ads_engagement_rate_ranking`](../06-reference/all-fields.md) · [`facebook_ads_conversion_rate_ranking`](../06-reference/all-fields.md)
- [`facebook_ads_ad_name`](../06-reference/all-fields.md) · [`facebook_ads_year_week`](../06-reference/all-fields.md) — not `facebook_ads_week`

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
