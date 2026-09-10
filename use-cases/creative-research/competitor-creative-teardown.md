# Tear down one competitor's creative

You have picked the one brand worth studying, and before your next creative brief you want to know what they actually say, how they say it, and in what shape.

> [!NOTE]
> This is the expensive version of a research run: reading the creatives means transcripts and frames, which bill at **$0.08 and $0.10 per creative** instead of $0.02. Pick the six to eight you will actually write up before you enrich anything. Price list in [README.md](README.md).

## Ask this

```
Audit everything this brand has live on Meta right now, from the public Ad Library:
<competitor brand name>          (or paste the Ad Library URL)

Deduplicate by the media file first, so one creative running as many ads is one row.
Then pick the six to eight creatives worth reading — mix the longest-running with
the newest — and open each one: give me the frames, the transcript, the headline
and the on-image text.

For each of those tell me the format, the hook (the first thing a person sees or
reads) and the angle (the promise or problem it leads with). Group the angles that
repeat and rank the groups by how many creatives sit in each. Then publish it as a
hosted report and give me the link.
```

## What comes back

Three stages: the deduplicated list, then the creatives you opened, then a URL. Every value below is invented as an illustration.

**1. The audit.** One row per unique creative — deduplication by media bytes is explained in [what-competitors-are-running.md](what-competitors-are-running.md).

```
Raw ads pulled          60    (cap reached)
Unique creatives        18

Angle group                       Creatives   Formats
<angle in the brand's own words>          7    video 6 · image 1
<angle in the brand's own words>          5    video 3 · image 2
<angle in the brand's own words>          4    image 4
<angle in the brand's own words>          2    video 2
```

**2. The creatives you opened.** `view_creative` returns the frames as pictures plus the transcript, one creative at a time. This is the only step where anyone actually sees the ad.

<details><summary>The per-creative rows underneath (18 in this illustration)</summary>

```
#    Format   Hook                                   Angle group        Ads   Days
1    video    "<first line spoken or on screen>"     <angle>             14    112
2    video    "<first line spoken or on screen>"     <angle>              9     87
3    image    "<headline in the image>"              <angle>              5     34
…
18   image    "{{product.name}}"                     <catalog>            3      9
```

</details>

**3. The published report.** `publish_report` returns the link you send. The tables above are working material, not the deliverable.

## How to read it

**Do not read the gap between raw ads and unique creatives as a measurement.** The pull was capped, so the raw number is a ceiling you set, not a count of what the brand runs. What the collapse does tell you is that one idea is being bought across many placements.

**The biggest angle group is their bet, not their best.** It is where the production budget went, which is a statement of belief. There is no CTR, no conversion and no engagement anywhere in this flow to tell you whether the belief paid off ([README.md](README.md)), so treat the biggest group as a funded hypothesis — worth testing against your own, not worth copying blind.

**A headline reading `{{product.name}}` is a catalog campaign.** Dynamic ads come back with the placeholder unrendered, exactly like that. It is not a bug in the pull and it is not a typo on their side: it is how you spot, from the outside, that a brand is running product-feed creative rather than hand-made ads. Read those rows as inventory, not as messaging.

**A single angle carried in one format is fragile.** If seven creatives sit in one group and six of those are video, they have never tested that promise as a static. That is a cheap experiment you can run before they do.

**The hooks are the reusable part.** Angles are tied to their product; the shape of a hook — a question, a number, a before-and-after, a face talking to camera — transfers to any product in the category.

## The trap

> [!WARNING]
> **`platforms` is eligibility, not delivery — there is no Instagram-versus-Facebook split in here.** The field lists where an ad is *allowed* to appear, which is close to "all of them" for most advertisers, and the run's own limitation text says it cannot answer that question. So a creative marked for Instagram and Facebook may have spent its entire life on one of them, and you have no way to tell which. If a teardown you write says "they are 70% Instagram", delete the sentence — it is not a soft estimate, it is a number that does not exist. Where a placement split matters, you need a connected ad account and the placement breakdown described in [../../reference/all-fields.md](../../reference/all-fields.md), on your own ads, not theirs.

## Go deeper

- Which of their angles do I have no equivalent of in my own account?
- Write three hooks in the shape of their top group, for my product.
- Open their three newest creatives and tell me what changed versus the long-runners.
- Which formats are missing from their mix entirely?
- Show me only the creatives whose hook is a question.

## Fields this uses

None. The teardown reads Meta's public Ad Library, so **no field in [../../reference/all-fields.md](../../reference/all-fields.md) is involved** — those describe an ad account you are connected to, and here you are connected to nothing. What the audit returns instead are research variables: `variants_total`, `days_active`, `any_active` and `platforms`, the last of which is eligibility only. The actions are `meta_ads_research.run_audit`, `meta_ads_research.view_creative` and `meta_ads_research.publish_report`: [../../reference/all-actions.md](../../reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
