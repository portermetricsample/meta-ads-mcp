# Get told when something breaks

You do not want to open a dashboard every morning; you want to hear about it the day spend doubles, a campaign stops delivering, or cost per lead jumps.

## Ask this

```
Check my Meta ad account for the last 3 days against the 14 days before it.
Tell me only what is wrong: campaigns whose spend changed by more than 30%,
campaigns that spent yesterday but got no link clicks, ads that stopped
spending entirely, and any campaign whose cost per lead is more than 30%
above its own 14-day average.
Use offsite_conversion_fb_pixel_lead for leads, not conversions.
If nothing crosses those lines, reply "all clear" and nothing else.
```

Save it once and it becomes a one-line question every morning: *"run my Meta alert check."*

## What comes back

Either a short list, or one word.

```
ALERTS — last 3 days vs prior 14

spend spike     Campaign A     +64%   (1,240.00 → 2,030.00 per day)
no clicks       Campaign B     spent 310.00 yesterday, 0 link clicks
went dark       Ad 14          spent every day for 3 weeks, 0 for 2 days
cost per lead   Campaign C     18.40 vs 12.90 average   +43%
```

> [!NOTE]
> Invented figures. The thresholds are the ones you wrote into the question — nothing here ships with default alert levels.

## How to read it

**Be honest about what is scheduled and what is not.** Nothing in this connector watches your account on a timer or emails you. There is no alerting service. What you get is a question that returns a short answer, and three ways to make it recur:

- **Ask it on demand.** One saved sentence in your assistant, run when you sit down. No setup.
- **Save the analysis** so the definition — fields, period, comparison — is stored and reused instead of retyped, which is what keeps the numbers comparable week to week.
- **Publish it as a hosted report** you can open on a URL and send to a client, instead of re-running the question for them.
- **Put the schedule outside the connector.** Your assistant's own scheduled-task feature, if it has one, or an automation tool that can call the server on a cron — see [n8n](../05-connect/n8n.md).

"Went dark" is the alert that pays for the whole exercise. An ad that stops spending is invisible in a report that only shows what did spend, because the row simply is not there. You have to ask for it by comparing against the earlier period.

The cost-per-lead line is safe to threshold on: `facebook_ads_cost_per_lead` matches spend ÷ leads exactly, so a jump in it is a real jump, not a rounding artefact.

Thresholds are yours. Write the percentages into the prompt; there is no default and nothing will invent one for you.

## The trap

> [!WARNING]
> **An alert built on `facebook_ads_conversions_all` will never fire, because that field is not conversions.**
>
> It counts every action Meta records — video views, page likes, post engagements, comments, profile taps — and puts them in the same total as a purchase or a lead. On a live account this gap was measured at three orders of magnitude — the broad field reporting hundreds of thousands where the lead field reported barely a hundred. The measurement is in [the conversion tracking audit](../02-auditing/conversion-tracking-audit.md).
>
> That gap is what breaks an alert. A 30% fall in real leads moves the big total by nothing at all. The alert stays silent while the account bleeds. And a threshold set against that big number is not measuring your business, it is measuring how many people scrolled past a video.
>
> Name the event in the prompt. `offsite_conversion_fb_pixel_purchase`, `offsite_conversion_fb_pixel_lead`, `onsite_conversion_messaging_conversation_started_7d`. If you cannot say which event an alert is watching, the alert is not watching anything.

## Go deeper

- Same check, but for ad sets instead of campaigns.
- Add a rule for frequency above a number I give you.
- Which placements caused the spend spike in the flagged campaign?
- Show me the last 30 days by day for the campaign that went dark.
- Save this as a hosted report I can share with the client.

## Fields this uses

- [`facebook_ads_spend`](../06-reference/all-fields.md)
- [`facebook_ads_inline_link_clicks`](../06-reference/all-fields.md)
- [`facebook_ads_offsite_conversion_fb_pixel_lead`](../06-reference/all-fields.md) · [`facebook_ads_offsite_conversion_fb_pixel_purchase`](../06-reference/all-fields.md)
- [`facebook_ads_cost_per_lead`](../06-reference/all-fields.md)
- [`facebook_ads_onsite_conversion_messaging_conversation_started_7d`](../06-reference/all-fields.md)
- [`facebook_ads_frequency`](../06-reference/all-fields.md)
- [`facebook_ads_campaign_name`](../06-reference/all-fields.md) · [`facebook_ads_ad_name`](../06-reference/all-fields.md) · [`facebook_ads_date`](../06-reference/all-fields.md)

`facebook_ads_conversions_all` exists and is listed in the reference. Read the trap above before you point an alert at it.

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
