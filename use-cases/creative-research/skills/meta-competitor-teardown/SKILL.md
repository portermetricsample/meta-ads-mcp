---
name: meta-competitor-teardown
description: Read a brand's live Meta (Facebook/Instagram) ads from the public Ad Library through the Porter Metrics MCP and turn them into a hosted creative teardown. Trigger when the user asks what a competitor is running on Meta or Facebook, wants a swipe file, a creative teardown or a competitor ad audit, or pastes a Meta Ad Library URL. No ad account and no access to theirs is required. Encodes what the Ad Library does not contain, and the fact that the run bills per creative.
---

# Meta competitor teardown

## The job

Pull one brand's live ads from Meta's public Ad Library, deduplicate them, read the few worth reading, and publish a report. Works on brands you have no relationship with — `requires_account: false`.

## The steps — three calls, not one

**1 — `meta_ads_research.run_audit`.** Give it the brand name, or a `page_id` when the name is ambiguous. Those are the only two ways in — a pasted Ad Library URL is not a parameter. It pulls the live ads and deduplicates by hashing media bytes. This is raw material, not the deliverable.

Deduplication is dramatic and it is the finding: in a verified run, 40 raw ads collapsed to **8 unique creatives**, and one single creative was running as **38 separate ads**.

**2 — `meta_ads_research.view_creative`.** One creative at a time. This is the only step where anyone actually sees the ad — frames as pictures, plus the transcript, the headline and the on-image text. Pick the six to eight worth writing up first (mix the longest-running with the newest), because this step is where the cost is.

**3 — `meta_ads_research.publish_report`.** Returns the hosted link. That link is the deliverable.

## What to write up

For each opened creative: the format, the hook (the first thing a person sees or reads) and the angle (the promise or problem it leads with). Group the repeating angles and rank the groups by how many creatives sit in each.

The biggest angle group is where their production budget went — a funded hypothesis, not a proven winner. There is nothing in this data that says whether it worked.

A headline reading `{{product.name}}` is not a bug. Dynamic ads come back with the placeholder unrendered — that is how you spot product-feed creative from the outside. Read those rows as inventory, not messaging.

## Trap checklist — check every one before publishing

- [ ] **It costs real money, tiered per creative.** Roughly $0.02 for discovery, $0.08 with a transcript, $0.10 with vision. One verified run billed $0.16 total. Enriching everything instead of the six to eight you will use is where the bill comes from.
- [ ] **No platform split was claimed.** `platforms` is **eligibility, not delivery** — it lists where an ad is *allowed* to appear. The run's own limitation text says it cannot answer "IG vs FB share". A creative marked for both may have spent its whole life on one, and nothing here says which. If a draft says "they are 70% Instagram", delete the sentence: it is not a soft estimate, it is a number that does not exist. A real placement split needs a connected ad account and your own ads.
- [ ] **No performance metric was invented.** There is no CTR, no clicks, no conversions, no likes, comments or shares anywhere in this flow. The only proxies that exist are `variants_total`, `days_active` and `any_active`. Nothing here ranks creative by results.
- [ ] **Killed tests were accounted for.** `active_only` is **on by default**, so everything the brand has stopped running is invisible. Analysing what they abandoned needs a separate run with that turned off — say so rather than implying the list is everything they ever ran.
- [ ] **The raw-ads number was not presented as a count of their output.** `max_items` caps silently: a run that requested 40 returned 40 and flagged that the brand likely has more. The raw figure is a ceiling you set.
- [ ] **Brand resolution was confirmed.** A verified run auto-confirmed a brand at `confidence: 0.4` while recommending the user be asked to choose. When the name is ambiguous, pass `page_id` instead.
- [ ] **No field from the account-side reference was used.** This reads public data — nothing in `reference/all-fields.md` applies here, because you are connected to nothing.

## Stop and ask the user

- **Confirm the brand and the number of creatives to enrich before calling `view_creative`.** That call is the one that spends money, per creative.
- **Ask before publishing.** `publish_report` produces a hosted link that can be shared onward — confirm the user wants it published, and never put a client name in the report title without asking.
- If brand resolution comes back low-confidence, stop and ask the user which page they meant rather than auditing the wrong company.
