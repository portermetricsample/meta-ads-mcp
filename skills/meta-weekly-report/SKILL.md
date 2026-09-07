---
name: meta-weekly-report
description: Pull last week's or last month's Meta (Facebook/Instagram) Ads numbers by campaign through the Porter Metrics MCP, with the prior period beside it. Trigger when the user asks for a weekly or monthly Meta report, "last week by campaign", a client update on Facebook or Instagram ads, or a period-over-period comparison of spend, clicks, CTR or cost per click. Encodes the fields that quietly mean something else and the rates that are wrong by 100x if pasted raw.
---

# Meta weekly or monthly report

## The job

One row per campaign for the period, the same campaigns for the period before, and a change column. Reads run through `query_data`.

## The steps

**1 — Pick the account.** `list_accounts` if the user has more than one.

**2 — Query the period, broken down by `facebook_ads_campaign_name`.** Ask for:

- `facebook_ads_spend`
- `facebook_ads_impressions`
- `facebook_ads_inline_link_clicks`
- `facebook_ads_inline_link_click_ctr`
- `facebook_ads_cost_per_inline_link_click`
- `facebook_ads_offsite_conversion_fb_pixel_purchase` (or `_lead`, whichever the business actually runs on)

**3 — Query the prior period the same way**, then compute the change per campaign.

**4 — Convert every rate to a percentage before showing anyone**, and say in the report that you did. Sort by spend, highest first.

**5 — Read it in order:** spend says where the money went, cost per link click says what happened to the price of traffic, purchases say whether the traffic was worth buying.

## Trap checklist — check every one before sending the report

- [ ] **Every rate was multiplied by 100.** Rates come back as decimal fractions. A link CTR of **2.56%** arrives as `0.025567691511131932` — verified on a live account. Applies to `facebook_ads_ctr`, `facebook_ads_inline_link_click_ctr`, `facebook_ads_unique_ctr`, `facebook_ads_outbound_CTR` and every other `*_ctr` field. Pasted raw it reads as a catastrophe; passed to a spreadsheet that already formats percentages it reads as a rounding error.
- [ ] **Spend came from `facebook_ads_spend`, not `facebook_ads_amount_spent`.** `amount_spent` is an account-level lifetime value — it looks wildly high and does not move when you change the date range.
- [ ] **One click field was chosen, named in the report, and paired with its own rate and cost field.** The connector exposes several counts of the same traffic:
  - `facebook_ads_clicks` — every click, including likes, comments and profile taps. The widest. A CPC built on it always looks cheaper than the truth.
  - `facebook_ads_unique_clicks` — deduplicated people.
  - **`facebook_ads_inline_link_clicks` — clicks to your destination. This is traffic. Use this one unless the user asks otherwise.**
  - `facebook_ads_unique_inline_link_clicks` — deduplicated link clickers.
  - `facebook_ads_outbound_click` — clicks that leave Meta.

  These are different counts of the same thing, not parts of a whole. Never add them together.
- [ ] **Reach was not summed across rows and frequency was not totalled.** (Meta platform behaviour, not something measured here.) Reach counts people and deduplicates, so four weekly reach numbers do not add up to the month — query reach over the exact period being reported. Frequency is an average, so it has no total either.
- [ ] **The time dimension is `facebook_ads_year_week`, not `facebook_ads_week`.** `week` returns a bare ISO week number with no year (`31`), so any range crossing a year sorts wrong.
- [ ] **A campaign showing enormous growth was checked for a start date.** A campaign switched on mid-period is not a win.
- [ ] **Cost fields were trusted as-is.** `cost_per_inline_link_click` matches spend ÷ clicks out to six decimal places, with no client-side rounding. If a cost number looks wrong, the click field underneath it changed — the arithmetic did not.
- [ ] **If a field name errors, the error was read.** Most Meta fields are prefixed `facebook_ads_`, but Porter blend fields are bare — `landing_page_views` is one, and `facebook_ads_landing_page_view` fails outright. The error message names the form that works. `list_fields(connector="facebook-ads")` gives the live list.

## Stop and ask the user

- This skill only reads. If the conversation turns to changing a budget, pausing a campaign or launching anything, stop and confirm with the user first — a report is never a mandate to act.
- Ask which conversion event the business runs on before you put a "conversions" column in a client-facing report. Do not guess, and do not use the all-actions total (see the `meta-conversion-audit` skill).
- History is capped at 37 months by Meta's API. A start date beyond that errors with `(#3018)`.
