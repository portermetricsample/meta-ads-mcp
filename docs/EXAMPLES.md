# Example prompts — and the shape of what comes back

Every response below is the real structure this server returns.

**On the numbers:** read-side figures are taken from live accounts and then **de-identified** — brand names removed and values rescaled. The *shape* is exact: the column order, the row counts, the units, the ordering. Write-side figures (ids, the video upload) are unaltered, because they come from Porter's own test account.

## Account totals

> **How much did I spend on Meta ads last month?**

```
spend        16,492
impressions   2,174
clicks           73
```

## Which campaign spent the money

> **Which campaign did that spend come from?**

```
16,492 | 2,174 | 73 | "<campaign name>" | 120211044318980323
```

Worth knowing: this campaign had been **deleted**. The spend is still attributed to it by name — many tools return a blank or drop the row.

## Placement breakdown

> **Break that down by placement.**

| Placement | Spend | Impressions | Clicks |
|---|---|---|---|
| Instagram · Reels | 8,679 | 988 | 41 |
| Instagram · Feed | 3,801 | 554 | 10 |
| Instagram · Stories | 3,728 | 559 | 20 |
| Instagram · Explore | 254 | 66 | 2 |
| Instagram · Profile Feed | 30 | 7 | 0 |

Five distinct Instagram surfaces, not one bucket labelled "Instagram".

## Demographics

> **Who is my audience, by age and gender?**

```
25-34 female   5,792 |  804 | 26
25-34 male     4,808 |  688 | 28
35-44 female   2,323 |  265 |  8
35-44 male     2,328 |  272 |  8
45-54 female     509 |   57 |  1
45-54 male       432 |   54 |  2
```

Sums exactly to the account total — worth checking, because deduplicated metrics like reach do **not**.

## Device

> **Which devices are my ads showing on?**

```
android_smartphone  |  795,136 imp |  8,117 clicks
iphone              |  390,979 imp |  5,482 clicks
ipad                |   29,436 imp |    538 clicks
desktop             |  249,272 imp |    236 clicks
android_tablet      |   23,485 imp |    232 clicks
other               |    6,098 imp |     37 clicks
ipod                |       14 imp |      0 clicks
```

Desktop bought a fifth of the impressions and 3% of the clicks — the kind of split that only shows up when the breakdown is available.

## Real conversions

> **How many leads and WhatsApp conversations did this account generate?**

```
leads                                  80
landing page views                384,830
messaging conversations started       285
```

`onsite_conversion_messaging_conversation_started_7d` is a separate field from `leads`. Asking for "conversions" alone returns neither cleanly — see [FIELDS.md](FIELDS.md).

## Cross-channel — the thing a Meta-only server cannot do

> **Compare my Meta, Google and TikTok spend for the last 30 days.**

| Platform | Spend | Clicks | Impressions |
|---|---|---|---|
| Google Ads | 119,872 | 196,842 | 15,837,081 |
| Meta Ads | 93,290 | 99,070 | 1,636,925 |
| TikTok Ads | 55,071 | 220,716 | 6,770,460 |

One question, three platforms, one call. TikTok bought the most clicks on the least spend.

## Creative review with previews

> **Show me my ads with their spend and a preview link.**

```
<ad name> | 1,684 | business.facebook.com/ads/api/preview_iframe.php?d=… | <thumbnail>
<ad name> | 1,299 | business.facebook.com/ads/api/preview_iframe.php?d=… | <thumbnail>
<ad name> |   208 | business.facebook.com/ads/api/preview_iframe.php?d=… | <thumbnail>
```

Nine preview surfaces are available as separate fields — feed, story, Reels, right column and more.

## Creating a campaign

> **Create a paused Traffic campaign for Colombia, ages 25–54, with this image and a Learn More button.**

```
campaign  120250160092660607   PAUSED
ad set    120250160103700607   CO · age 25-54 · advantage_audience 0 · LINK_CLICKS
ad        120250160105780607   PAUSED
```

Read back through Meta's own API afterwards: targeting stored exactly as requested, creative body / headline / image / CTA identical to what was sent.

> **Set the daily budget to 50,000,000.**

Refused, with the account minimum named — rather than accepted silently.

## Uploading a video from your machine

> **Upload this local MP4 to my ad account.**

```
video id 4621248201428062 — length 4.083s, uploading complete, processing complete
```

Accepts a public URL **or** raw base64, so an agent can upload a local file end to end with no human in the loop.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. Catalog verified against the live Porter MCP on 2026-09-07.*
