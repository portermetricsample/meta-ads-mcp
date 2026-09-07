# Build custom audiences and lookalikes

Retargeting has been running on one stale list for months, and you want a fresh website audience plus a lookalike built from your best customers.

## Ask this

```
In my Meta ad account, do two things.
1. Create a website custom audience called "<audience name>" from my pixel:
   people who visited any page containing "<url fragment>" in the last 30 days.
2. Create a lookalike of my existing audience "<seed audience name>",
   for <country code>, at 1% similarity.
Then list my custom audiences and tell me which ad sets are using each one.
```

## What comes back

An id per audience created, then the account's audience list. Values below are illustrative.

```
custom audience   120250000000000021   website rule · 30 days
lookalike         120250000000000022   seed "<seed audience name>" · CO · 1%
```

| Audience | Type | Approximate size | Ready to use |
|---|---|---|---|
| `<audience name>` | website rule | filling | not yet |
| `<seed audience name>` | customer file | 4,100 | yes |
| `<lookalike name>` | lookalike | 210,000 | yes |

## How to read it

A rule-based audience starts empty and fills as people match the rule, so an audience with nothing in it right after creation is expected rather than broken.

The seed decides everything about a lookalike. A seed of your highest-value customers produces a different audience than a seed of everyone who ever loaded a page, even though both look the same size on screen.

Two seed types are supported: a rule over website or pixel activity, and a customer file you supply. Both work through this connector — if someone tells you the customer-file route is unavailable, check [what it cannot do](../06-reference/what-it-cannot-do.md), which lists it as supported.

> [!IMPORTANT]
> Uploading a customer list is a decision about other people's personal data, not a technical step. Use only contacts you are allowed to use for advertising, under whatever consent and privacy rules apply to you and your client, and get that confirmed by the person who owns the relationship before any file moves. If you are unsure, build the audience from website activity instead.

## The trap

> [!WARNING]
> **Interest targeting here is one OR-group and nothing else.** You can list interests and reach anyone matching any of them. You cannot narrow with AND, you cannot exclude an interest, and you cannot add behaviors — and language or locale targeting is not available at all. So an ad set you built in Ads Manager as "interested in running AND in nutrition, excluding existing customers, Spanish speakers only" cannot be rebuilt here. Do that narrowing with a custom audience and geo instead, or accept broader targeting than the brief describes.

## Go deeper

- List my custom audiences with their type, newest first.
- Which ad sets are currently using the audience `<audience name>`?
- Add the contacts in this CSV to `<audience name>` and tell me how many rows were accepted.
- Show me my pixels and the custom conversions built on them.
- Create lookalikes of the same seed at 1%, 3% and 5% for `<country code>` so I can test reach against precision.

## Fields this uses

Audiences themselves are managed through the action catalog rather than the reporting fields — see [all-actions.md](../06-reference/all-actions.md). The fields below are what you read once an audience is attached to an ad set:

- [`facebook_ads_adset_id`](../06-reference/all-fields.md) · [`facebook_ads_adset_name`](../06-reference/all-fields.md)
- [`facebook_ads_reach`](../06-reference/all-fields.md) · [`facebook_ads_frequency`](../06-reference/all-fields.md)
- [`facebook_ads_adsettargeting_geo_location_countries`](../06-reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_cities`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) · [`facebook_ads_offsite_conversion_fb_pixel_lead`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
