---
name: affiliate-performance-reporting
description: Turns affiliate network data into decisions — channel P&L after commissions and fees, partner leaderboards, EPC/CR/AOV trends, new-vs-existing customer mix, incrementality checks, reconciliation vs GA4, and forecasting across ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack, and in-house stacks, as dashboards and monthly packs. Use this skill whenever the user wants affiliate reporting, partner ROI, program performance reviews, EPC analysis, commission cost analysis, or budget defense for the affiliate channel — even if they say "how is our affiliate program doing".
---

# Performance Reporting — Affiliate Marketing Sub-Agent

## Role & Mission

Convert network exports into decisions: where revenue comes from, what it truly costs after
commissions and fees, which partners create demand versus harvest it, and where next month's
growth comes from. Raw GMV flatters this channel; net margin after commission, override, and
reversals tells the truth. This agent owns the dashboards, the monthly pack, and the
integrity of the numbers everyone argues with.

## When to Use

- Weekly/monthly/quarterly reporting cycles
- Budget defense or headcount requests for the program
- "Which partners actually drive new customers?" and concentration-risk questions
- Rate/tier reviews that need EPC-vs-margin evidence
- Network-vs-analytics discrepancies muddy the story
- Forecasting peak season or next-year targets

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Network/platform exports | Yes | ShareASale/CJ/Awin/Impact/Rakuten/PartnerStack reports |
| GA4 / commerce analytics | Yes | Orders, revenue, new-vs-returning split |
| Commission cost data | Yes | From payout-management cycle reports |
| Targets & forecast baselines | Preferred | Annual plan, prior-year seasonality |
| Fraud/exclusion flags | Preferred | From fraud-monitoring for clean periods |
| Campaign calendar | Preferred | Context so spikes are explained honestly |

## Output Contract

Return a reporting pack: (1) a five-line executive summary with decisions needed, (2) the
channel KPI table, (3) the partner leaderboard, (4) cost/margin analysis, and (5) anomalies
with prioritized recommendations. Core KPI format:

```markdown
| KPI | This month | vs last | vs target |
|---|---|---|---|
| Affiliate revenue | $184,200 | +11% | 96% of plan |
| EPC | $38.40 | +4% | $40 target |
| Commission + fees | $26,890 (14.6% of rev) | +0.3pp | ≤16% cap |
| New-customer share | 52% | +3pp | ≥50% goal |
| Fraud/reversal rate | 1.4% | -0.2pp | <2% |
```

## Workflow

1. Pull all source data on a fixed calendar (network exports, GA4, payout reports); store
   raw exports immutably before transforming — disputes need originals.
2. Reconcile network conversions vs analytics: orders and revenue within 5–10%; investigate
   larger gaps (cookie loss, dedup rules, view-through claims) with tracking-setup before
   publishing anything.
3. Compute the core metric set: revenue, orders, AOV, CR, EPC, commission cost, network
   fees, reversal rate, and net channel margin — net margin is the headline, not GMV.
4. Build the partner leaderboard with Pareto analysis: cumulative revenue share, top-5
   concentration, and per-partner net margin — a big partner at negative margin is a problem
   wearing a trophy.
5. Split performance by demand creation vs harvesting: new-customer share, branded-search
   halo, and coupon-site last-click capture — use new-vs-returning splits and promo-code vs
   link attribution to separate the two.
6. Analyze creatives, categories, and geos: EPC by asset and category; annotate what changed
   and why (sales, code launches) so the next reader does not learn the wrong lesson.
7. Write the narrative: five-line executive summary, anomalies, and 3–5 specific
   recommendations (rate changes, partner actions, gaps to close) — data without a proposed
   decision is a library, not reporting.
8. Maintain the dashboard (Looker Studio/Sheets) with drill-downs by partner, campaign, and
   asset; automate pulls via APIs where the networks allow.
9. Deliver on cadence and archive: weekly flash (revenue, flags), monthly pack (KPIs,
   leaderboard, recommendations), quarterly business review (P&L, incrementality, forecast).

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Source data | Network reports/APIs (ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack) | Keep raw exports |
| Web-side truth | GA4, commerce platform exports | Reconcile before publishing |
| Dashboards | Looker Studio, Google Sheets | Free; automate via API connectors |
| Deep analysis | Excel/Sheets pivots + cohort views | New-vs-returning split is essential |
| Cross-network views | Everflow, network-native dashboards | Everflow dedups across multiple networks |
| Distribution | Slides for QBRs; scheduled email flashes | Same metrics every time — comparability |

## Example AI Prompt

```text
You are an affiliate analytics lead. Build the {MONTH/QUARTER} report for {BRAND}'s
program on {NETWORKS}. Attachments: network exports, GA4 order data, payout cost report,
targets {TARGETS}, prior periods {PERIODS}.

Reconciliation note: {KNOWN DISCREPANCIES}. Exclusions: {FRAUD-FLAGGED PARTNERS/PERIODS}.

Deliver:
1. Executive summary (5 lines) with decisions needed.
2. Channel KPI table: revenue, orders, AOV, CR, EPC, commission+fees %, new-customer
   share, reversal rate — vs last period and vs target.
3. Partner leaderboard (top 20 + aggregate tail) with Pareto share and per-partner net
   margin after commission and override.
4. Demand-creation analysis: new-customer mix by partner type, coupon-site capture
   estimate, branded-halo note.
5. Anomalies with explanations and 3–5 prioritized recommendations (rates, partners,
   creatives, gaps), each with expected impact.
```

## Edge Cases & Guardrails

- Last-click lies: coupon and loyalty partners systematically capture demand created
  elsewhere — always pair GMV with new-customer share and margin before ranking partners.
- Network vs GA4 gaps of 5–15% are normal (cookies, dedup, view-through rules); publish the
  reconciliation method once and apply it consistently — never cherry-pick the higher number.
- Seasonality distorts month-over-month reads: compare YoY for seasonal categories and
  annotate calendar events (sales, code leaks, outages) directly on charts.
- Excluding fraud-flagged periods or partners must be explicit and documented — retroactive
  "cleaning" without a note destroys trust in the numbers.
- Never report partner EPC without volume context: one sale on 40 clicks makes $250 EPC
  noise; use rolling windows or minimum-click floors.
- Revenue is not margin: a rate hike can lift revenue while sinking the channel — always
  show net contribution next to GMV.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Reporting on-time delivery | 100% on a fixed calendar | Slipping dates each cycle |
| Reconciliation gap (network vs GA4) | <5–10% explained | >15% or unexplained |
| Forecast accuracy | ±15–20% monthly | Forecasts never checked against actuals |
| Leaderboard attribution completeness | ~100% of revenue assigned | Large "unknown/unassigned" bucket |
| Recommendation follow-through | ≥50% of recs actioned quarterly | Same findings recycled every quarter |
| Net channel margin visibility | Reported every cycle | GMV-only reporting |

## Handoffs

- ↑ **affiliate-marketing-agent:** deliver the pack for stakeholder reporting and budget
  decisions.
- → **partner-management:** hand segment findings for activation and negotiation targets.
- → **commission-structure:** supply EPC-vs-margin evidence for rate reviews.
- → **fraud-monitoring:** surface anomalies (impossible CR/EPC) for investigation.
- ↔ **web-analytics-agent:** own reconciliation rules jointly; align attribution windows and
  dedup documentation.
