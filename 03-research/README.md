# Research — reading ads you do not own

Open this section when you want to see what another brand is advertising on Meta right now, and you have no login, no partner access and no relationship with them.

Everything here runs on Meta's **public Ad Library**. You are not connecting to anyone's account, so there are no permissions to request and nothing for the other brand to approve.

## Four things to know before you start

**It is three calls, and the deliverable is a URL.** `meta_ads_research.run_audit` pulls and dedupes the brand's live ads, `meta_ads_research.view_creative` returns the frames and transcript of one creative so someone can actually look at it, and `meta_ads_research.publish_report` turns the result into a hosted report. The audit on its own is raw material. What you send to a client is the published report link.

**It costs money, per creative, by depth.** Roughly **$0.02** for a creative that is only discovered and deduplicated, **$0.08** if its audio is transcribed, **$0.10** if its frames are read. A verified discovery-only run on a public brand collapsed 40 ads to 8 unique creatives and billed **$0.16** — eight creatives at two cents. Depth is what costs, not brand size: an invented but arithmetically honest example — 12 creatives where 6 got transcripts and 4 got vision — comes to $0.92. Say the number out loud before you sweep ten brands.

**There are no performance metrics. None.** No CTR, no clicks, no conversions, and no likes, comments or shares either. `metrics_available` comes back `false` and always will. What you get instead are three proxies — `variants_total` (how many ads carry this one creative), `days_active` (how long it has been live) and `any_active` (whether it is still running). Every judgement on these pages is built on those three and on the creative itself. If a report you write implies engagement data, it is wrong.

**A weak brand match does not stop the run.** Pass `page_id` or the Ad Library URL when the name is ambiguous — [what-competitors-are-running.md](what-competitors-are-running.md) explains what goes wrong when you do not.

| File | Use this when… |
|---|---|
| [what-competitors-are-running.md](what-competitors-are-running.md) | You need a list of one brand's live ads, by brand name, in the next five minutes |
| [competitor-creative-teardown.md](competitor-creative-teardown.md) | You already know who to study and want the angles, formats and hooks behind their ads |
| [build-a-swipe-file.md](build-a-swipe-file.md) | You want to sweep a whole category and keep the handful of ideas worth stealing |

Actions behind this section: `meta_ads_research.run_audit`, `meta_ads_research.view_creative` and `meta_ads_research.publish_report` — see [../06-reference/all-actions.md](../06-reference/all-actions.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
