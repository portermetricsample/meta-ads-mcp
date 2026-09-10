# Build a swipe file for a whole category

You are starting on a new category — a new client, a new product line — and you need a folder of ideas worth stealing before you write a single brief.

> [!NOTE]
> A sweep multiplies the bill. Each brand is its own run at about **$0.02 per creative** for discovery, and more if you enrich. Five brands that turn up 96 unique creatives between them cost roughly **$1.92** at the discovery tier. Price list in [README.md](README.md).

## Ask this

```
Sweep the live Meta ads of these brands from the public Ad Library, one brand
at a time so nothing gets truncated. Discovery only — no transcripts, no frames
— until I say otherwise:

<brand 1>
<brand 2>
<brand 3>
<brand 4>
<brand 5>

For each brand, tell me which page you matched before you pull anything.
Deduplicate each brand's creatives by the media file. Then across all five,
group every creative by the hook shape it uses and keep only the shapes that
show up for more than one brand. For each shape give me the brands using it,
how many creatives use it, and two real examples of the copy.

Then publish the swipe file as a hosted report grouped by hook shape.
```

> [!TIP]
> Run one brand, look at what comes back, then decide whether the other four are worth paying for. You usually find after the first brand that two names on your list were not competitors at all — and at that point you have spent cents, not a sweep.

## What comes back

One row per hook shape that more than one brand uses, then a URL from `publish_report`. Illustrative values only — the brands, counts and copy below are invented.

```
Brands swept              5
Unique creatives         96   (deduplicated within each brand)
```

| Hook shape | Brands using it | Creatives | Example copy |
|---|---|---|---|
| `<shape, e.g. a question>` | 4 of 5 | 23 | "`<line>`" · "`<line>`" |
| `<shape>` | 3 of 5 | 11 | "`<line>`" · "`<line>`" |
| `<shape>` | 2 of 5 | 7 | "`<line>`" · "`<line>`" |

Plus the discards: shapes used by exactly one brand, kept in a separate list.

## How to read it

**Four of five brands doing the same thing is the category convention.** That is the thing every new entrant is measured against — you either meet it or you deliberately break it, but you should not stumble into it by accident.

**The one-brand shapes are the interesting half.** A shape nobody else uses is either an idea the category has not found yet or one it has already tried and dropped. You cannot tell which from live ads alone, so treat it as a cheap test, not as a plan.

**Count brands before you count creatives.** Twenty-three creatives from four brands is a convention. Twenty-three creatives from one brand is one company's habit, and it dressed up as a trend because it out-produced everyone else.

**Deduplication is per brand, because each brand is a separate run.** If three of your five brands run the same stock footage or the same agency template, it survives as three creatives and inflates whichever shape it belongs to. Sibling brands under one parent are the usual culprit — check the examples come from genuinely different companies before you call something a convention.

**Keep the copy, not the ad.** What goes in the swipe file is the shape and the line. The finished creative belongs to them; the structure is what you brief.

## The trap

> [!WARNING]
> **`active_only` is on by default, so every test a brand killed is invisible.** You are looking at survivors. That is genuinely useful — a shape running across four brands has been kept by four different teams — but it means the swipe file cannot tell you what the category tried and abandoned, and the shapes you never see may be the ones that failed rather than the ones nobody thought of. Worse, it quietly flatters the winners: a brand that tested forty angles and kept two looks, from out here, exactly like a brand that only ever had two. If you want the graveyard, that is a separate run with `active_only` turned off, and a separate bill.

## Go deeper

- Add two more brands to the sweep and tell me if the ranking of shapes changes.
- Re-run the two most interesting brands with `active_only` off and show me what they stopped running.
- Which shapes does my own account use, and which of these am I missing?
- Show me only the shapes that no brand in this list uses — the open space.
- Write one hook per shape for my product, keeping their structure and none of their words.

## Fields this uses

None. A swipe-file sweep is built entirely from Meta's public Ad Library, so it touches **no field in [../../reference/all-fields.md](../../reference/all-fields.md)** — nothing here requires an account, a permission or a token. The research variables it does return are `variants_total`, `days_active` and `any_active`; there are no performance metrics of any kind. It runs `meta_ads_research.run_audit` once per brand, `meta_ads_research.view_creative` on anything you want to look at, and `meta_ads_research.publish_report` for the shareable version: [../../reference/all-actions.md](../../reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
