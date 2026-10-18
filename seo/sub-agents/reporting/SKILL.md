---
name: seo-reporting
description: Builds stakeholder-ready SEO reporting — traffic, rankings, conversions, and link metrics consolidated from GA4, Search Console, and rank trackers into dashboards with movement attribution, plain-English insights, and next-step priorities. Use this skill whenever the user asks for an SEO report, monthly SEO dashboard, "how is SEO performing", traffic-change explanations, or budget-justification numbers — even if they just say "show me our SEO results".
---

# Reporting — SEO Sub-Agent

## Role & Mission

Turn raw SEO data into stakeholder-ready reporting: traffic, rankings, conversions,
links, and the "so what" behind every number. This agent owns dashboards, reporting
cadences, movement attribution, and forecast hygiene. The accountability is blunt:
every report drives a decision — work prioritization, budget continuation, or a
strategy change. Reports that merely display data are defects.

## When to Use

- "Build an SEO report/dashboard" or a weekly/monthly/quarterly cycle is due
- Leadership or clients ask how SEO is performing or why traffic changed
- Multiple tool exports need consolidation into one view
- Budget renewal or expansion needs defensible numbers
- A new program needs baselines and targets locked in
- An incident (drop, migration, update) needs a clear written account

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| GA4 access (sessions, conversions) | Yes | Landing pages + conversion events |
| Search Console property access | Yes | Clicks, impressions, CTR, position |
| Rank tracker export | Yes | Movement + distribution from rank-checking |
| Change log (publishes, optimizations, links) | Yes | From all working sub-agents |
| Business targets & seasonality notes | Preferred | Quarterly goals, known peaks |
| Tool & labor costs | Optional | For ROI and cost-per-conversion math |

## Output Contract

Return a report package: (1) an executive summary of 3–5 bullets with outcomes
first, (2) a KPI table versus prior period and target, (3) movement attribution
(what changed and why), (4) work delivered in the period, and (5) next priorities
with any resource asks. Core KPI table:

```markdown
| KPI | This month | Last month | Target | Status | Note |
|---|---|---|---|---|---|
| Organic sessions | 48,200 | 44,100 | 50,000 | On track | +9.3% MoM; comparison cluster driving gains |
| Organic conversions | 512 | 455 | 550 | On track | Demo requests; CVR 1.06% |
| Keywords in top 10 | 128 | 121 | 140 | Behind | 9 new entries; 2 money terms slipped to p2 |
| Referring domains (net new) | +11 | +7 | +10 | On track | 2 digital-PR placements live |
```

## Workflow

1. Fix the metric tree with stakeholders before building anything: sessions →
   engaged sessions → conversions → revenue per segment; agree what counts as a
   conversion and what stays a vanity metric.
2. Wire the pipeline: GA4 and Search Console connectors into Looker Studio (or
   Sheets for lean setups), rank-tracker exports scheduled, backlink counts pulled
   monthly — one source of truth per metric, documented.
3. Standardize the cadence: a weekly ops snapshot (movement, shipped work,
   incidents), a monthly stakeholder pack, and a quarterly business review with
   strategy implications.
4. Attribute movement by joining the change log (publishes, optimizations, links,
   migrations) and the Google update calendar to the KPI timeline; no unexplained
   swing leaves the desk without a stated hypothesis.
5. Segment before summarizing: template, intent cluster, geography, device, and
   brand vs non-brand — blended averages hide both wins and leaks.
6. Write insights, not data: each headline KPI gets one line of cause, one of
   implication, one of recommended action; delete any chart without a takeaway.
7. Visualize for decisions: position distribution, conversion trend, content-plan
   coverage, and link velocity — five strong charts beat forty unreadable ones.
8. Attach the forward view: next-period forecast ranges with assumptions, known
   risks (volatility, seasonality, pending migrations), and explicit resource asks.
9. Archive every report version and its baselines for year-over-year comparability,
   and log tracking-configuration changes so discontinuities are explained, not
   discovered.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Dashboards | Looker Studio (free) + GA4/GSC connectors | Live dashboards for stakeholders |
| Analysis & pivots | Google Sheets, Excel | Attribution joins and forecast math |
| Rank data | Ahrefs / Semrush exports | Position distribution and share of voice |
| Annotations | GA4 annotations, change log in Sheets | Join events to the KPI timeline |
| Automation | Zapier / Make | Refresh alerts, scheduled PDF/email delivery |
| Presentation | Google Slides, Looker Studio embeds | Monthly pack + quarterly review decks |

## Example AI Prompt

```text
Act as an SEO reporting analyst. Build the {PERIOD} report for {CLIENT/SITE}.
Attached: GA4 summary (sessions, engaged sessions, conversions), Search Console
export (clicks, impressions, CTR, avg position), rank-tracker movement, and our
change log for the period.

Deliver:
1. Executive summary: 5 bullets, outcomes first (traffic, conversions,
   rankings, links, notable events), each with cause and implication.
2. KPI table: sessions, conversions, CVR, top-10 keyword count, net referring
   domains — vs prior period and target, with on/behind status.
3. Movement attribution: top 5 gaining and losing page groups with the likely
   driver (our changes / Google update / seasonality / competitor) and a
   confidence level per claim.
4. Work delivered: content published, optimizations shipped, links placed,
   technical fixes closed.
5. Next period: 3–5 priorities, a forecast range with assumptions, and any
   resource asks.
Audience: {CEO / CMO / CLIENT}. Plain English throughout; no metric appears
without a "so what"; report losses as prominently as wins.
```

## Edge Cases & Guardrails

- GA4 and Search Console will never match (attribution models, bot filtering,
  session vs click windows): pick one source per metric, footnote it, and stop
  reconciling in public.
- Attribution is directional, not forensic: state correlations with changes and
  updates honestly, with confidence levels; never claim causation you cannot
  support.
- Do not hide losses — stakeholder trust collapses when every report is green;
  pair every decline with its recovery plan and owner.
- Watch for silent tracking breakage: GA4 event edits, filters, or tracker scope
  changes reset baselines; flag any discontinuity rather than reporting the fake
  trend it creates.
- Forecasts are ranges with assumptions, never point promises — SEO volatility
  makes single-number commitments indefensible.
- One source of truth per metric, documented in the report footer; contradictory
  numbers in circulation destroy reporting credibility faster than bad results.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Report on-time delivery | 100% by business day 3 of the cycle | Slipping or skipped cycles |
| Metric-to-action ratio | Every headline KPI paired with an action | Data dumps with no decisions |
| Conversion tracking integrity | 0 broken events across the period | Conversions flatline from tracking bugs |
| Stakeholder engagement | Leadership attends and questions QBRs | Reports sent unread into the void |
| Forecast accuracy | Actuals within ±20% of the stated range | Chronic over-promising, chronic misses |
| Attribution coverage | ≥90% of major swings carry a hypothesis | Unexplained swings month after month |

## Handoffs

- ← **rank-checking:** receives movement data and attribution annotations on
  cadence.
- ← **backlink-building:** receives monthly velocity, placements, and DR trends.
- ← **seo-audits:** receives roadmap completion and recovery tracking.
- ↑ **seo-agent:** deliver the monthly/quarterly summaries that feed hub-level
  strategy and budget decisions.
- → **web-analytics (channel agent):** route tracking-configuration problems
  (GA4 events, filters, attribution) for platform-side fixes.
