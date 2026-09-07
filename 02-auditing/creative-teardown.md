# Work out why one ad works

One ad is quietly carrying the whole account and the client wants three more like it, so you need to know which part of it is doing the work.

## Ask this

```
Take my five highest-spending Meta ads from the last 30 days and tear
them down one by one.

For each ad give me: spend, impressions, 3-second video plays,
ThruPlays, and how many plays reached 25%, 50%, 75%, 95% and 100%.

Work out two ratios and show them as percentages: 3-second plays
divided by impressions, and ThruPlays divided by 3-second plays.

Then show the second-by-second retention curve for each ad.

Finally, for each ad show the headline text, the body text, the
call-to-action button, the image or video thumbnail, and a preview
link I can open.
```

## What comes back

**Per ad — the funnel**

| Ad | Spend | Impressions | 3s plays | ThruPlays | 25% | 50% | 75% | 95% | 100% |
|---|---|---|---|---|---|---|---|---|---|
| Ad 1 | 6,200.00 | 210,000 | 63,000 | 12,600 | 41,000 | 22,000 | 14,100 | 9,800 | 9,100 |
| Ad 2 | 4,800.00 | 180,000 | 34,200 | 4,100 | 20,500 | 8,900 | 5,000 | 3,600 | 3,300 |

Illustrative numbers, real structure.

**The two ratios**

```
Ad 1   3s plays / impressions  30.0%      ThruPlays / 3s plays  20.0%
Ad 2   3s plays / impressions  19.0%      ThruPlays / 3s plays  12.0%
```

> [!NOTE]
> Those two percentages are ones you asked to be worked out from the play counts. Any rate that comes straight out of the connector — anything ending in `_ctr` — arrives as a decimal fraction instead: `0.0256` means 2.56%. Full explanation in [audience-audit.md](audience-audit.md).

**The retention curve** — 17 points, the last one a "60 seconds or more" bucket

```
second 0   100%
second 1    72%
second 2    58%
second 3    49%
second 4    44%
…
second 60 or more
```

There are 17 of these fields, not one for every second of a minute, so ask for the field list if you need to know exactly which points are covered.

**The creative itself**

| Ad | Headline | Body | Button | Preview |
|---|---|---|---|---|
| Ad 1 | `<title asset text>` | `<body asset text>` | `<call to action>` | `<preview url>` |

## How to read it

The first ratio is the hook. It tells you what share of the people who were shown the ad stopped long enough to start it. It is a judgement on the first frame and almost nothing else — the thumbnail, the opening line, the first movement.

The second ratio is the hold. It tells you what share of the people who started actually stayed. A strong hook with a weak hold means the opening promised something the rest of the ad did not pay off — that is a script problem, not a thumbnail problem, and remaking the first three seconds will not fix it.

The second-by-second curve turns "the hold is weak" into an instruction. Find the second where the line falls off a cliff and go watch the ad at that timestamp. That is usually where the logo appears, where the voiceover changes speaker, or where the offer arrives too early.

Only then read the creative table. Once you know whether you have a hook problem or a hold problem, the headline, body and button tell you which element to rewrite for the next three variants. Open the preview link before you write anything — the same ad reads differently in a feed and in a story.

## The trap

> [!WARNING]
> A "video view" here is three seconds long. `facebook_ads_action_video_view` counts plays that reached the three-second mark, not people who watched your ad, and one person can be counted more than once. Build a hook rate on it and you get a usable number; describe that number to a client as "30% of people watched the ad" and you are wrong by an order of magnitude. When you need people rather than plays, ask for the deduplicated version, `facebook_ads_unique_3s_video_view`.

## Go deeper

- Show me the same teardown for my five worst-performing ads so I can compare the retention curves.
- Which call-to-action button has the best cost per link click across the whole account?
- Group my ads by image asset and show which image appears in the most winning ads.
- Show me each ad's quality ranking, engagement rate ranking and conversion rate ranking.
- For my carousel ads, which card gets the clicks — show card name, description and destination.
- Give me the story and Reels preview links for the top ad, not just the feed one.

## Fields this uses

- [`facebook_ads_action_video_view`](../06-reference/all-fields.md) · [`facebook_ads_unique_3s_video_view`](../06-reference/all-fields.md)
- [`facebook_ads_video_thruplay_watched_actions`](../06-reference/all-fields.md)
- [`facebook_ads_video_p25_watched_actions`](../06-reference/all-fields.md) … [`facebook_ads_video_p100_watched_actions`](../06-reference/all-fields.md)
- [`facebook_ads_video_avg_time_watched_actions`](../06-reference/all-fields.md)
- [`facebook_ads_video_play_curve_second_0`](../06-reference/all-fields.md) … [`second_60_more`](../06-reference/all-fields.md)
- [`facebook_ads_title_asset_text`](../06-reference/all-fields.md) · [`facebook_ads_body_asset_text`](../06-reference/all-fields.md) · [`facebook_ads_description_asset_text`](../06-reference/all-fields.md) · [`facebook_ads_call_to_action_asset_name`](../06-reference/all-fields.md)
- [`facebook_ads_image_asset_name`](../06-reference/all-fields.md) · [`facebook_ads_image_asset_url`](../06-reference/all-fields.md) · [`facebook_ads_video_asset_thumbnail_url`](../06-reference/all-fields.md) · [`facebook_ads_ad_format_asset`](../06-reference/all-fields.md)
- [`facebook_ads_ad_mobile_feed_preview_url`](../06-reference/all-fields.md) · [`facebook_ads_ad_instagram_preview_url`](../06-reference/all-fields.md) · [`facebook_ads_ad_instagram_story_preview_url`](../06-reference/all-fields.md)
- [`facebook_ads_quality_ranking`](../06-reference/all-fields.md) · [`facebook_ads_engagement_rate_ranking`](../06-reference/all-fields.md) · [`facebook_ads_conversion_rate_ranking`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
