---
name: meta-conversion-audit
description: Audit what a Meta (Facebook/Instagram) ad account is actually counting as a conversion, through the Porter Metrics MCP. Trigger when the user says the numbers look too good, the dashboard and the sales inbox disagree, asks whether the pixel is firing, wants a conversion tracking or pixel audit, or asks "are these conversions real". Encodes the field that reported three orders of magnitude more than the real one on the same row.
---

# Meta conversion audit

## The job

Find out which events are actually installed and firing, and whether the number being reported as "conversions" is a business result or a pile of video views.

## The steps

**1 — List the setup.** `facebook_ads.pixel_list` and `facebook_ads.customconversion_list`.

**2 — Pull the last 30 days, one row per standard pixel event**, each with how many times it fired and its total value:

`facebook_ads_offsite_conversion_fb_pixel_purchase` · `_lead` · `_add_to_cart` · `_add_to_wishlist` · `_initiate_checkout` · `_complete_registration` · `_search` · `_view_content` · `_add_payment_info` · `_custom`

Value twins are the same names prefixed `facebook_ads_value_` — `facebook_ads_value_offsite_conversion_fb_pixel_purchase`, and so on.

**3 — Add the deduplicated column**, people rather than events: `facebook_ads_unique_action_purchase`, `facebook_ads_unique_action_lead` and their siblings.

**4 — Add the sanity check:** `landing_page_views` (bare, no prefix) and `facebook_ads_spend` for the same window.

**5 — Add `facebook_ads_attribution_setting`**, then split the account's main conversion event by `facebook_ads_campaign_name`.

**6 — Read the funnel downwards and find the step that breaks.** View content → add to cart → initiate checkout → purchase should each be a fraction of the one above. A step reporting zero while the step below it reports sales is not a bad conversion rate — it is an event that is not installed.

## Trap checklist — check every one before reporting a verdict

- [ ] **Never report `facebook_ads_conversions_all` as conversions.** On one campaign, one 30-day window, one row, against a live account:

      facebook_ads_conversions_all                    251,980
      facebook_ads_offsite_conversion_fb_pixel_lead       103
      landing_page_views                                4,134
      facebook_ads_spend                               12,879

  Both of the first two lines are labelled conversions. Only the second one is. `conversions_all` totals every action recorded — video views, page likes, comments, profile taps — in the same number as a lead or a purchase. **Always name the event you want.** The giveaway is that it exceeds landing page views: nobody converted more times than they arrived.
- [ ] **`landing_page_views` was written bare.** It is a Porter blend field, not a Meta connector field. `facebook_ads_landing_page_view` fails with an unknown-field error rather than returning zero.
- [ ] **A zero row was judged against what the business should fire.** A lead-generation account with zero leads is broken; a shop with zero leads is normal. State which events this business is supposed to fire before diagnosing anything.
- [ ] **The value column was checked, not just the count.** Events firing with no value attached means ROAS can never be calculated and every return figure in the account will read as zero or empty.
- [ ] **Times fired was compared against people.** A large gap is normal for add to cart and abnormal for purchase — one buyer counted as several purchases inflates revenue and understates cost per purchase.
- [ ] **In any multi-platform query, Meta conversions were asked for by their Meta-native names.** The blended cross-connector conversion column returns 0 for Meta: the Meta rows are there, the conversions are not.
- [ ] **Rates in this audit were converted to percentages.** Every `*_ctr` field returns a decimal fraction — `0.0256` is 2.56%.
- [ ] **The window was inside 37 months.** Meta's API rejects anything earlier with `(#3018)`.

## Stop and ask the user

- This audit only reads. Turning off a campaign, changing an optimization event or editing a pixel is a separate decision — present the finding and let the user decide.
- Before writing "the pixel is broken" in anything client-facing, confirm with the user which events this business is supposed to fire. A missing event and an irrelevant event look identical in the data.
- Never publish an account id, a pixel id or a real spend figure into a shared document without asking.
