# Build custom audiences and lookalikes

Retargeting has been running on one stale list for months, and you want a fresh website audience plus a lookalike built from your best customers.

## Ask this

```
In my Meta ad account, do two things.
1. Create a website custom audience called "<audience name>" from my pixel: 
   people who visited any page containing "<url fragment>" in the last 30 days.
2. Create a lookalike of my existing audience "<seed audience name>", 
   for <country code>, at 1% similarity.
Then list my custom audiences with their size and when they were last updated.
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

A new rule-based audience starts empty and fills as people match the rule, so "size 0" right after creation is normal. A lookalike also needs time before it is usable.

The seed decides everything about a lookalike. A seed of your highest-value customers produces a different audience than a seed of everyone who ever loaded a page, even though both are the same size on screen.

Two seed types are supported: a rule over website or pixel activity, and a customer file you supply. For a customer file, rows are hashed and normalized on the server before they reach Meta — you do not prepare the hashing yourself.

> [!IMPORTANT]
> Uploading a customer list is a decision about other people's personal data, not a technical step. Use only contacts you are allowed to use for advertising, under whatever consent and privacy rules apply to you and your client, and get that confirmed by the person who owns the relationship before any file moves. If you are unsure, build the audience from website activity instead.

## The trap

> [!WARNING]
> **A lookalike will not be created without a location.** Name the country — or the list of countries — in the same sentence, or the request comes back with a missing-locations error. Worse: that same missing-locations error also appears when the location *was* supplied correctly, and the real cause is a seed audience below Meta's minimum of roughly 100 people. Check the seed's size before you go hunting for a typo in the country code.

## Go deeper

- List my custom audiences with size, type and last update, newest first.
- Which ad sets are currently using the audience `<audience name>`?
- Add the contacts in this CSV to `<audience name>` and tell me how many rows were accepted.
- Show me my pixels and the custom conversions built on them.
- Create lookalikes of the same seed at 1%, 3% and 5% for `<country code>` so I can test reach against precision.

## Fields this uses

Audiences themselves are managed through the action catalog rather than the reporting fields — see [all-actions.md](../06-reference/all-actions.md). The fields below are what you read once an audience is attached to an ad set:

- [`facebook_ads_adset_id`](../06-reference/all-fields.md) · [`facebook_ads_adset_name`](../06-reference/all-fields.md)
- [`facebook_ads_reach`](../06-reference/all-fields.md) · [`facebook_ads_frequency`](../06-reference/all-fields.md)
- [`facebook_ads_adsettargeting_geo_location_countries`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md) · [`facebook_ads_offsite_conversion_fb_pixel_lead`](../06-reference/all-fields.md)

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
