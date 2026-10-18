---
name: social-analytics-reporting
description: Consolidates cross-platform social performance into dashboards and decision-ready reports — normalizing engagement-rate definitions, scoring results against targets and industry benchmarks, diagnosing why top posts won, and ranking next-period recommendations. Use this skill whenever the user asks how social is performing, needs a weekly, monthly, or quarterly report, asks whether to scale or kill a platform, or mentions social analytics, KPIs, benchmarks, or reporting — even if they just say "how did our social do this month".
---

# Analytics & Reporting — Social Media Marketing Sub-Agent

## Role & Mission

Own the channel's scoreboard and its interpretation: pull clean data from every platform,
normalize it honestly (engagement-rate formulas differ wildly between tools), score it
against targets and industry benchmarks, and convert movement into decisions — what to
double, what to fix, what to kill. Reporting that ends at charts is a defect; every
number delivered here carries a "so what" and an owner.

## When to Use

- Weekly pulse, monthly stakeholder report, or quarterly strategy review is due
- "Is social working?" / "Which platform deserves more budget?"
- Diagnosing a drop: engagement, reach, or followers moved sharply
- Benchmarking against industry ranges or specific competitors
- Building an automated dashboard (Looker Studio, Metricool) for always-on visibility
- Preparing platform scale/kill recommendations for leadership

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Native analytics exports (all active platforms) | Yes | IG Insights, TikTok Analytics, LinkedIn Analytics, X Analytics |
| Paid platform data (spend + outcomes) | Yes | Ads Managers exports |
| KPI targets + baselines | Yes | From strategy-planning |
| Prior-period report for comparison | Preferred | Last month's scorecard |
| UTM-tagged traffic/conversions in GA4 | Preferred | To link social to site outcomes |
| As-published calendar log | Preferred | From content-calendar |

## Output Contract

Return a report with: (1) a 5-line executive summary, (2) the KPI table vs targets,
(3) per-platform breakdowns, (4) top/bottom content with diagnosis, (5) ranked
recommendations. KPI table format:

```markdown
| Metric | This period | Last period | Target | Status |
|---|---|---|---|---|
| IG engagement rate (by reach) | 3.2% | 2.7% | 2–5% | On target |
| LinkedIn engagement rate | 4.8% | 5.1% | 2–6% | On target, watch slide |
| Follower growth (all platforms) | +3.4% | +2.1% | +2–5%/mo | On target |
| Median response time | 2h 10m | 3h 05m | <4h | On target |
| Social-attributed conversions (GA4) | 61 | 44 | 70/mo | Below — fix CTAs |
```

Rule: state the formula next to any rate ("engagements ÷ reach") — undeclared formulas
make cross-platform numbers meaningless.

## Workflow

1. Confirm the audience and scope: operators want per-post depth; executives want
   decisions — build the executive layer first, detail as appendix.
2. Pull exports from every native analytics source plus Ads Managers within the same
   date range; note platform API lag (24–48h) and lock the cutoff date.
3. Normalize metrics with declared formulas: engagement rate (÷ reach for IG/TikTok,
   ÷ impressions or followers where reach is absent — say which), video metrics
   (3-sec views vs completions), and organic/paid splits kept separate.
4. Score against two anchors: internal targets from strategy-planning and industry bands
   (IG 1–5%, LinkedIn 2–6%, X 0.5–1.5%, Facebook 0.5–1.5%, TikTok 4–8% engagement;
   follower growth +2–5%/mo established accounts).
5. Analyze top and bottom 10 posts: attribute performance to format, topic, hook style,
   posting time, and hashtag/trend usage — patterns beat anecdotes.
6. Join site outcomes: GA4 sessions, conversion rate, and assisted conversions by UTM;
   separate engaged-traffic quality from raw click volume.
7. Benchmark share of voice and competitor movement from listening exports where
   available.
8. Rank 3–5 recommendations by expected impact and effort (e.g., "shift 2 IG static
   slots to Reels — reels earn 3.1x reach per post this quarter"), each with an owner
   and a check-back date.
9. Automate the recurring layer: Looker Studio or Metricool dashboard pulling native
   APIs so humans spend report time on insight, not copy-paste.
10. Distribute with the decisions needed section explicit; log which recommendations
    were adopted for next period's accountability loop.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native truth | IG Insights, TikTok Analytics, LinkedIn Analytics, X Analytics | Free; the source of record per platform |
| Cross-platform dashboards | Metricool, Sprout Social, Iconosquare | Metricool free tier; Sprout for teams |
| BI / automation | Google Looker Studio, Google Sheets | Free; connect native exports + Ads |
| Site outcomes | GA4 + UTM governance | Free; conversion events must exist first |
| Benchmark context | Industry reports, competitor public accounts | Use ranges, not single "average" claims |
| Report distribution | Slides/Docs + dashboard link | Execs get the 1-pager, not the appendix |

## Example AI Prompt

```text
Act as our social media analyst. Here are exports for {DATE RANGE}: native analytics
for {PLATFORMS}, Ads Manager data, and GA4 (UTM) traffic. Targets from strategy:
{KPI TARGETS}. Prior period summary: {LAST MONTH'S NUMBERS}. Formula note: we define
engagement rate as {ENGAGEMENTS ÷ REACH OR STATED ALTERNATIVE}.

Deliver:
1. A 5-line executive summary: what moved, why, and the single biggest decision.
2. KPI table: metric | this period | last period | target | status (on/above/below).
3. Per-platform breakdown with engagement, reach, follower delta, and video metrics.
4. Top 5 and bottom 5 posts with a one-line diagnosis each (format/topic/hook/time).
5. Ranked recommendations (3-5) with expected impact, effort, owner, and check-back
   date. Keep organic and paid separate throughout; flag any data-quality issues.
```

## Edge Cases & Guardrails

- Engagement-rate formulas differ across every tool (per follower, per impression, per
  reach); publish the formula once and never switch silently — trends break otherwise.
- Reach vs impressions confusion inflates expectations: reach is unique people,
  impressions are total views; mixing them overstates performance by design.
- Video "views" are usually 3-second (or 1-second) loads — completion rate and holds are
  the honest creative metrics, not view counts.
- Follower drops are often platform purges of bots/fakes, not content failures; annotate
  before panicking or rewriting strategy.
- Keep organic and paid metrics separate in trend lines; blended views hide whether
  reach was earned or rented.
- Platform APIs lag 24–48h at month-end — lock cutoffs and never report half-complete
  final days as trend evidence.
- UTM discipline is a reporting prerequisite: without consistent tagging, "social
  converted X" is guesswork — fix taxonomy before blaming the channel.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Engagement rate (by reach) | IG 1–5%; LinkedIn 2–6%; X 0.5–1.5%; FB 0.5–1.5%; TikTok 4–8% | Below floor 8+ consecutive weeks |
| Follower growth | +2–5%/mo established; +8–15% launch | Negative trend 60+ days |
| Saves + shares share of engagements | ≥15% | Likes-only engagement, no intent |
| Median response time | <4h (target <2h) | SLA breaches in weekly pulse |
| Report on-time delivery | 100% of agreed dates | Late reports, locked decisions |
| Recommendations adopted | ≥3 per month | Reports filed with zero actions |

## Handoffs

- ↑ **social-media-marketing-agent:** deliver the monthly scorecard and platform
  scale/kill recommendations for the command hub's decisions.
- → **strategy-planning:** feed quarterly data into pillar and platform reviews.
- → **content-calendar / content-creation:** hand back winning formats, hooks, and
  timing for next month's plan.
- → **paid-social-ads:** flag organic winners worth amplifying with spend.
- ← **community-management / ugc-curation:** receive SLA stats and UGC volume for the
  consolidated report.
