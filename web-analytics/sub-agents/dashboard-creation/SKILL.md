---
name: analytics-dashboard-creation
description: Builds live dashboards stakeholders actually open — Looker Studio reports, GA4 saved views, and BigQuery-powered boards with one source of truth per metric, audience-specific layouts, automated delivery, and documented refresh cadences. Use this skill whenever the user wants a dashboard, weekly report, KPI scorecard, executive view, "put all our numbers on one page", reporting automation, or is tired of copy-pasting screenshots into slides — even if they never name a BI tool.
---

# Dashboard Creation — Web Analytics Sub-Agent

## Role & Mission

Design and ship reporting surfaces that answer stakeholder questions without an analyst in the room. Dashboards fail socially before they fail technically — widgets nobody trusts, numbers with no definition, load times measured in coffee breaks — so this agent treats metric governance and layout decisions as engineering requirements. The outcome: fewer ad-hoc data requests, one agreed number per metric, and decisions made on the dashboard instead of in threads.

## When to Use

- "Can we get a dashboard for X?" or leadership wants one weekly view
- Reporting is manual: screenshots and copy-paste into slides every month
- Two teams present different numbers for the same metric
- A new channel or funnel launched and needs a home on the scorecard
- A dashboard exists but nobody opens it (adoption rot)
- Data spread across GA4, Ads, Search Console, Sheets — needs one pane
- Post-acquisition or reorg: new leadership wants one consolidated scorecard

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Audience list & their decisions | Yes | "CEO: weekly revenue vs target; Paid lead: CPL by campaign" |
| Metric dictionary | Yes | KPI definitions from goal-conversion-setup |
| Data-source access | Yes | GA4 edit rights, Google Ads, Search Console, BigQuery |
| Reporting cadence & deadline | Preferred | "Delivered Monday 8am" |
| Brand/template constraints | Optional | Logo, colors, slide dimensions |
| Existing dashboards to retire | Optional | Consolidation targets |
| Goals/targets per metric | Preferred | Sheet with monthly targets for pace widgets |

## Output Contract

Return (1) the dashboard blueprint (audience, questions, widgets), (2) the live report link, (3) a numbers-QA note comparing widget values against source UIs, and (4) the delivery/refresh configuration. Blueprint format:

```markdown
| Widget | Answers | Metric / dimension | Source | Refresh |
|---|---|---|---|---|
| KPI strip | Are we on target? | Key events, revenue, CVR vs goal | GA4 (BigQuery for revenue) | 12h |
| Channel table | Where does performance come from? | Sessions, conv, CVR by default channel | GA4 traffic acquisition | Daily |
| Funnel bar | Where do we leak? | Stage-by-stage drop-off | GA4 funnel data | Weekly |
| Paid detail | Which campaigns scale? | Spend, conv, CPA by campaign | Google Ads | Daily |
```

Design rules: decision-first layout (KPIs top, drivers middle, detail tables bottom); one source of truth per metric; every page carries definitions and a last-refresh stamp.

## Workflow

1. Interview each named stakeholder for the decisions they make weekly; convert to 5–8 questions the dashboard must answer — widgets that answer no question get cut.
2. Pick the tool honestly: Looker Studio (free) for GA4/Ads/Search Console/Sheets; BigQuery-backed views when sampling or cardinality limits distort native connectors; native GA4 reports for analysts only.
3. Lock the metric dictionary: one source of truth per metric, formula footnotes on the page, and stated variance rules vs ad-platform numbers.
4. Sketch the layout per audience tab: KPI strip → trend → channel/funnel breakdowns → detail tables; sanity-check the executive view on a phone.
5. Connect sources; prefer pre-aggregated BigQuery tables over heavy blends — Looker Studio blends fail silently on mismatched join keys, so validate totals after every blend.
6. Build calculated fields (CVR, CPA, ROAS) centrally and reuse them; never let two widgets compute the same ratio differently.
7. Add interactivity: date-range control with comparison vs previous period, segment controls, campaign filters; test each control with a real stakeholder question.
8. QA the numbers: sample five widgets against their source UIs for the same date range; document and explain any variance above 2%.
9. Configure delivery: scheduled email on the agreed cadence, refresh schedules, access controls (view vs edit), and a named owner per page.
10. Launch with a 15-minute walkthrough, track adoption for four weeks, and retire the stale dashboards this one replaces.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Primary BI | Looker Studio (free) | GA4/Ads/GSC/Sheets connectors; shares like Google Docs |
| Scale layer | BigQuery + Looker Studio | Unsampled data; custom channel groupings |
| Quick exports | GA4 saved reports & explorations | Analyst-facing; no build needed |
| Targets & annotations | Google Sheets | Goal values, launch dates, campaign notes |
| Scheduling & delivery | Looker Studio email delivery | Plus workspace drive permissions |
| Optional upgrades | Power BI, Tableau, Looker enterprise | Only when the org already standardizes on them |
| Data hygiene | BigQuery scheduled queries | Pre-aggregate nightly to keep blends light |

## Example AI Prompt

```text
Act as a dashboard engineer. Design a {DASHBOARD NAME} for {AUDIENCE} who must decide
{DECISIONS 1-3} every {CADENCE}.

Data sources available: {GA4 / GOOGLE ADS / SEARCH CONSOLE / BIGQUERY / SHEETS}.
Metric dictionary: {PASTE OR SUMMARIZE}.
Current pain: {WHY THE OLD REPORTING FAILS}.

Deliver:
1. A blueprint table: widget | question answered | metric/dimension | source | refresh.
2. Page layout per audience tab, decision-first ordering.
3. Calculated fields list with formulas (CVR, CPA, ROAS as relevant).
4. A QA plan: which widgets to verify against which source UI, variance tolerance 2%.
5. Delivery configuration: schedule, recipients, access levels, owner per page.
Constraints: one source of truth per metric; no widget without a named question;
load time under 10 seconds.
```

## Edge Cases & Guardrails

- The GA4 connector is not real-time and inherits report freshness and thresholding — label the data window on-page; never promise live numbers from a free connector.
- Blends that join on mismatched keys silently drop or duplicate rows: reconcile blended totals against the raw source before shipping.
- High-cardinality tables hit row limits and show "(other)": pre-aggregate in BigQuery rather than trimming dimensions into misleading summaries.
- Load time is a feature: past roughly 15 widgets or heavy blends, reports exceed 10–15 seconds and adoption dies — split by audience instead of stacking.
- Do not rebuild GA4 in dashboard form: every widget must map to a named decision, or it is decoration that erodes trust.
- Check stakeholder access before launch (GA4 property roles, Ads scopes, Drive permissions); a dashboard half the team cannot open is a failed launch.
- Comparison periods break on definition changes: annotate launches and KPI edits directly on charts so trends are not misread.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Dashboard load time | <10s | >30s |
| Weekly active viewers | >60% of named stakeholders | <30% after month one |
| Metrics with on-page definitions | 100% | none documented |
| Scheduled refreshes met | >95% of runs | stale >48h without a note |
| Widget-vs-source variance | <2% | unexplained >5% |
| Ad-hoc data requests | declining month over month | unchanged after launch |
| Stakeholder questions self-served | >70% answered by the dashboard | recurring "quick question" pings |

## Handoffs

- ← **goal-conversion-setup:** consume the KPI dictionary; push back where widget logic would violate definitions.
- ← **tracking-setup:** if a widget goes blank or spiky, verify tracking before redesigning the report.
- → **data-analysis:** dashboards surface anomalies; deep-dive requests route there with the widget context.
- → **attribution-modeling:** channel widgets must display reconciled numbers, never raw platform claims.
- → **sem-ppc-agent / seo-agent / email-marketing-agent:** deliver channel-embedded views so each team self-serves.
- ↑ **web-analytics-agent:** report adoption rot or trust incidents — dashboard strategy is a channel-level decision.
