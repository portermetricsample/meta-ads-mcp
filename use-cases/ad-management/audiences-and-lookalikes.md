# Build custom audiences and lookalikes

Retargeting has been running on one stale list for months, and you want a fresh website audience plus a lookalike built from your best customers.

> [!IMPORTANT]
> **This page has not been run end to end.** No audience and no lookalike has been created against a live ad account from this repo. The actions, the requirement that a lookalike carries a location, and the interest-targeting limits below are all real and checked against the connector — **but no response shape is documented here, because none has been seen.** Create one, read it back, and confirm it in Ads Manager before you attach it to anything that spends.

## Ask this

```
In my Meta ad account, do two things.
1. Create a website custom audience called "<audience name>" from my pixel:
   people who visited any page containing "<url fragment>" in the last 30 days.
2. Create a lookalike of my existing audience "<seed audience name>",
   for <country code>, at 1% similarity.
Then list my custom audiences and tell me which ad sets are using each one.
```

## What the connector offers

| Action | What it is for |
|---|---|
| `facebook_ads.customaudience_create` | Both seed types: a rule over website or pixel activity, **and** a customer file you supply |
| `facebook_ads.customaudience_add_users` | Push a CSV into an existing audience — hashing and normalisation happen server-side |
| `facebook_ads.customaudience_list` / `get` / `update` / `delete` | Read and manage what already exists |
| `facebook_ads.lookalike_create` | **Requires a location** — `country` or `location_countries`. A lookalike with no location is not a valid request |
| `facebook_ads.pixel_list` · `facebook_ads.customconversion_list` | Find the pixel and the conversions a rule can be built on |
| `facebook_ads.interest_search` | Look up interest terms before you name them in targeting |

If someone tells you the customer-file route is unavailable through this connector, they are wrong — [what it cannot do](../../reference/what-it-cannot-do.md) lists both seed types as supported.

## How to read it

**The seed decides everything about a lookalike.** A seed of your highest-value customers produces a different audience than a seed of everyone who ever loaded a page, even though both come back looking like an audience of a certain size. The percentage is a similarity setting, not a quality setting.

**A lookalike will not build without a location.** That is the one hard requirement documented on the action — decide the country before you ask.

**Check the audience in Ads Manager before you spend on it.** Size, readiness and match rate for a customer file are not things this page can tell you what to expect, because the responses have not been observed. A read-back plus a look at the account is the check.

> [!IMPORTANT]
> Uploading a customer list is a decision about other people's personal data, not a technical step. Use only contacts you are allowed to use for advertising, under whatever consent and privacy rules apply to you and your client, and get that confirmed by the person who owns the relationship before any file moves. If you are unsure, build the audience from website activity instead.

## The traps

> [!WARNING]
> **Interest targeting here is one OR-group and nothing else.** You can list interests and reach anyone matching any of them. You cannot narrow with AND, you cannot exclude an interest, and you cannot add behaviors — and language or locale targeting is not available at all. So an ad set you built in Ads Manager as "interested in running AND in nutrition, excluding existing customers, Spanish speakers only" cannot be rebuilt here. Do that narrowing with a custom audience and geo instead, or accept broader targeting than the brief describes.

> [!WARNING]
> **Your country targeting is quietly wider than you asked for.** This one was verified on a live ad set: a country was sent on its own, and Meta stored it alongside `location_types` of `frequently_in`, `home` and `recent` — none of which were sent. That means people who **recently visited or frequently travel to** the country, not only the people who live there. If your audience work assumes residents, that assumption is not what is running.

> [!WARNING]
> **The targeting parameter names do not mirror the ones you see on the way out.** Asking for `targeting_geo_location_countries` is rejected outright as an unrecognized parameter; the real name is **`targeting_countries`**. The connector takes flat `targeting_*` parameters and assembles Meta's nested structure itself, so the input name and the read-back name are deliberately different. Verified names in [launch a campaign](launch-a-campaign.md).

## Go deeper

- List my custom audiences with their type, newest first.
- Which ad sets are currently using the audience `<audience name>`?
- Add the contacts in this CSV to `<audience name>` and tell me how many rows were accepted.
- Show me my pixels and the custom conversions built on them.
- Create lookalikes of the same seed at 1%, 3% and 5% for `<country code>` so I can test reach against precision.

## Fields this uses

Audiences themselves are managed through the action catalog rather than the reporting fields — see [all-actions.md](../../reference/all-actions.md). The fields below are what you read once an audience is attached to an ad set:

- [`facebook_ads_adset_id`](../../reference/all-fields.md) · [`facebook_ads_adset_name`](../../reference/all-fields.md)
- [`facebook_ads_reach`](../../reference/all-fields.md) · [`facebook_ads_frequency`](../../reference/all-fields.md)
- [`facebook_ads_adsettargeting_geo_location_countries`](../../reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_cities`](../../reference/all-fields.md) · [`facebook_ads_adsettargeting_geo_location_type`](../../reference/all-fields.md) — `geo_location_type` is where the widened location types show up
- [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../../reference/all-fields.md) · [`facebook_ads_offsite_conversion_fb_pixel_lead`](../../reference/all-fields.md)

> [!WARNING]
> **You can read how the geo targeting works, but not where it points.** `facebook_ads_adsettargeting_geo_location_type` correctly returns the widened list — `home, recent` — so you can see Meta added visitors and recent travellers to your one country. But `facebook_ads_adsettargeting_geo_location_countries` comes back **empty** on ad sets that plainly have country targeting. Age fields populate fine, so it is that one field.
>
> An audit asking "which countries does this ad set target?" gets a blank and may conclude there is no geo targeting at all. To see the countries, read the ad set back through Meta rather than through reporting.
