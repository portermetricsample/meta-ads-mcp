# Limitations

Verified against the live connector. We publish this because knowing what a tool cannot do saves more time than another feature list.

> [!WARNING]
> **Bid strategy defaults to `LOWEST_COST_WITH_BID_CAP`** — confirmed by creating a campaign with no bid strategy and reading it back from Meta. It requires a bid amount to deliver, and it is not offered in the values you may set. Always pass `LOWEST_COST_WITHOUT_CAP` explicitly. Full explanation: [launch a campaign](../use-cases/ad-management/launch-a-campaign.md).

## Not exposed by this connector

| Capability | Status | Workaround |
|---|---|---|
| Dayparting / ad scheduling | ❌ not a parameter | Ads deliver continuously between start and end time |
| Language / locale targeting | ❌ | Use geo targeting |
| Interest AND-narrowing, behaviors, interest exclusions | ❌ single OR-group only | Broad targeting + geo |
| Messaging optimization (`CONVERSATIONS` goal) | ❌ | Point at WhatsApp/Messenger optimizing for `LINK_CLICKS` |
| Boost an existing organic post | ❌ no `object_story_id` | Build the ad from assets |
| Custom attribution window (`attribution_spec`) | ❌ | Ad sets use the account default |
| Catalog / Dynamic Product Ads | ❌ | Ads Manager |
| Advantage+ **Shopping** | ❌ | Removed by Meta from the API in v24 (subcode 2490568) — Ads Manager only. Not a connector gap. Advantage+ **App** still works, via `smart_promotion_type`. |
| App-install optimization goal | ❌ | Choose another objective |
| `facebook_ads_spend_cap`, `target_roas` | ❌ | Use `bid_strategy: MINIMUM_ROAS` + `bid_value` |
| Financial services special ad category | ❌ not in enum | Ads Manager |
| Delete an uploaded image or video | ❌ | Ads Manager |

## Supported — do not assume otherwise

Placements · custom audiences (customer-file **and** website/pixel-rule) · lookalikes · full campaign/ad set/ad CRUD · delete at every level · asset upload by URL **and** raw base64.

## Known gotchas


**`facebook_ads_amount_spent` is an account-level lifetime value.** For period spend use **`facebook_ads_spend`**.

**`facebook_ads_conversions_all` counts every action**, including page engagements and video views — not business conversions. For those use the specific fields (`facebook_ads_offsite_conversion_fb_pixel_purchase`, `facebook_ads_offsite_conversion_fb_pixel_lead`).

**Blended `conversions` does not cover Meta.** In a cross-platform query it returns 0 for Meta Ads. Use the Meta-native conversion fields.

**Advantage+ Audience must be set explicitly when you target by age.** `targeting_advantage_audience: 1` is incompatible with `age_max < 65` (subcode 1870189).

**History is capped at 37 months** by Meta's API, not by this connector.

---

*Catalog verified against the live Porter MCP on 2026-09-07.*
