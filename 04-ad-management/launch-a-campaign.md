# Launch a campaign, ad set and ad in one go

The creative is approved, the client wants it live tomorrow, and you do not want to click through Ads Manager three times to build the same thing.

You give your assistant one instruction. Underneath, it makes four calls in a fixed order — **campaign → ad set → image upload → ad** — and each one needs the one before it. Everything on this page comes from that sequence being run for real against a live Meta ad account, read back through Meta, and then deleted.

## Ask this

```
Build me a paused Traffic campaign in my Meta ad account.
Bid strategy: lowest cost without a bid cap. Daily budget 5 in account currency.
No special ad category. Budget sharing off.
Ad set: United States, ages 25 to 54, Facebook and Instagram only,
optimizing for link clicks, Advantage+ Audience off.
Ad: upload the image at <public image URL>, headline "<headline>",
body "<body text>", a Learn More button, landing page <your URL>.
Leave everything paused and show me each id and each read-back as you go.
```

## What comes back, step by step

Every id, hash and name below is **made up for illustration**. Only the field names, the values Meta stored, and the behaviour are real.

### 1. The campaign

```
campaign id            120000000000000001        ← made-up id
objective              OUTCOME_TRAFFIC
daily_budget           500                       ← 5 was sent
budget_remaining       500
effective_status       PAUSED
special_ad_categories  []                        ← ["NONE"] was sent
bid_strategy           LOWEST_COST_WITH_BID_CAP  ← nothing was sent for this
```

Three things in that read-back are worth stopping on.

**The budget was sent as `5` and stored as `500`.** The parameter is `daily_budget_amount` and it takes the number you would say out loud — 5 means five, 30 means thirty. Meta converts to its own minor units on its side. Never multiply by 100 yourself; the connector's own description says so, and doing it anyway spends 100x what you meant.

**`special_ad_categories` went in as `["NONE"]` and came back as `[]`.** That is normal. An empty array on read does not mean you forgot to declare it.

**`budget_remaining` matches the daily budget exactly** on a campaign that has never delivered, because "remaining" is what is left *today*, not what is left in the flight. It is not a pacing number.

That `bid_strategy` line is the one that matters most, and it is the first trap below.

### 2. The ad set

```
ad set id            120000000000000002   ← made-up id
geo_locations        countries: ["US"]
                     location_types: ["frequently_in", "home", "recent"]
age_min              25
age_max              54
advantage_audience   0
publisher_platforms  ["facebook", "instagram"]
daily_budget         (absent)
bid_strategy         (absent)
```

> [!WARNING]
> **`location_types` was never sent. Meta added it.** One country went in; three location types came back, and two of them are not residents — people who **recently visited** and people who **frequently travel to** the country. If you are building anything local, read the trap below before you spend money on it.

Age, Advantage+ Audience and the platform list all came back exactly as they were sent. The budget fields are simply missing, because the budget lives on the campaign — a budget column reads blank at whichever level does not hold the budget, so never read a blank as a zero budget.

The parameter names here do not look like Meta's own field names. `targeting_geo_location_countries` is rejected outright as an unrecognized parameter. The real one is **`targeting_countries`**. Verified working alongside it: `targeting_age_min`, `targeting_age_max`, `targeting_advantage_audience`, `targeting_publisher_platforms`. They are flat `targeting_*` names, and the connector builds Meta's nested structure itself.

### 3. The image

```
images:
  628.jpg:
    hash   <made-up hash string>
```

The response is keyed by **file name**, and the file name is taken from the last piece of the image URL. An image URL ending in `/1200/628` produced a key called `628.jpg`. So there is no fixed key to look for — your assistant has to read the first entry under `images` and take its hash. That hash is what the ad is built from.

### 4. The ad

```
ad id             120000000000000003   ← made-up id
status            PAUSED
```

Three ids means all four calls landed and the chain is linked. If you only get one or two, the chain broke at the first missing level and nothing below it exists.

Ask for a read-back — "show me this campaign, ad set and ad as they are stored now" — and compare body, headline, image and button against the brief before anything is activated. Paused is the state you want while you review; activating is a separate, deliberate instruction, never a side effect of building.

## The traps

All six were hit or confirmed in the run described above.

> [!WARNING]
> **1 — The bid strategy you get by default is one you are not allowed to ask for.** Create a campaign without naming a strategy and Meta stores `LOWEST_COST_WITH_BID_CAP` — verified by creating a real campaign and reading it back. That is a bid-cap strategy, and it needs a bid amount nobody prompted you for; without one the campaign looks correct and cannot deliver.
>
> It is not even in the list you can choose from — that offers `LOWEST_COST_WITHOUT_CAP`, `COST_CAP`, `BID_CAP` and `MINIMUM_ROAS`. So the fix is not to avoid it, it is to **always say `LOWEST_COST_WITHOUT_CAP` explicitly** unless you want a cap.

> [!WARNING]
> **2 — Meta silently widens your geo targeting.** `targeting_countries: ["US"]` went in. What came back was `location_types: ["frequently_in", "home", "recent"]` — three types, none of them requested.
>
> That default reaches people who **recently visited** the country and people who **frequently travel to** it, on top of the people who live there. Nobody warns you, and it changes who sees the ad. If your offer only makes sense to residents — a local service, a physical shop, anything with a catchment area — assume part of the budget is going to travellers and visitors until you have checked the read-back yourself.

> [!NOTE]
> **3 — It is `headline`, not `title`.** Send `title` on the ad and it is dropped silently: no error, no headline, an ad that looks half-built in preview and nowhere else.

> [!NOTE]
> **4 — `link` is required even when the destination is inside the app.** There is no "no destination" ad here. Something has to go in `link`.

> [!NOTE]
> **5 — `special_ad_categories` is required, and it is an array.** For an ordinary ad the value is `["NONE"]`. Not `[]`, not the bare string `NONE` — a string is rejected outright. It then reads back as `[]`, which is expected, not a failure.

> [!NOTE]
> **6 — `is_adset_budget_sharing_enabled` must always be sent.** Leave it out and Facebook rejects the request. It is stated in the connector's own parameter description, and there is no sensible default to fall back on — send it every time, on or off.

And two more worth knowing before you build:

- `cta_type` is a short list, not free text. `LEARN_MORE` works; `GET_STARTED` is rejected on this connector.
- `page_id` is required on the ad. It comes from `facebook_ads.page_list` — ask for the account's pages first if you do not have it.
- If you cap the age below 65, Advantage+ Audience must be off. Turning it on alongside an age cap is rejected with error subcode 1870189.

## If it fails before anything is created

A campaign create that fails with `failed to resolve credentials` (HTTP 401) is not a permissions problem with the connector and not something to work around — that account's Meta connection needs reconnecting. In the test run, the same parameters that failed on one account wrote successfully on another.

## What was actually tested

The four calls on this page — campaign, ad set, image upload, ad — were executed end to end against a live Meta ad account, every object created paused, every one read back through Meta, and then deleted. Deleting the campaign removed its ad set and its ad with it; a follow-up list came back empty.

Some things this page does not claim to have tested: video ads, carousels, lifetime budgets, and any objective other than Traffic. Some campaign types are not buildable here at all — app-install optimization, the messaging `CONVERSATIONS` goal, catalog ads and Advantage+ Shopping. Check [what it cannot do](../06-reference/what-it-cannot-do.md) before you promise a client a campaign type, and [audiences and lookalikes](audiences-and-lookalikes.md) for the targeting limits (one OR-group of interests, no exclusions, no language targeting).

## Go deeper

- Read this campaign, ad set and ad back and confirm the targeting and creative match the brief.
- Show me the location types on this ad set — am I paying for visitors as well as residents?
- Look up the geolocation code for `<city or region>` so I can target it instead of the whole country.
- Build a second ad set under the same campaign, identical except for the age range, so I can compare.
- Show me the preview links for this ad so I can see it before it runs.

## Fields this uses

Reading and writing use different names for the same thing. The `targeting_*` names above are what you **send**; the fields below are what you **read**.

- [`facebook_ads_status`](../06-reference/all-fields.md) · [`facebook_ads_campaign_configured_status`](../06-reference/all-fields.md)
- [`facebook_ads_objective`](../06-reference/all-fields.md) · [`facebook_ads_buying_type`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_id`](../06-reference/all-fields.md) · [`facebook_ads_adset_id`](../06-reference/all-fields.md) · [`facebook_ads_ad_id`](../06-reference/all-fields.md)
- [`facebook_ads_adsettargeting_age_min`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_age_max`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_countries`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_type`](../06-reference/all-fields.md) — `geo_location_type` is where the widened location types show up
- [`facebook_ads_image_asset_hash`](../06-reference/all-fields.md) — see [upload creative](upload-creative.md)
- [`facebook_ads_adsetdaily_budget`](../06-reference/all-fields.md) · [`facebook_ads_bidamount`](../06-reference/all-fields.md) — and see [change budgets and bids](edit-budgets-and-bids.md) for which level a budget lands on

> [!WARNING]
> **You can read how the geo targeting works, but not where it points.** `facebook_ads_adsettargeting_geo_location_type` correctly returns the widened list — `home, recent` — so you can see Meta added visitors and recent travellers to your one country. But `facebook_ads_adsettargeting_geo_location_countries` comes back **empty** on ad sets that plainly have country targeting. Age fields populate fine, so it is that one field.
>
> An audit asking "which countries does this ad set target?" gets a blank and may conclude there is no geo targeting at all. To see the countries, read the ad set back through Meta rather than through reporting.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*