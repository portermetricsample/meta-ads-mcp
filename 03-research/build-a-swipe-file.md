# Build a swipe file for a whole category

You are starting on a new category — a new client, a new product line — and you need a folder of ideas worth stealing before you write a single brief.

## Ask this

```
Sweep the live Meta ads of these brands from the public Ad Library, one brand
at a time so nothing gets truncated:

<brand 1>
<brand 2>
<brand 3>
<brand 4>
<brand 5>

Deduplicate each brand's creatives. Then across all five, group every creative
by the hook shape it uses, and keep only the shapes that show up for more than
one brand. For each shape give me the brands using it, how many creatives use
it, and two real examples of the copy.
```

> [!TIP]
> Ask for a short list from each brand first, look at what comes back, then re-run the ones worth the full pull. A five-brand sweep asked for in one breath is slow, and you usually find after the first brand that two names on your list were not competitors at all.

## What comes back

One row per hook shape that more than one brand uses. Illustrative values only — the brands, counts and copy below are invented.

| Hook shape | Brands using it | Creatives | Example copy |
|---|---|---|---|
| `<shape, e.g. a question>` | 4 of 5 | 23 | "`<line>`" · "`<line>`" |
| `<shape>` | 3 of 5 | 11 | "`<line>`" · "`<line>`" |
| `<shape>` | 2 of 5 | 7 | "`<line>`" · "`<line>`" |

Plus the discards: shapes used by exactly one brand, kept in a separate list.

## How to read it

**Four of five brands doing the same thing is the category convention.** That is the thing every new entrant is measured against — you either meet it or you deliberately break it, but you should not stumble into it by accident.

**The one-brand shapes are the interesting half.** A shape nobody else uses is either an idea the category has not found yet or one it has already tried and dropped. You cannot tell which from public data, so treat it as a cheap test, not as a plan.

**Count brands before you count creatives.** Twenty-three creatives from four brands is a convention. Twenty-three creatives from one brand is one company's habit, and it dressed up as a trend because it out-produced everyone else.

**Keep the copy, not the ad.** What goes in the swipe file is the shape and the line. The finished creative belongs to them; the structure is what you brief.

## The trap

> [!WARNING]
> **Deduplication happens inside each brand, not across the sweep.** If three of your five brands run the same stock footage, the same agency template or the same seasonal format, it survives as three separate creatives and inflates whichever shape it belongs to. Before you call something a category convention, check that the examples come from genuinely different companies — sibling brands under one parent are the usual culprit.

## Go deeper

- Add two more brands to the sweep and tell me if the ranking of shapes changes.
- Which shapes does my own account use, and which of these am I missing?
- Show me only the shapes that no brand in this list uses — the open space.
- Write one hook per shape for my product, keeping their structure and none of their words.
- Publish the swipe file as a hosted report grouped by hook shape.

## Fields this uses

None. A swipe-file sweep is built entirely from Meta's public Ad Library, so it touches **no field in [../06-reference/all-fields.md](../06-reference/all-fields.md)** — nothing here requires an account, a permission or a token. It runs on `meta_ads_research.run_audit` once per brand and `meta_ads_research.publish_report` for the shareable version: [../06-reference/all-actions.md](../06-reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
