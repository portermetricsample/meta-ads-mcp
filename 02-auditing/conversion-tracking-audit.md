# Check the pixel is firing and you are counting the right thing

The dashboard says conversions are up, the client says the sales inbox is quiet, and one of you is reading a number that does not mean what it says.

## Ask this

```
Audit my Meta conversion tracking.

First, list the pixels and the custom conversions on this ad account.

Then, for the last 30 days, show me a table of every standard pixel
event with how many times it fired and its total value: purchases,
leads, add to cart, initiate checkout, complete registration,
view content, search, add payment info, add to wishlist, and custom.

Add a second column for the deduplicated version of each — people
rather than events.

Then show me the attribution setting on the account, and split
purchases by campaign so I can see which campaigns are reporting
conversions at all.
```

## What comes back

**The setup**

```
pixels               <id> · <name> · <status>
custom conversions   <id> · <name> · <rule>
```

**The events** — one row per standard event. Illustrative counts, real columns.

| Event | Times fired | People | Value |
|---|---|---|---|
| purchase | 214 | 198 | 41,300 |
| add to cart | 1,940 | 1,610 | 288,000 |
| initiate checkout | 640 | 590 | 96,400 |
| view content | 12,800 | 9,300 | — |
| lead | 0 | 0 | — |
| complete registration | 0 | 0 | — |
| add payment info | 0 | 0 | — |

**Attribution**

```
attribution_setting   <the window this account reports on>
```

## How to read it

Read the funnel downwards and look for the step that breaks. View content into add to cart into initiate checkout into purchase should each be a fraction of the one above it. A step that reports zero while the one below it reports sales is not a bad conversion rate — it is an event that is not installed.

A zero row is only a problem if that event should exist. A lead generation account with zero leads is broken; a shop with zero leads is normal. Say out loud which events this business is supposed to fire before you diagnose anything.

The value column is the other half of the check. Events firing with no value attached means you can count conversions but can never calculate return on ad spend, and every ROAS number in the account will read as zero or empty.

Compare times fired against people. A large gap is normal for add to cart and abnormal for purchase — if one buyer is counted as several purchases, revenue is inflated and cost per purchase is understated.

Finally, split purchases by campaign. If one campaign reports conversions and the rest report none, the pixel is fine and the problem is that only one campaign is optimising for it.

> [!NOTE]
> Meta's conversion counts do not travel through a generic cross-platform conversion field. In a query that spans Meta alongside Google or TikTok, the blended conversion column comes back as zero for Meta — the Meta rows are there, the conversions are not. Ask for the Meta-native conversion fields by name whenever Meta is in a multi-platform table.

## The trap

> [!WARNING]
> There is a field that answers "how many conversions did I get" and it is the wrong one. `facebook_ads_conversions_all` totals every action the account recorded — page engagements and video views land in the same number as purchases. It always looks healthy, it always looks like the pixel is working, and it is the single easiest way to report a broken account as a good one. Audit with the named events (`facebook_ads_offsite_conversion_fb_pixel_purchase`, `_lead`, and the rest) and never put the all-actions total in front of a client.

## Go deeper

- Show me purchases counted by pixel event against purchases counted across devices, side by side.
- Which of my ad sets are optimising for an event that has fired zero times in 30 days?
- Show me offline conversions and messaging conversations started, in case results are landing outside the website.
- Break purchases down by day for the last 30 days so I can see the day the tracking broke.
- List the custom conversions on this account and show which campaigns actually use them.

## Fields this uses

- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) and its nine siblings (`_lead`, `_add_to_cart`, `_initiate_checkout`, `_complete_registration`, `_view_content`, `_search`, `_add_payment_info`, `_add_to_wishlist`, `_custom`)
- [`facebook_ads_value_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) — the value twin of each event
- [`facebook_ads_omni_purchase`](../06-reference/all-fields.md) · [`facebook_ads_omni_add_to_cart`](../06-reference/all-fields.md) · [`facebook_ads_omni_initiated_checkout`](../06-reference/all-fields.md)
- [`facebook_ads_unique_action_purchase`](../06-reference/all-fields.md) · [`facebook_ads_unique_action_lead`](../06-reference/all-fields.md)
- [`facebook_ads_offline_conversion_purchase`](../06-reference/all-fields.md) · [`facebook_ads_offline_conversions_leads`](../06-reference/all-fields.md)
- [`facebook_ads_onsite_conversion_messaging_conversation_started_7d`](../06-reference/all-fields.md)
- [`facebook_ads_attribution_setting`](../06-reference/all-fields.md)
- Actions: `facebook_ads.pixel_list` · `facebook_ads.customconversion_list` — see [all-actions.md](../06-reference/all-actions.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
