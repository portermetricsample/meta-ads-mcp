# Available fields — Meta Ads

**500 metrics and 167 dimensions.** Field names are namespaced: `facebook_ads_<name>`.

> [!WARNING]
> **A few fields break that rule and are written bare.** These are Porter *blend* fields, shared across connectors. `landing_page_views` is one — `facebook_ads_landing_page_view` is rejected outright. When a field name fails, read the error: it names the form that works. Get the live list with `list_fields(connector="facebook-ads")`.

## Delivery
`impressions` · `reach` · `frequency` · `spend` · `social_spend` · `full_view_impressions` · `full_view_reach`

> [!WARNING]
> Use **`facebook_ads_spend`** for period spend. `facebook_ads_amount_spent` is an account-level lifetime value — put it in a weekly report and the number will look wildly high and will not move with the date range.

## Clicks — four different numbers
| Field | What it counts |
|---|---|
| `clicks` | every click, including likes, comments, profile taps |
| `unique_clicks` | deduplicated people |
| `inline_link_clicks` | clicks to your destination |
| `unique_inline_link_clicks` | deduplicated link clickers |
| `outbound_click` | clicks that leave Meta |

> [!WARNING]
> These are five different counts of the same traffic, not five parts of a whole — never add them together. `clicks` is the widest because it includes likes, comments and profile taps, so a CPC built on it will always look cheaper than one built on `inline_link_clicks`. Pick one click field, pair it with its matching rate and cost field, and say in the report which one you used.

## Rates
`ctr` · `unique_ctr` · `inline_link_click_ctr` · `unique_inline_link_click_ctr` · `outbound_CTR` · `unique_outbound_CTR`

## Cost — ~60 variants

<details><summary>Show the common cost fields</summary>

`cpc` · `cpc_link` · `cpm` · `cpp` · `cost_per_inline_link_click` · `cost_per_unique_click` · `cost_per_unique_inline_link_click` · `cost_per_outbound_click` · `cost_per_thruplay` · `cost_per_purchase` · `cost_per_lead` · `cost_per_conversion` · `cost_per_unique_conversion` · `cost_per_action_type` · `cost_per_3s_video_view` · `cost_per_estimated_ad_recallers` · `cost_per_new_messaging_conversation` · …

</details>

## Conversions — all 10 pixel events, each with a value twin

<details><summary>Show the pixel events, value twins and omni fields</summary>

`offsite_conversion_fb_pixel_purchase` · `_lead` · `_add_to_cart` · `_add_to_wishlist` · `_initiate_checkout` · `_complete_registration` · `_search` · `_view_content` · `_add_payment_info` · `_custom`

Value twins: `value_offsite_conversion_fb_pixel_purchase`, and so on for each.

Omni (cross-device): `omni_purchase` · `omni_add_to_cart` · `omni_initiated_checkout` · `omni_complete_registration` · `omni_view_content` · `omni_search` · `omni_app_install`

</details>

> [!WARNING]
> `conversions_all` counts **every action**, including engagements — a video view or a page like lands in the same total as a purchase. Report it as a business result and you will overstate performance by a wide margin. For business conversions use the named fields.

## Unique — ~80 deduplicated variants
Every action above has a `unique_action_*` twin — `unique_action_purchase`, `unique_action_lead`, `unique_action_offsite_conversion_fb_pixel_purchase`, and so on. These count **people**, not events.

## ROAS
`purchase_roas_purchase` · `website_purchase_roas` · `mobile_app_purchase_roas` · `website_purchase_roas_perc`

## Video — including second-by-second retention

<details><summary>Show the video fields</summary>

`action_video_view` (3s) · `video_thruplay_watched_actions` · `video_p25/p50/p75/p95/p100_watched_actions` · `video_15_sec_watched_actions` · `video_30_sec_watched_actions` · `video_avg_time_watched_actions` · `unique_3s_video_view`

**`video_play_curve_second_0` … `second_60_more`** — 17 fields giving how many viewers were still watching at each second.

</details>

## Engagement
`action_post_engagement` · `action_page_engagement` · `comment` · `like` · `post` · `onsite_conversion_post_save` · `photo_view` · `instagram_profile_engagement`

## Messaging
`onsite_conversion_messaging_conversation_started_7d` · `onsite_conversion_messaging_first_reply` · `onsite_conversion_messaging_block` · `messaging_reply_rate` · `cost_per_new_messaging_conversation`

## Offline and store
`offline_conversion_purchase` · `offline_conversions_leads` · `offline_conversion_add_to_cart` · `store_visit_with_dwell` · plus action-value twins

## Budgets and account
`campaign_daily_budget` · `campaign_lifetime_budget` · `campaign_budget_remaining` · `adsetdaily_budget` · `spend_cap` · `balance` · `bidamount`

## Currency-converted spend
`spend_usd` · `spend_eur` · `spend_gbp` · `spend_sek`

---

# Dimensions — 167

## Breakdowns that split metrics

<details><summary>Show the breakdown dimensions</summary>

`publisher_platform` · `platform_position` · `device_platform` · `impression_device` · `age` · `gender` · `country_code` · `country_name` · `region` · `dma` · `hourly_stats_aggregated_by_advertiser_time_zone` · `hourly_stats_aggregated_by_audience_time_zone` · `action_type` · `product_id` · `place_page_id`

</details>

## Structure

<details><summary>Show the structure dimensions</summary>

`campaign_id` · `campaign_name` · `adset_id` · `adset_name` · `ad_id` · `ad_name` · `objective` · `buying_type` · `status` · `ad_status` · `adset_status` · `campaign_configured_status`

</details>

## Creative assets

<details><summary>Show the creative-asset dimensions</summary>

`image_asset` · `image_asset_id` · `image_asset_name` · `image_asset_hash` · `image_asset_url` · `image_thumbnail` · `video_asset` · `video_asset_thumbnail_url` · `body_asset` · `body_asset_text` · `title_asset_text` · `description_asset_text` · `call_to_action_asset_name` · `link_url_asset_website_url` · `ad_format_asset`

</details>

## Ad previews — nine surfaces
`ad_desktop_feed_preview_url` · `ad_mobile_feed_preview_url` · `ad_instagram_preview_url` · `ad_instagram_story_preview_url` · `ad_facebook_story_preview_url` · `ad_right_column_preview_url` · `ad_instant_article_preview_url` · `ad_mobile_banner_preview_url` · `ad_mobile_interstitial_preview_url`

## Carousel cards
`action_carousel_card_name` · `carousel_card_description` · `carousel_card_call_to_action_type` · `carousel_card_target_url` · `carousel_card_image_url` · `carousel_card_image_id`

## Promoted posts
`promoted_post_id` · `promoted_post_id_ig` · `promoted_post_message` · `promoted_post_caption` · `promoted_post_permalink_url` · `promoted_post_permalink_url_ig` · `promoted_post_picture` · `promoted_post_created_time` · `promoted_post_type`

## UTMs — parsed
`ad_utm_source` · `ad_utm_medium` · `ad_utm_campaign` · `ad_utm_content` · `ad_utm_term`

## Quality
`quality_ranking` · `engagement_rate_ranking` · `conversion_rate_ranking` · `auction_competitiveness` · `results_indicator` · `result_values_performance_indicator`

## Targeting read-back
`adsettargeting_age_min` · `adsettargeting_age_max` · `adsettargeting_geo_location_countries` · `adsettargeting_geo_location_cities` · `adsettargeting_geo_location_type`

## Lead forms
`lead_forms` · `lead_form_name` · `lead_platform` · `lead_is_organic` · `lead_field__id`

## Time

<details><summary>Show the time dimensions</summary>

`date` · `day` · `week` · `week_iso` · `month` · `quarter` · `year` · `year_month` · `year_week` · `year_week_iso` · `year_quarter` · `start_date` · `end_date`

</details>

## Account and business
`account_id` · `account_name` · `account_currency` · `account_status` · `business_name` · `business_country_code` · `business_city` · `timezone_name` · `timezone_offset_hours_utc` · `users`

## Attribution
`attribution_setting` · `campaign_is_skadnetwork_attribution`

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. Catalog verified against the live Porter MCP on 2026-09-07.*
