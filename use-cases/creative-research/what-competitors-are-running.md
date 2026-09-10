# See what a competitor is running on Meta right now

A prospect asks how they stack up against the loudest brand in their category, and you have no access to that brand's ad account — only its name.

> [!NOTE]
> This is a paid run — about **$0.02 per creative** for a plain list like this one. A verified run on a public brand billed **$0.16**. The full price list is in [README.md](README.md).

## Ask this

```
Pull the ads this brand is running on Meta right now from the public Ad Library:
<competitor brand name>          (or paste the Ad Library URL, which is safer)

Deduplicate by the media file, so one creative running as many ads is one row.
Give me a table with the format, the first line of the ad copy, how many ads
carry that creative and how long it has been live. Tell me the raw ad count and
the unique creative count separately, and tell me if the pull hit its cap.

Before anything else, tell me which page you matched and how confident you are.
Then publish it as a hosted report and give me the link.
```

## What comes back

Three stages, in this order. Values below are invented as an illustration except where marked; the shape is what matters.

**1. The match, first.**

```
Matched page      <Brand Name>   page_id <numeric id>
confidence        0.4            recommendation: ask user to choose
```

**2. The deduplicated list.** `run_audit` hashes the media bytes, so the same file running under a hundred signed links is one row.

```
Raw ads pulled          40    (cap reached — brand likely has more)
Unique creatives         8

#   Format   Opening line of copy               Ads carrying it   Days live
1   video    "<first line of the ad copy>"                  38          140
2   video    "<first line of the ad copy>"                   6           63
3   image    "<first line of the ad copy>"                   4           21
…
```

The 40 → 8 collapse and the 38-ad creative are both real, from a verified run. They are not two halves of one sum — the pull was capped at 40, so do not subtract one from the other.

**3. The published report.** `publish_report` returns a URL. That is the deliverable; the table above is working material.

> [!NOTE]
> Not every brand exposes the same detail in the Ad Library, so some columns come back thinner for one brand than another. Ask for what you want and take what arrives — the run does not fail because one field is missing.

## How to read it

**Read the collapse, not the count.** Forty ads becoming eight creatives is the finding. It means the brand is buying breadth with a small set of ideas, and it means anyone quoting "40 ads" — including their own team — is describing their media buying, not their creative output.

**One creative on 38 ads is a conviction, not a result.** `variants_total` says how many ads carry that file. A brand does not spread one creative across dozens of ads by accident; it does that to a creative it believes in. You cannot see whether the belief is correct, because there is no performance data anywhere in this flow ([README.md](README.md)).

**`days_active` is the closest thing to a scoreboard.** Something live for 140 days has survived 140 days of someone looking at a dashboard you cannot see. It is weak evidence and it is the best you have. Pair it with `variants_total`: long-lived *and* widely duplicated is the strongest signal in the whole run.

**Treat the raw count as a floor.** `max_items` caps quietly — 40 requested, 40 returned, with a note that the brand likely has more. Nothing errors. If you need the real library size, raise the cap and pay for it.

## The trap

> [!WARNING]
> **A weak brand match does not stop the run.** In a verified run the action auto-confirmed a brand at `confidence: 0.4` while its own recommendation was to ask the user to choose. It then scraped, billed, and would happily have published — all against a page nobody checked. Anything with a common word in the name, a franchise, a regional arm, or a bigger namesake in another country is a coin flip. Ask for the matched page name and id in the same breath as the audit, and when it is at all ambiguous pass `page_id` or the Ad Library URL instead of typing the brand name.

## Go deeper

- Do the same for the two brands closest to this one and put the three unique-creative counts side by side.
- Split their unique creatives by format and tell me which format they are betting on.
- Show me the frames and the transcript of their longest-running creative.
- Group their ad copy into themes and name each theme in one sentence.
- Which of their live creatives mention a price, a discount or a guarantee?

## Fields this uses

None. This reads Meta's public Ad Library, so it uses **no field from [../../reference/all-fields.md](../../reference/all-fields.md)** — those are account fields and start applying only once an account is connected. What the audit returns instead are research variables: `variants_total`, `days_active` and `any_active`, plus `metrics_available`, which is always `false`. The actions are `meta_ads_research.run_audit`, `meta_ads_research.view_creative` and `meta_ads_research.publish_report`, listed in [../../reference/all-actions.md](../../reference/all-actions.md).
