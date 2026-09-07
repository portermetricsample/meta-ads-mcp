# See who converts and who burns budget

Spend is flat, results are down, and nobody can tell you whether the problem is the creative or the fact that half the budget is going to a phone screen nobody buys on.

## Ask this

```
For the last 30 days, break my Meta ad spend down four separate ways.
Give me a separate table for each, do not mix them.

1. By age and gender
2. By platform and placement position
3. By device
4. By country

Every table should have spend, impressions, link clicks, cost per link
click, purchases and cost per purchase, sorted by spend.
```

## What comes back

Four tables.

> [!NOTE]
> Every figure in this repository is invented. What is real is the **shape** — the column order, the row granularity, and the fact that Instagram comes back as five separate surfaces rather than one bucket.

**Age and gender**

```
25-34 female   4,100 spend |  61,200 imp |  1,340 clicks
25-34 male     3,250 spend |  49,800 imp |    910 clicks
35-44 female   2,700 spend |  38,400 imp |    620 clicks
35-44 male     1,900 spend |  27,100 imp |    410 clicks
45-54 female     800 spend |  11,300 imp |    150 clicks
45-54 male       550 spend |   7,900 imp |     90 clicks
```

**Placement** — Instagram comes back as five distinct surfaces, not one bucket

| Placement | Spend | Impressions | Clicks |
|---|---|---|---|
| Instagram · Reels | 5,400 | 84,000 | 1,900 |
| Instagram · Feed | 3,100 | 46,500 | 780 |
| Instagram · Stories | 2,900 | 41,200 | 560 |
| Instagram · Explore | 1,400 | 19,800 | 210 |
| Instagram · Profile Feed | 500 | 4,200 | 70 |

**Device**

```
android_smartphone   102,400 imp |  2,050 clicks
iphone                88,700 imp |  1,780 clicks
desktop               31,500 imp |     95 clicks
ipad                  10,200 imp |    140 clicks
android_tablet         6,800 imp |     85 clicks
other                  1,900 imp |     20 clicks
```

**Country** — one row per country, same columns.

## How to read it

Look for the row where the share of spend and the share of results are furthest apart. In the device table above, desktop takes roughly a fifth of the impressions and returns about three percent of the clicks — that is the single most actionable line in the whole audit, and it is invisible in any report that says "mobile vs desktop".

Placement is where the money usually leaks, because the five Instagram surfaces behave nothing alike. Reels and Stories are watched; Feed and Explore are scrolled; Profile Feed is often a rounding error taking budget from something better. Before you exclude a placement, check whether it is genuinely expensive or just small — a placement with a handful of impressions has no reliable cost per result yet.

Age and gender is the table clients ask for and the one you should act on last. It describes who Meta chose to show the ads to, which is largely a consequence of your creative and your objective. Treat a skew as a finding about the creative, not a reason to hard-target.

Country matters most when one market is subsidising another inside a single ad set. If two countries have very different costs per purchase, they need different ad sets and different budgets, not a shared one.

## The trap

> [!WARNING]
> Spend, impressions and clicks add up across these rows; **reach and frequency do not**. Reach counts distinct people, and one person can appear on Instagram Reels on Tuesday and Instagram Stories on Thursday — they are one person in the account total and two rows in the placement table. Adding the reach column gives a number larger than your real audience, and any frequency you calculate from it is wrong. Ask for reach at the level you intend to report it, and use the deduplicated `unique_*` fields when you need people rather than events.

## Go deeper

- Split placement by age group so I can see which surface works for which age.
- Which hour of the day has the cheapest cost per purchase, in my time zone?
- Show me the same country table broken down by region for my largest market.
- Which placements are getting spend but have produced no purchases in 30 days?
- Compare cost per purchase by device for the last 30 days against the 30 days before.

## Fields this uses

- [`facebook_ads_age`](../06-reference/all-fields.md) · [`facebook_ads_gender`](../06-reference/all-fields.md)
- [`facebook_ads_publisher_platform`](../06-reference/all-fields.md) · [`facebook_ads_platform_position`](../06-reference/all-fields.md)
- [`facebook_ads_device_platform`](../06-reference/all-fields.md) · [`facebook_ads_impression_device`](../06-reference/all-fields.md)
- [`facebook_ads_country_code`](../06-reference/all-fields.md) · [`facebook_ads_country_name`](../06-reference/all-fields.md) · [`facebook_ads_region`](../06-reference/all-fields.md) · [`facebook_ads_dma`](../06-reference/all-fields.md)
- [`facebook_ads_hourly_stats_aggregated_by_advertiser_time_zone`](../06-reference/all-fields.md)
- [`facebook_ads_reach`](../06-reference/all-fields.md) · [`facebook_ads_frequency`](../06-reference/all-fields.md)
- [`facebook_ads_unique_inline_link_clicks`](../06-reference/all-fields.md) · [`facebook_ads_unique_action_purchase`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
