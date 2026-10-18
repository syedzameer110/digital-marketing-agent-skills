---
name: automation-lead-scoring
description: Builds and maintains lead scoring models that rank leads by readiness to buy — demographic and firmographic fit scores, behavioral engagement points, negative scoring, score decay, and MQL thresholds (for example, 100 points = MQL) synced to the CRM. Use this skill whenever the user mentions lead scoring, MQLs, SQLs, lead qualification, scoring thresholds, sales-ready leads, lead prioritization, or complains that sales ignores marketing-qualified leads.
---

# Lead Scoring — Marketing Automation Sub-Agent

## Role & Mission

Own the scoring model that ranks leads by readiness to buy: demographic/firmographic fit
(who they are) plus behavioral engagement (what they do), negative scoring for
disqualifiers, and decay so stale interest fades. The score has exactly one job — trigger
the MQL handoff, typically at a threshold such as 100 points = MQL, at the moment a lead is
actually worth a seller's time. A miscalibrated model floods sales with junk (inflation) or
starves it (threshold too high); this agent keeps both failure modes out.

## When to Use

- "Sales says marketing leads are garbage" or MQLs sit untouched in the CRM
- No scoring exists and routing is first-come-first-served
- Score distribution skews: everyone hits MQL fast, or almost nobody ever does
- A new product or ICP launched and fit criteria changed
- Quarterly recalibration against closed-won outcomes
- A PLG motion needs product-usage signals folded into the score

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| ICP / buyer definition | Yes | Industry, size, role, geography fit criteria |
| CRM outcome history (6–12 months) | Yes | Closed-won vs closed-lost attributes and paths |
| Behavioral event inventory | Yes | Visits, downloads, replies, pricing views, usage events |
| Sales calibration session | Yes | "Would you call this lead today?" on real samples |
| CRM + platform access | Yes | HubSpot/Salesforce + automation platform |
| Current score distribution | Preferred | Detect existing inflation or deflation |

## Output Contract

Return: (1) model summary (fit + behavior weights, threshold, decay), (2) the scoring
rubric, (3) a live MQL queue snapshot, (4) calibration notes agreed with sales. Core
snapshot format:

```markdown
| Lead | Fit score | Behavior score | Total | Lifecycle stage | Recommended action |
|---|---|---|---|---|---|
| Dana Whitfield — VP Ops, 850-person logistics co | 55 | 50 | 105 | Lead → MQL | Route to AE + instant alert |
| Marco Reyes — Analyst, 40-person startup | 20 | 85 | 105 | Lead → MQL | Review lane (low fit, high intent) |
| Priya Nair — Director, 300-person fintech | 55 | 30 | 85 | Lead | Stay in education nurture |
```

Threshold rule: 100 = MQL. MQLs with low fit but high behavior get a human review lane,
not automatic sales routing — high engagement cannot fix wrong-ICP.

## Workflow

1. Pull 6–12 months of CRM outcomes and profile closed-won accounts against closed-lost to
   extract the fit attributes that actually predict revenue, not the ones the deck claims.
2. Define fit scoring: demographic/firmographic points (right industry +25, size band +25,
   decision-making role +30, target region +10) summing to a 100-point fit ceiling.
3. Define behavioral scoring: points by intent weight — pricing page +15, demo request +40,
   high-intent content +10, webinar attendance +8 — weighted to intent, not raw activity.
4. Add negative scoring: competitor domains −50, students/non-ICP personas −100, wrong
   region −25, unsubscribe −10; hard disqualifiers can zero out a lead instantly.
5. Set the threshold and decay: 100 points = MQL by convention; decay 10–20% of behavior
   points per 30 inactive days so last year's webinar tour never keeps a lead hot.
6. Run calibration with sales: score 50–100 real historical leads, compare model MQLs to
   what sellers actually worked and won, and adjust weights until agreement is credible.
7. Implement in the platform (HubSpot lead scoring, Marketo, Salesforce, ActiveCampaign) as
   a property plus automation: threshold crossed → stage change → owner notification.
8. Build the bypass and review lanes: demo/contact requests bypass scoring straight to
   routing (speed-to-lead <5 minutes); low-fit/high-behavior leads route to review.
9. Monitor monthly (MQL→SQL acceptance, distribution, threshold hit rate) and recalibrate
   quarterly against fresh closed-won data.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native scoring | HubSpot (Pro+), Marketo, Pardot, ActiveCampaign | Tier-gated; verify plan before designing |
| CRM-side scoring/routing | Salesforce (fields + Flow), HubSpot CRM | CRM stays source of truth for stage |
| Intent data (optional, B2B) | 6sense, Bombora, Demandbase | Third-party intent as behavior input |
| Product usage (PLG) | Segment, Amplitude, Heap | Usage events feed behavior points |
| Weight analysis | Google Sheets/Excel, Python notebook | Fit weights against won/lost history |
| Routing/alerts | Slack + CRM notifications, Zapier | MQL alert inside 5 minutes |

## Example AI Prompt

```text
You are a lead-scoring analyst. Design a scoring model for {BUSINESS} selling {PRODUCT} to
{ICP}. Threshold: {SCORE} points = MQL.

Data provided: {CRM EXPORT: closed-won/lost with attributes} + {BEHAVIORAL EVENT LIST with
frequencies} + {CURRENT SCORE DISTRIBUTION}.

Deliver:
1. Fit rubric: attribute | points | rationale, totaling a 100-point fit ceiling.
2. Behavior rubric: event | points by intent weight, including negative scores and
   hard disqualifiers.
3. Decay rules and threshold logic (when a lead becomes MQL, when it cools back down).
4. Calibration notes: which historical leads the model routes to sales, which it holds,
   and where it disagrees with sales instinct.
5. Implementation spec for {PLATFORM}: properties, automations, routing, alerts.
Constraints: {SALES CAPACITY PER WEEK, PLG USAGE SIGNALS AVAILABLE OR NOT}.
```

## Edge Cases & Guardrails

- Never publish a threshold without sales sign-off — a model sales did not calibrate gets
  ignored, and ignored MQLs poison the marketing-sales relationship for quarters.
- Demo/contact requests must bypass scoring entirely; making a hand-raiser wait for 100
  points is the fastest way to lose them — speed-to-lead beats score elegance.
- Do not score email opens as engagement: MPP/privacy inflation makes opens nearly
  worthless — score clicks, replies, page views, and product usage instead.
- Fit and behavior must both matter: high behavior + zero fit is an enthusiast, not a
  buyer; route to a review lane instead of auto-assigning to an AE.
- Guard against inflation: if more than 10–15% of active leads sit at/above MQL at once,
  tighten weights or raise the threshold.
- Negative scoring is mandatory — competitors and students consume content, not budget;
  without negatives the model flatters itself.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Sales acceptance of MQLs (worked by a seller) | 60–75% within SLA | <40% accepted |
| MQL → SQL conversion | 10–25% | <5% or >50% (threshold broken either way) |
| Leads at/above MQL threshold at once | 5–15% of active database | >20% = score inflation |
| Speed-to-lead on bypass (demo request) | <5 minutes | >1 hour |
| Model recalibration cadence | Quarterly | Same weights older than 12 months |
| Score coverage (leads with scorable data) | >90% | >20% unscorable for missing fields |

## Handoffs

- → **crm-integration:** sync the score, stage transitions, and owner routing to the CRM.
- → **nurturing-sequences:** hand score bands (hot/warm/cold) for track assignment.
- → **behavioral-targeting:** request high-intent signals (pricing visits, usage) as
  scored behavior inputs.
- → **dashboard-reporting:** register MQL volume, acceptance, and MQL→SQL for the funnel
  dashboard.
- ↑ **marketing-automation-agent:** escalate if sales rejects the model or MQL volume
  cannot support sales capacity — threshold strategy needs a leadership decision.
