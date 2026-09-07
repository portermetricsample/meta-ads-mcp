# See who converts and who burns budget

Spend is flat, results are down, and nobody can tell you whether the problem is the creative or the fact that half the budget is going to a surface nobody buys on.

## Ask this

```
For the last 30 days, break my Meta ad spend down four separate ways.
Give me a separate table for each, do not mix them.

1. By age and gender
2. By publisher platform and platform position
3. By device
4. By country

Every table should have spend, impressions, link clicks, link click
rate, cost per link click, purchases and cost per purchase, sorted by
spend. Show spend exactly as it comes back, do not round it.
```

## What comes back

Four tables.

> [!NOTE]
> Every figure in this repository is invented, and the row labels in the age, device and country tables are illustrative. The **placement list below is not** — those are the real platform and position values the connector returns.

**Age and gender**

```
25-34 female   4,100 spend |  61,200 imp |  1,340 clicks
25-34 male     3,250 spend |  49,800 imp |    910 clicks
35-44 female   2,700 spend |  38,400 imp |    620 clicks
35-44 male     1,900 spend |  27,100 imp |    410 clicks
45-54 female     800 spend |  11,300 imp |    150 clicks
45-54 male       550 spend |   7,900 imp |     90 clicks
```

**Placement** — seven publisher platforms and nineteen position rows

| Platform | Position | Spend | Impressions | Link clicks | Link CTR |
|---|---|---|---|---|---|
| facebook | feed | 4,075.987200 | 412,800 | 6,190 | 0.01499516 |
| instagram | feed | 3,462.898800 | 331,600 | 5,240 | 0.01580217 |
| instagram | instagram_reels | 2,889.161400 | 297,300 | 4,910 | 0.01651530 |
| facebook | facebook_reels | 2,181.018400 | 268,400 | 3,720 | 0.01385991 |
| instagram | instagram_stories | 1,573.540200 | 188,200 | 1,640 | 0.00871413 |
| facebook | facebook_stories | 1,069.784100 | 141,900 | 1,180 | 0.00831572 |
| facebook | instream_video | 602.932000 | 96,500 | 402 | 0.00416580 |
| audience_network | an_classic | 552.935200 | 74,600 | 903 | 0.01210456 |
| instagram | instagram_explore_grid_home | 495.806400 | 62,100 | 508 | 0.00818035 |
| facebook | facebook_reels_overlay | 264.000200 | 38,200 | 214 | 0.00560209 |
| facebook | search | 243.660400 | 21,400 | 366 | 0.01710280 |
| unknown | unknown | 193.922100 | 26,700 | 143 | 0.00535581 |
| messenger | messenger_stories | 186.285000 | 27,500 | 188 | 0.00683636 |
| threads | threads_feed | 137.566800 | 15,900 | 232 | 0.01459119 |
| facebook | biz_disco_feed | 101.815900 | 12,700 | 118 | 0.00929134 |
| audience_network | rewarded_video | 94.848900 | 18,300 | 96 | 0.00524590 |
| instagram | instagram_search | 89.464200 | 9,800 | 74 | 0.00755102 |
| whatsapp | status | 49.618800 | 8,400 | 61 | 0.00726190 |
| facebook | facebook_notification | 26.812800 | 4,900 | 41 | 0.00836735 |

Cost and purchase columns are trimmed here for width; ask for them and they arrive alongside.

> [!TIP]
> **Two things about the numbers in that table, before you paste any of them anywhere.**
>
> **The rate is a decimal fraction, not a percentage.** A link CTR of `0.01499516` is **1.50%**. Every `*_ctr` field behaves this way. Put the raw figure in a report labelled "%" and you are out by a factor of a hundred.
>
> **Spend grows six decimal places under a breakdown.** A campaign row reports spend to two decimals — `18292.06`. Split the same spend by placement and every row comes back to six — `4075.987200`, `3462.898800`, and so on down the table. Round each row to cents before you add them up and the total lands a hair off the account figure: above, the raw rows sum to `18292.058800` and the rounded rows sum to `18292.07`. Reconcile on the raw values, or allow a tolerance and stop hunting for a bug that is not there.

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

Look for the row where the share of spend and the share of results are furthest apart. In the device table above, desktop takes about 13% of the impressions and returns about 2% of the clicks — that is the single most actionable line in the whole audit, and it is invisible in any report that says "mobile vs desktop".

Placement is where the money usually leaks, and the reason is the length of that table. This is not Facebook versus Instagram. It is nineteen distinct surfaces across seven platforms, and three of them are places most advertisers never consciously chose: Audience Network, which is other people's apps; WhatsApp status; and Threads. Read the small rows before the big ones — that is where you find budget going somewhere nobody signed off on.

Then check whether a weak placement is genuinely expensive or just small. A surface with a few thousand impressions has no reliable cost per result yet, and excluding it on one bad week is how you end up strangling delivery for no gain.

Age and gender is the table clients ask for and the one you should act on last. It describes who Meta chose to show the ads to, which is largely a consequence of your creative and your objective. Treat a skew as a finding about the creative, not a reason to hard-target.

Country matters most when one market is subsidising another inside a single ad set. If two countries have very different costs per purchase, they need different ad sets and different budgets, not a shared one.

## The trap

> [!WARNING]
> **There is an `unknown / unknown` row in the placement table, it holds real spend, and you cannot attribute it to anything.** It is not an error and it is not empty — it comes back with impressions, clicks and money against it, and the platform and position both literally read `unknown`. You cannot exclude it, optimise it, or explain it to a client. Two things follow. First, the placement rows you *can* read do not account for all the spend, so never present a placement table as a complete split without saying what the unknown row took. Second, if you build a "% of budget by placement" chart, that row has to appear in it — quietly dropping it is how a chart ends up adding to 97% and nobody notices.

## Go deeper

- How much spend landed in the unknown placement row over the last 90 days, month by month?
- Split placement by age group so I can see which surface works for which age.
- Show me spend and purchases on Audience Network, Threads and WhatsApp separately from Facebook and Instagram.
- Which hour of the day has the cheapest cost per purchase, in my time zone?
- Show me the same country table broken down by region for my largest market.
- Which placements are getting spend but have produced no purchases in 30 days?

## Fields this uses

- [`facebook_ads_age`](../06-reference/all-fields.md) · [`facebook_ads_gender`](../06-reference/all-fields.md)
- [`facebook_ads_publisher_platform`](../06-reference/all-fields.md) · [`facebook_ads_platform_position`](../06-reference/all-fields.md)
- [`facebook_ads_device_platform`](../06-reference/all-fields.md) · [`facebook_ads_impression_device`](../06-reference/all-fields.md)
- [`facebook_ads_country_code`](../06-reference/all-fields.md) · [`facebook_ads_country_name`](../06-reference/all-fields.md) · [`facebook_ads_region`](../06-reference/all-fields.md) · [`facebook_ads_dma`](../06-reference/all-fields.md)
- [`facebook_ads_hourly_stats_aggregated_by_advertiser_time_zone`](../06-reference/all-fields.md)
- [`facebook_ads_spend`](../06-reference/all-fields.md) · [`facebook_ads_impressions`](../06-reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../06-reference/all-fields.md) · [`facebook_ads_inline_link_click_ctr`](../06-reference/all-fields.md) · [`facebook_ads_cost_per_inline_link_click`](../06-reference/all-fields.md)
- [`facebook_ads_unique_inline_link_clicks`](../06-reference/all-fields.md) · [`facebook_ads_unique_action_purchase`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
