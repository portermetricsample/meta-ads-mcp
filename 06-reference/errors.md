# Troubleshooting

Real errors, verbatim, with the fix.

## `Advantage Audience Flag Required` (subcode 1870227)
> To create your ad set, you need to enable or disable the Advantage audience feature.

Set `targeting_advantage_audience` explicitly — `0` for manual targeting, `1` for Advantage+.
**If you set `targeting_age_max` below 65, it must be `0`** — `1` with an age cap triggers subcode 1870189, which cannot be fixed after creation.

## `Bid Amount Required For The Bid Strategy Provided` (subcode 1815857)
The parent campaign is on `LOWEST_COST_WITH_BID_CAP`. Either supply `bid_value`, or set the campaign to `LOWEST_COST_WITHOUT_CAP`.

## `Performance goal isn't available` (subcode 2490408)
The `optimization_goal` is not valid for the campaign objective. `OUTCOME_TRAFFIC` accepts `LINK_CLICKS`, `LANDING_PAGE_VIEWS`, `IMPRESSIONS`, `REACH`, `POST_ENGAGEMENT`, `OFFSITE_CONVERSIONS`, `THRUPLAY`.

## `Budget Is Too Small` (subcode 2446375)
Below the account minimum for its currency. COP accounts: 3,076/day. USD: 100/day. INR: 9,615/day.

## `amount … converts to … over 5000x the account daily minimum`
A guardrail, not a bug. Re-check the number; if intentional, pass `confirm_large_budget: true`.

## `(#3018) The start date of the time range cannot be beyond 37 months`
Meta's retention limit. Narrow the date range.

## `(#2654) Missing Locations in Lookalike Spec`
`lookalike_create` requires a location. Pass `country: "US"` or `location_countries: ["US","CA"]`.

## `Missing Locations` on a valid lookalike
The seed audience is likely below Meta's minimum size (~100 people). Grow the seed.

## `the URL served a web page, not the file`
A Google Drive or Dropbox **share** link returns HTML, not media. Use a direct-download URL, or pass the bytes as `image_base64` / `video_base64`.

## `Unknown field(s) absent from every loaded schema`
Field names are namespaced. Use `list_fields(connector="facebook-ads")` — it is `facebook_ads_impressions`, not `impressions`.

## Query returns 0 rows but the account has spend
Try the widest legal window before concluding the account is empty, and drop dimensions to test the aggregate. A `data_freshness` block with `row_count: 0` means *unknown*, not *zero*.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. Catalog verified against the live Porter MCP on 2026-09-07.*
