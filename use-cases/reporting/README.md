# Reporting

Open this section when the work is on a schedule — the Monday report, the month-end deck, the weekly check that nothing is drifting.

| File | Use this when… |
|---|---|
| [weekly-and-monthly-report.md](weekly-and-monthly-report.md) | You owe someone last week's or last month's numbers, by campaign, against the period before. |
| [budget-pacing.md](budget-pacing.md) | You need to know whether spend is on track for the budget you committed to. |
| [creative-fatigue.md](creative-fatigue.md) | You want the weekly check on ads whose frequency is climbing while clicks get more expensive. |
| [alerts.md](alerts.md) | You would rather be told when something breaks than remember to look. |
| [all-channels-at-once.md](all-channels-at-once.md) | The question spans Meta, Google and TikTok and you do not want three exports. |

**Skill:** [skills/meta-weekly-report/SKILL.md](skills/meta-weekly-report/SKILL.md) — loads the rate-decimal trap and the field list automatically.

## Four things that will bite you in every file here

Each is explained in full on one page. Read that page before you send anything to a client.

| What happens | Where it is explained |
|---|---|
| Click-through rates arrive as decimal fractions — `0.0256` means 2.56%, so a raw paste is wrong by 100x | [weekly-and-monthly-report.md](weekly-and-monthly-report.md) |
| `facebook_ads_conversions_all` counts video views and page likes as conversions | [alerts.md](alerts.md) |
| Weeks come back as bare numbers with no year, so a range crossing New Year sorts backwards | [creative-fatigue.md](creative-fatigue.md) |
| The budget fields cannot answer "am I pacing" — pace from spend by day instead | [budget-pacing.md](budget-pacing.md) |

Cost fields are the reassuring exception: they match spend ÷ actions exactly, with no rounding drift.
