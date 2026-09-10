---
name: meta-launch-campaign
description: Build a paused Meta (Facebook/Instagram) campaign, ad set and ad end to end through the Porter Metrics MCP. Trigger when the user asks to launch, build, create or set up a Meta or Facebook or Instagram campaign, ad set or ad, or says "get this creative live". Encodes the write parameters that are rejected under their obvious names, the bid strategy you get when you say nothing, and the geo targeting Meta widens on its own.
---

# Launch a Meta campaign

## The job

Four calls in a fixed order, each depending on the one before: **campaign → ad set → image upload → ad**. Everything is created PAUSED. You build it, read it back, show the user, and stop.

## Before you start

Collect from the user: objective, daily budget, country or countries, age range, platforms, the image URL, headline, body text, button, and the destination link. If the `page_id` is not known, get it from `facebook_ads.page_list`. Confirm which ad account with `list_accounts`.

## The steps

**1 — `facebook_ads.campaign_create`**

Always send all four of these, even when the user did not mention them:

- `bid_strategy: "LOWEST_COST_WITHOUT_CAP"` — never leave it out. See trap 1.
- `special_ad_categories: ["NONE"]` — an array, required. Not `[]`, not the bare string `NONE`.
- `daily_budget_amount` — the number the user said out loud. 5 means 5.00 in the account's currency.
- `is_adset_budget_sharing_enabled` — on or off, but always sent.

The valid `bid_strategy` values are `LOWEST_COST_WITHOUT_CAP`, `COST_CAP`, `BID_CAP` and `MINIMUM_ROAS`. `confirm_large_budget` guards budgets over 5000x the account minimum.

**2 — `facebook_ads.adset_create`**

The targeting parameters are flat `targeting_*` names and do not mirror Meta's own field names. Verified working: `targeting_countries`, `targeting_age_min`, `targeting_age_max`, `targeting_advantage_audience`, `targeting_publisher_platforms`.

`targeting_geo_location_countries` is rejected as an unrecognized parameter. Do not use it.

If `targeting_age_max` is below 65, `targeting_advantage_audience` must be off — the combination is rejected with subcode 1870189.

**3 — `facebook_ads.image_upload`**

Takes a public URL or `image_base64`. The response is keyed by file name, taken from the last segment of the URL — a URL ending `/1200/628` returns a key `628.jpg`. Read the first entry under `images` and take its hash. Never hardcode the key.

**4 — `facebook_ads.ad_create`**

`headline` (not `title`), `link`, `page_id`, `cta_type`. `LEARN_MORE` is a valid `cta_type`; `GET_STARTED` is rejected on this connector.

**5 — Read it back**

List the campaign, ad set and ad as stored, and show the user body, headline, image, button, budget, age range and the ad set's `location_types`. Three ids means the chain linked. Fewer means it broke at the first missing level and nothing below it exists.

## Trap checklist — check every one before reporting success

- [ ] **Bid strategy was sent explicitly.** Create a campaign without naming one and Meta stores `LOWEST_COST_WITH_BID_CAP` — verified by creating a real campaign and reading it back. That value is not in the list you are allowed to choose from, it needs a bid amount nobody asked you for, and without one the campaign looks correct and cannot deliver.
- [ ] **The geo targeting was widened and the user knows.** `targeting_countries: ["US"]` went in; `location_types: ["frequently_in", "home", "recent"]` came back. Two of those are not residents — people who recently visited and people who frequently travel to the country. It was never sent. Say this out loud whenever the offer is local.
- [ ] **`targeting_countries`, never `targeting_geo_location_countries`.**
- [ ] **`headline`, never `title`.** `title` is dropped silently: no error, no headline.
- [ ] **`link` was sent** — it is required even when the destination is inside the app.
- [ ] **`special_ad_categories: ["NONE"]` was sent.** It reads back as `[]`. That is normal, not a missing declaration.
- [ ] **`is_adset_budget_sharing_enabled` was sent.** Facebook rejects the request when it is omitted.
- [ ] **`daily_budget_amount` was not multiplied by 100.** Sending 5 stored `daily_budget: "500"` — Meta converts server-side. Multiplying yourself overcharges by 100x.
- [ ] **`budget_remaining` was not presented as pacing.** On a campaign that has never delivered it equals the daily budget. It is today's allowance, not the flight's balance.
- [ ] **A blank budget on the ad set was not read as zero.** `daily_budget` and `bid_strategy` are simply absent from the ad set when the budget lives on the campaign.

## Stop and ask the user

- **Never activate anything.** Everything ships PAUSED. Turning a campaign, ad set or ad on is a separate, explicit instruction from the user — never a step in this build.
- **Confirm the budget number back to the user before creating the campaign**, in the account's currency.
- **Ask before deleting anything.** Deleting a campaign cascades — its ad set and ad go with it.
- If a create fails with `failed to resolve credentials` (HTTP 401), stop. That account's Meta connection needs reconnecting; it is not a parameter problem and there is nothing to retry around.

## Not buildable here

App-install optimization, the messaging `CONVERSATIONS` goal, catalog / dynamic product ads, and Advantage+ Shopping (removed by Meta from the API in v24, subcode 2490568). Advantage+ App still works via `smart_promotion_type`. Also unavailable: dayparting, language targeting, interest exclusions, boosting an existing organic post, and custom attribution windows. Say so rather than improvising a workaround.

Only the Traffic objective with an image ad was tested end to end. Video, carousel and lifetime budgets follow the same shape but were not verified — tell the user when you are on untested ground.
