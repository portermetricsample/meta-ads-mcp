# Tear down one competitor's creative

You have picked the one brand worth studying, and before your next creative brief you want to know what they actually say, how they say it, and in what shape.

## Ask this

```
Audit everything this brand has live on Meta right now, from the public Ad Library:
<competitor brand name>

Deduplicate first, so one creative running across many placements is one row.
Then for each unique creative tell me: the format, the hook — the first thing a
person sees or reads — and the angle, meaning the promise or problem it leads with.
Group the angles that repeat and rank the groups by how many creatives sit in each.
```

## What comes back

Two layers: the deduplicated creative list, then the groups on top of it. Every value below is invented as an illustration.

```
Unique creatives: 22   (deduplicated from 61 raw entries)

Angle group                       Creatives   Formats
<angle in the brand's own words>         9     video 8 · image 1
<angle in the brand's own words>         6     video 3 · image 3
<angle in the brand's own words>         4     image 4
<angle in the brand's own words>         3     video 3
```

<details><summary>The per-creative rows underneath (22 in this illustration)</summary>

```
#    Format   Hook                                   Angle group
1    video    "<first line on screen>"               <angle>
2    video    "<first line on screen>"               <angle>
3    image    "<headline in the image>"              <angle>
…
22   image    "<headline in the image>"              <angle>
```

</details>

## How to read it

**The gap between 61 and 22 is the placement tax.** Sixty-one raw entries collapsing to twenty-two unique creatives means the brand is buying breadth with a small set of ideas. Read the twenty-two; the sixty-one tells you nothing you can copy.

**The biggest angle group is their bet, not their best.** It is where they have put the most production budget, which is a statement of belief. You cannot see whether it works, so treat it as a hypothesis they are funding — worth testing against your own, not worth copying blind.

**A single angle carried in one format is fragile.** If nine of their creatives sit in one group and eight of those are video, they have never tested that promise as a static. That is a cheap experiment you can run before they do.

**The hooks are the reusable part.** Angles are tied to their product; the shape of a hook — a question, a number, a before-and-after, a face talking to camera — transfers to any product in the category.

## The trap

> [!WARNING]
> **Deduplication works on the media file, not on the idea.** Two creatives that look identical to you are counted separately if the brand re-exported or re-uploaded the video, because the file is different. So "22 unique creatives" is a ceiling, not a fact: the real number of distinct ideas is that number or lower, never higher. Eyeball the list before you quote the count to a client.

## Go deeper

- Which of their angles do I have no equivalent of in my own account?
- Write three hooks in the shape of their top group, for my product.
- Which formats are missing from their mix entirely?
- Show me only the creatives whose hook is a question.
- Publish this teardown as a hosted report with the creatives grouped by angle.

## Fields this uses

None. The teardown reads Meta's public Ad Library, so **no field in [../06-reference/all-fields.md](../06-reference/all-fields.md) is involved** — those describe an ad account you are connected to, and here you are connected to nothing. The action is `meta_ads_research.run_audit`, with `meta_ads_research.publish_report` for the hosted version: [../06-reference/all-actions.md](../06-reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
