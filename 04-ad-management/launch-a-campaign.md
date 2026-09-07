# Launch a campaign, ad set and ad in one go

The creative is approved, the client wants it live tomorrow, and you do not want to click through Ads Manager three times to build the same thing.

## Ask this

```
Build me a paused Traffic campaign in my Meta ad account.
Use the lowest cost strategy with no bid cap.
Ad set: Colombia only, ages 25 to 54, optimizing for link clicks,
daily budget 50000 in account currency, Advantage+ Audience turned off.
Ad: use the image at <public image URL>, headline "<headline>",
body "<body text>", a Learn More button, landing page <your URL>.
Leave everything paused and show me the ids you created.
```

## What comes back

Three ids, one per level. Ids below are made up for illustration.

```
campaign  120250000000000001   PAUSED
ad set    120250000000000002   CO · age 25-54 · advantage_audience 0 · LINK_CLICKS
ad        120250000000000003   PAUSED
```

## How to read it

Three ids means all three levels were built and linked. If you only get one or two, the chain broke and the missing level is where the error is — nothing below a missing level exists.

The ad set line is your receipt on targeting: country, age range, whether Advantage+ Audience was left off, and what the ad set is optimizing for. Read it against the brief before you activate anything.

Ask for a read-back — "show me this campaign, ad set and ad as they are stored now" — and compare body, headline, image and button to what you sent.

Say "leave everything paused" in the request and check the status you get back before you go any further. Paused is the state you want while you review; activating is a separate, deliberate instruction.

Some objectives are simply not available to build here: app-install optimization, the messaging `CONVERSATIONS` goal, and catalog or Advantage+ Shopping campaigns. Check [what it cannot do](../06-reference/what-it-cannot-do.md) before you promise a client a campaign type. Targeting has its own limits — one OR-group of interests, no exclusions, no language targeting — set out in [audiences and lookalikes](audiences-and-lookalikes.md).

## The trap

> [!WARNING]
> **The bid strategy you get by default is one you are not allowed to ask for.** Create a campaign without naming a strategy and Meta stores `LOWEST_COST_WITH_BID_CAP` — verified by creating a real campaign and reading it back. That is a bid-cap strategy, and it needs a bid amount nobody prompted you for; without one the campaign looks correct and cannot deliver.
>
> It is not even in the list you can choose from — that offers `LOWEST_COST_WITHOUT_CAP`, `COST_CAP`, `BID_CAP` and `MINIMUM_ROAS`. So the fix is not to avoid it, it is to **always say `LOWEST_COST_WITHOUT_CAP` explicitly** unless you want a cap.

> [!WARNING]

> [!NOTE]
> A second one that bites at creation: if you cap the age below 65, Advantage+ Audience must be off. Turning it on alongside an age cap is rejected, with error subcode 1870189.

## Go deeper

- Read this campaign, ad set and ad back and confirm the targeting and creative match the brief.
- Look up the geolocation code for `<city or region>` so I can target it instead of the whole country.
- Build a second ad set under the same campaign, identical except for the age range, so I can compare.
- Which performance goals are valid for this campaign objective?
- Show me the preview links for this ad so I can see it before it runs.

## Fields this uses

- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_objective`](../06-reference/all-fields.md) · [`facebook_ads_buying_type`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_id`](../06-reference/all-fields.md) · [`facebook_ads_adset_id`](../06-reference/all-fields.md) · [`facebook_ads_ad_id`](../06-reference/all-fields.md)
- [`facebook_ads_adsettargeting_age_min`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_age_max`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_countries`](../06-reference/all-fields.md)
- [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md) · [`facebook_ads_bidamount`](../06-reference/all-fields.md) — and see [change budgets and bids](edit-budgets-and-bids.md) for which level a budget lands on

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
