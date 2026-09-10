# Tools — Meta Ads

Reads run through `query_data`. Everything else is in Porter's action catalog, reached with `list_actions` → `execute_action`.

## Reading

| Tool | What it does |
|---|---|
| `list_accounts` | Your Meta ad accounts, searchable by name or id |
| `list_fields` | The 1,205 metrics and 167 dimensions |
| `query_data` | Any metric × dimension × date range, **across several accounts and connectors in one call** |
| `create_blend` / `query_blend` | Save a recurring analysis |
| `create_report` | Hosted dashboard |

## Campaign structure — write

| Action | Notes |
|---|---|
| `facebook_ads.campaign_create` | PAUSED by default. **Pass `bid_strategy` explicitly** — see [what it cannot do](what-it-cannot-do.md) |
| `facebook_ads.campaign_update` | Name, status, budget, bid strategy, CBO↔ABO |
| `facebook_ads.campaign_delete` | Destructive; removes children |
| `facebook_ads.adset_create` | Flat `targeting_*` params assembled into Meta's nested spec |
| `facebook_ads.adset_update` / `adset_delete` | |
| `facebook_ads.ad_create` | Creative assembled inline from flat params |
| `facebook_ads.ad_update` / `ad_delete` | |
| `facebook_ads.campaign_list` / `adset_list` / `ad_list` | Includes `effective_status` filtering |

## Assets

| Action | Notes |
|---|---|
| `facebook_ads.image_upload` | Public URL **or** `image_base64` |
| `facebook_ads.video_upload` | Public URL **or** `video_base64` |

Base64 means an agent can upload a local file with no human in the loop.

## Audiences

| Action | Notes |
|---|---|
| `facebook_ads.customaudience_create` | Customer-file seed **and** website/pixel-rule audiences |
| `facebook_ads.customaudience_add_users` | CSV; hashing and normalization handled server-side |
| `facebook_ads.customaudience_list` / `get` / `update` / `delete` | |
| `facebook_ads.lookalike_create` | **Requires a location** — `country` or `location_countries` |

## Pixels and conversions

`facebook_ads.pixel_list` · `facebook_ads.customconversion_list`

## Targeting discovery

`facebook_ads.interest_search` · `facebook_ads.geolocation_search`

## Competitor research — no account access required

| Action | Notes |
|---|---|
| `meta_ads_research.run_audit` | Pulls a brand's live ads from Meta's public Ad Library by name; dedupes by media hash |
| `meta_ads_research.publish_report` | Turns that audit into a hosted report |
| `google_ads_research.run_search_audit` | Same idea against Google's Ads Transparency Center |
| `google_ads_research.run_serp_teardown` | Live SERP with real destination URLs |

These read public data, so they work on brands you have no relationship with.

## Insights

`facebook_ads.insights_get` — raw Graph insights with `breakdowns`, `filtering`, `level` and `time_range`, for anything `query_data` does not cover.

---

Porter's catalog runs to **750+ actions across 25+ connectors**. Search it with `list_actions(task="…")` before assuming something is missing.


---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
