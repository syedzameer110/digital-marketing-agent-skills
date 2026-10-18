---
name: marketing-automation-agent
description: Builds and operates the marketing automation layer — customer journey mapping, workflow design, behavioral triggers, drip and nurture sequences, lead scoring, CRM sync, and automated reporting. Use this skill whenever the user mentions marketing automation, workflows, drip campaigns, email sequences, lead scoring, lifecycle marketing, HubSpot, Marketo, Braze, Customer.io, Klaviyo flows, CRM integration, MQLs, or abandoned-cart flows — even if they never say "automation" explicitly.
---

# Marketing Automation — Main Agent (Command Hub)

## Channel Overview

Marketing automation is the force multiplier that operationalizes every other channel: it
converts one-off campaigns into always-on journeys that fire on behavior — a signup, a
pricing-page visit, an abandoned cart, a drop in product usage — instead of the calendar.
Because messages arrive at the moment of intent, automated flows typically earn 2–5x the
revenue per message of batch-and-blast campaigns; in mature e-commerce programs automations
produce 30–40% of total email revenue from a fraction of the sends, and in B2B they carry
the entire lead-to-opportunity handoff. The channel also enforces discipline: lifecycle
stages (subscriber → lead → MQL → SQL → customer), suppression logic, and clean CRM data
are prerequisites, which is why automation quietly raises the quality of every channel
that feeds it. No other channel turns strategy into always-on execution: paid captures the
lead, content earns the attention, email carries the message — automation decides what
happens next, every time, without anyone clicking send.

Time-to-value is fast for the core layer and slower for the full engine: welcome,
abandoned-cart, and lead-nurture flows can be live in 2–4 weeks, while scoring models, CRM
sync, and behavioral branching usually need 1–3 months to stabilize and calibrate. Costs
split into platform fees (free tiers at Brevo/Mailchimp; ActiveCampaign from ~$29/mo;
HubSpot Marketing Hub Pro from ~$800/mo; Marketo and Braze typically $2,000–$10,000+/mo at
enterprise volumes) and the larger hidden cost — implementation labor for journey design,
event schemas, and integration (Zapier/Make for glue, Segment for event infrastructure).
Automation wins when journeys repeat, sales-marketing handoffs leak revenue, and
first-party data exists; it adds little for pure one-off blasts or audiences too small to
segment.

## Agent Hierarchy

```text
marketing-automation-agent (command hub)
└── sub-agents/
    ├── workflow-design/          → map journeys & blueprint workflow logic
    ├── trigger-setup/            → events & conditions that start automations
    ├── lead-scoring/             → rank leads by readiness to buy (MQL thresholds)
    ├── nurturing-sequences/      → build welcome, nurture & win-back drips
    ├── crm-integration/          → Salesforce/HubSpot sync, fields, lifecycle stages
    ├── behavioral-targeting/     → act on site, app & product behavior signals
    └── dashboard-reporting/      → automated flow revenue & funnel reporting
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| workflow-design | Launching any new journey, quarterly refresh, or overlapping-flow audit | Lifecycle stage map, conversion goals, channel inventory | None (entry point) |
| trigger-setup | A flow needs an entry point; triggers misfire, double-fire, or go silent | Event schema, form list, platform admin access | workflow-design |
| lead-scoring | Sales rejects marketing leads, no threshold set, or score distribution skews | ICP definition, CRM outcome history, sales sign-off | crm-integration |
| nurturing-sequences | A journey is designed and needs its actual emails/drips built | Sequence brief, brand voice, offers, content assets | workflow-design, trigger-setup |
| crm-integration | New platform stack, sync errors, duplicates, or lifecycle stages disagree | CRM + platform admin access, field inventory, dedupe rules | None (parallel-safe) |
| behavioral-targeting | High-intent behaviors (pricing views, carts, usage) trigger nothing | Event tracking plan, analytics data, segment definitions | trigger-setup |
| dashboard-reporting | Reporting is manual, flows lack revenue attribution, or errors surface late | Platform exports, GA4, revenue data, KPI tree | All (terminal node) |

## End-to-End Workflows

### Workflow A — Lead-to-Customer Pipeline (B2B, weeks 1–8)

1. Run **workflow-design** to map the subscriber → lead → MQL → SQL → customer journey and
   blueprint the workflows: instant response, education nurture, MQL alert, re-engagement.
   Output: signed-off journey map + build-ready workflow specs.
2. Run **crm-integration** so lead records, owners, and lifecycle stages sync bidirectionally
   between platform and CRM (HubSpot/Salesforce), with dedupe and conflict rules. Output:
   clean two-way sync verified with dummy records.
3. Run **trigger-setup** to wire entry points: form fills, demo requests, content downloads,
   chat captures — plus exit criteria (became customer, disqualified). Output: tested,
   registered triggers with suppression.
4. Run **lead-scoring**: fit + behavior model, 100-point MQL threshold, negative scoring,
   and decay — calibrated with sales against 90+ days of closed-won data. Output: live
   scoring model with routing and alerts.
5. Run **nurturing-sequences** to build the education track (5–7 emails over 4–6 weeks) and
   the instant speed-to-lead response flow. Output: live sequences with branches.
6. Layer **behavioral-targeting**: pricing-page visits, repeat demo-page sessions, and
   multi-page high-intent browsing accelerate scores or alert sales. Output: behavior
   branches live inside the journeys.
7. Switch on **dashboard-reporting**: flow attribution, MQL→SQL conversion, error alerting,
   weekly ops review. Output: automated funnel + revenue dashboard.
8. Enter the recurring loop: quarterly optimization against the dashboard, score
   recalibration, and journey refreshes as the offer and ICP evolve.

### Workflow B — E-commerce Lifecycle Engine (weeks 1–6)

1. **workflow-design** maps the customer lifecycle (browse → first purchase → repeat → VIP →
   at-risk → win-back) and blueprints the core revenue flows.
2. **trigger-setup** wires browse-abandon, abandoned-cart (1h/24h/72h cadence), post-purchase
   cross-sell, replenishment, and win-back entries with purchase-exit suppression.
3. **behavioral-targeting** defines the event schema (view_item, add_to_cart,
   checkout_start) with the web/analytics stack so Klaviyo or Customer.io receives clean,
   consented events.
4. **nurturing-sequences** builds the flows: welcome series (highest revenue per recipient),
   abandoned-cart recovery (typically recovers 5–15% of abandoned carts), post-purchase,
   and win-back drips.
5. **crm-integration** (or platform-native customer profiles) unifies purchase history and
   predicted-LTV/segment properties so targeting uses one customer truth.
6. **nurturing-sequences + behavioral-targeting** extend the engine with replenishment
   timing, category cross-sell, and usage-based VIP identification.
7. **dashboard-reporting** instruments revenue per flow, RPR, completion rates, and weekly
   error checks; monthly optimization runs against channel benchmarks.

### Workflow C — Quarterly Automation Optimization Sprint (recurring)

1. **dashboard-reporting** ranks every live flow by revenue, completion, and error rate;
   flags underperformers (>25% below benchmark) and stale journeys.
2. **workflow-design** revises flagged journeys: prune dead branches, fix drop-off steps,
   retire redundant flows that fight for frequency.
3. **lead-scoring** recalibration against the last quarter of MQL→SQL→closed-won outcomes.
4. **trigger-setup + behavioral-targeting** wire newly identified high-intent signals as
   new entries or branches.
5. **nurturing-sequences** refreshes copy and offers in top flows and A/B tests subject
   lines and send times.
6. Close with **dashboard-reporting**: before/after comparison and next-quarter priorities.

## KPI Dashboard

North-star metric: **automation-attributed revenue share** — the percentage of total (or
email) revenue produced by automated flows rather than campaigns.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Automation-attributed revenue share | Platform + commerce/CRM data | Monthly | 20–40% of revenue from automations |
| Flow completion rate (entered → final step) | Platform workflow analytics | Monthly | 50–80% per flow |
| MQL → SQL conversion (sales acceptance >70%) | CRM (HubSpot/Salesforce) | Monthly | 10–25% |
| Speed-to-lead (form fill → first touch) | Platform logs | Weekly | <5 minutes for demo requests |
| Workflow error rate (failed sends/skips) | Platform logs + alerting | Weekly | <1% of executed actions |
| Unsubscribe / complaint rate from automations | Platform | Monthly | <0.3% / <0.05% per send |
| Revenue per recipient (RPR) by flow | Platform + commerce data | Monthly | Welcome/cart flows top of all sends |
| Database engagement decay (no click in 90d) | Platform | Quarterly | <40% of list dormant; re-engagement running |
| Sync health (record/field match rate) | CRM integration monitor | Weekly | >98% match, zero unprocessed errors |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| <$500 (starter) | Brevo/Mailchimp/ActiveCampaign Lite tier; build 3 core flows (welcome, nurture, re-engagement) in-house; Zapier free tier for glue |
| $500–$2,000 (growth) | ActiveCampaign Plus or Klaviyo; add cart/browse flows and lead scoring; 20–40 hours one-time implementation |
| $2,000–$10,000 (scale) | HubSpot Marketing Hub Pro or Customer.io; CRM sync project, behavioral branching, dashboard build; fractional ops hire |
| $10,000+ (enterprise) | Marketo, Braze, or Salesforce Marketing Cloud + Salesforce CRM; dedicated marketing-ops headcount; agency implementation support |

Allocation principles:

- Platform fees should stay under ~40% of budget; the majority belongs to implementation
  and optimization labor — a mid tier fully configured beats an enterprise tier empty.
- Budget 20–60 hours of one-time build per complex workflow (scoring, CRM sync, heavy
  branching); recurring optimization needs roughly 15–20% of platform spend monthly.
- Keep glue tooling (Zapier/Make) under ~$100/mo unless multi-tool event volume justifies
  a CDP like Segment.
- Fund the unglamorous layer first: CRM sync and suppression logic prevent the revenue-
  burning mistakes (duplicate sends, stale data) before any new flow goes live.
- Hold 10% for experiments: new trigger types, send-time optimization, and channel
  extensions (SMS, in-app) — automation compounds through iteration, not launches alone.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Journey strategy & workflow design | In-house marketing lead + this agent | Needs business context and a cross-channel view |
| Platform build & flow operations | In-house ops or trained freelancer | Daily iteration; agency retainers rarely pay off for steady-state ops |
| CRM/RevOps integration | In-house RevOps or specialist consultant | High blast radius; needs admin access and governance |
| Enterprise implementation (Marketo/Braze) | Certified agency/consultant | One-time builds benefit from platform certification |
| Lead scoring model | In-house with sales sign-off | The model is only valid once sales calibrates it |
| Trigger/event wiring | In-house ops (web team for site events) | Fast iteration; needs GTM/dev coordination |
| Reporting & dashboards | In-house (automated) | Once built, dashboards run themselves |

## Reporting Cadence

- **Weekly (ops, 30 min):** workflow error log, send failures, sync health, speed-to-lead,
  trigger anomalies. Decision: fix-or-rollback calls within 24 hours.
- **Monthly (marketing + sales, 1 hr):** flow-by-flow revenue and completion, MQL→SQL and
  sales acceptance, unsubscribe/complaint trends, top optimization backlog.
- **Continuous (automated):** error, sync, and silent-trigger alerts land in Slack within
  the hour; nobody waits for a meeting to learn a revenue flow broke.
- **Quarterly (leadership):** automation revenue share, lifecycle funnel health, scoring
  recalibration, platform cost-vs-value review, next-quarter journey roadmap. Decision:
  budget reallocation and platform renewal or consolidation calls.

## Cross-Channel Integrations

- **→ email-marketing-agent:** automations are the execution engine for its strategy —
  share design systems, copy standards, deliverability guardrails, and campaign-vs-flow
  frequency caps; automation revenue reports back into its KPI dashboard.
- **→ crm systems (Salesforce, HubSpot CRM):** lifecycle stages, lead scores, and
  engagement history sync bidirectionally; MQL alerts and routing tasks land in the CRM.
- **→ web-analytics-agent:** event schemas and conversion definitions stay identical
  across GA4 and the automation platform so behavioral triggers run on validated data.
- **→ cro-agent:** CRO learnings (offers, messaging, page tests) feed branch logic and
  on-site personalization; automation drop-off steps become CRO test candidates.
- **→ content-marketing-agent:** nurturing sequences consume its gated assets, case
  studies, and editorial content as sequence steps; content gaps found in journeys feed
  its calendar.
- **← sem-ppc / paid social:** paid-captured leads enter instant welcome and speed-to-lead
  flows; UTM/source metadata drives scoring and routing rules.
- **← affiliate-marketing / influencer-marketing:** partner-referred leads enter scoring
  with source metadata; discount-code redemption exits promo-sensitive flows automatically.
- **→ mobile-marketing:** push and SMS steps slot into journeys as channels beside email,
  governed by the same suppression, consent, and quiet-hours logic.
- **← web-analytics:** monthly attribution reconciliation keeps the automation revenue
  share (20–40%) consistent with GA4 and finance numbers.
