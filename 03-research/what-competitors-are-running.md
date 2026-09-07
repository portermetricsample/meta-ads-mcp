# See what a competitor is running on Meta right now

A prospect asks how they stack up against the loudest brand in their category, and you have no access to that brand's ad account — only its name.

## Ask this

```
Pull the ads this brand is running on Meta right now from the public Ad Library:
<competitor brand name>

Deduplicate them, so one creative running in several placements is counted once.
Give me a table with the ad, whether it is an image or a video, and the first
line of the ad copy. Tell me how many unique creatives there are in total.
```

## What comes back

A list of live creatives, one row each. Names and numbers below are made up as an illustration — the shape is what matters.

```
Unique creatives live: 14

#   Format   Opening line of copy
1   video    "<first line of the ad copy>"
2   video    "<first line of the ad copy>"
3   image    "<first line of the ad copy>"
4   image    "<first line of the ad copy>"
…
```

> [!NOTE]
> Not every brand exposes the same detail in the Ad Library, so some columns come back thinner for one brand than another. Ask for what you want and take what arrives — the run does not fail because one field is missing.

## How to read it

**The count is the headline.** Fourteen unique creatives live means fourteen ideas in market, not fourteen ad sets and not fourteen dollars. A brand running two creatives is testing nothing; a brand running forty is running a creative factory, and you are competing with their volume, not their copy.

**Read the split between video and image before you read a single word.** It tells you where that brand believes attention is, and it is the cheapest thing to copy — you can change format this week, you cannot change positioning this week.

**Copy that repeats across creatives is their positioning.** One idea said fourteen ways is a brand that has decided. Fourteen unrelated ideas is a brand still searching, which is an opening.

## The trap

> [!WARNING]
> **This is a list of ads, not a list of results.** Nothing here comes from an ad account, so there is no spend, no click, no CTR and no ROAS attached to any row — none of the metrics in [../06-reference/all-fields.md](../06-reference/all-fields.md) apply, because those need an account you are connected to. If someone reads "14 ads" as "14× our budget", correct them. The Ad Library shows presence, never weight.

## Go deeper

- Do the same for the two brands closest to this one and put the three counts side by side.
- Split their live creatives by format and tell me which format they are betting on.
- Group their ad copy into themes and name each theme in one sentence.
- Which of their live ads mention a price, a discount or a guarantee?
- Publish this as a hosted report I can send to the client.

## Fields this uses

None. This reads Meta's public Ad Library, so it uses **no fields from [../06-reference/all-fields.md](../06-reference/all-fields.md)** — those are account fields and start applying only once an account is connected. The actions behind it are `meta_ads_research.run_audit` and `meta_ads_research.publish_report`, listed in [../06-reference/all-actions.md](../06-reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
