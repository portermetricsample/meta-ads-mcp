# Launch a campaign, ad set and ad in one go

The creative is approved, the client wants it live tomorrow, and you do not want to click through Ads Manager three times to build the same thing.

## Ask this

```
Build me a paused Traffic campaign in my Meta ad account.
Ad set: Colombia only, ages 25 to 54, optimizing for link clicks, 
daily budget 50,000 in account currency, Advantage+ Audience turned off.
Use the lowest cost strategy with no bid cap.
Ad: use the image at <public image URL>, headline "<headline>", 
body "<body text>", a Learn More button, landing page <your URL>.
Leave everything paused and show me the ids you created.
```

## What comes back

Three ids, one per level, all paused. Ids below are made up for illustration.

```
campaign  120250000000000001   PAUSED
ad set    120250000000000002   CO · age 25-54 · advantage_audience 0 · LINK_CLICKS
ad        120250000000000003   PAUSED
```

## How to read it

Three ids means all three levels were built and linked. If you only get one or two, the chain broke and the missing level is where the error is — nothing below a missing level exists.

The ad set line is your receipt on targeting: country, age range, whether Advantage+ Audience was left off, and what the ad set is optimizing for. Read it against the brief before you activate anything.

Ask for a read-back — "show me this campaign, ad set and ad as they are stored now" — and compare body, headline, image and button to what you sent. Everything is paused, so a wrong ad costs nothing until you say go.

## The trap

> [!WARNING]
> If you do not name a bid strategy, the campaign is created on `LOWEST_COST_WITH_BID_CAP` — a bid cap strategy that needs a bid amount to work. Without that amount the campaign is built, looks correct, and **cannot deliver a single impression** when you activate it. Say "lowest cost, no bid cap" in the prompt, or supply a bid amount on purpose.

> [!NOTE]
> A second one that bites at creation: if you cap the age below 65, Advantage+ Audience must be off. Turning it on with an age cap is rejected, and on some accounts that combination cannot be repaired after the ad set exists — you rebuild the ad set.

## Go deeper

- Read this campaign, ad set and ad back and confirm the targeting and creative match the brief.
- Search for interests related to `<topic>` before I decide whether to narrow this ad set.
- Look up the geolocation code for `<city or region>` so I can target it instead of the whole country.
- Build a second ad set under the same campaign, identical except for the age range, so I can compare.
- Which performance goals are valid for this campaign objective?

## Fields this uses

- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_objective`](../06-reference/all-fields.md) · [`facebook_ads_buying_type`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_id`](../06-reference/all-fields.md) · [`facebook_ads_adset_id`](../06-reference/all-fields.md) · [`facebook_ads_ad_id`](../06-reference/all-fields.md)
- [`facebook_ads_adsettargeting_age_min`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_age_max`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_countries`](../06-reference/all-fields.md)
- [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md) · [`facebook_ads_bidamount`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
