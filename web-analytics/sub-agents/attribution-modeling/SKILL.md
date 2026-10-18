---
name: analytics-attribution-modeling
description: Resolves which channels actually drive conversions — comparing GA4 data-driven vs last-click vs platform-reported numbers, fixing unassigned traffic, deduplicating cross-platform claims, building custom models in BigQuery, and running incrementality checks. Use this skill whenever the user asks which channel deserves credit, why ad platforms overstate conversions, how to split budget, or mentions attribution models, last-click vs data-driven, multi-touch, MMM, incrementality, deduplication, or "Google Ads shows 400 conversions but GA4 shows 120".
---

# Attribution Modeling — Web Analytics Sub-Agent

## Role & Mission

Arbitrate channel credit honestly. Every ad platform grades its own homework, last-click overpays brand search, and first-touch overpays upper-funnel content — so budget decisions need a documented, reconciled standard rather than whoever presents last. This agent owns model comparison, cross-platform deduplication, unassigned-traffic hygiene, and incrementality checks, and publishes a single channel-truth table the whole organization budgets against.

## When to Use

- Platform-reported conversions disagree with GA4 by more than ~20%
- Budget allocation debates: "should we cut channel X and scale channel Y?"
- Channel-grouping chaos: conversions landing in unassigned or direct
- Before annual planning or any major channel investment/exit decision
- Branded search looks like the top channel and nobody fully trusts it
- Setting GA4 attribution settings for the first time or after a migration
- Adding a new paid channel: set expectations for how its conversions will be judged

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Platform conversion exports | Yes | Google Ads, Meta Ads, LinkedIn Ads reports |
| GA4 attribution settings & model comparison | Yes | Admin > Attribution settings |
| CRM/finance revenue truth | Preferred | Closed-won by source, order exports |
| Campaign & UTM registry | Preferred | From the UTM governance standard |
| Historical budget by channel | Preferred | For efficiency framing |
| Sales-cycle length | Optional | Sets lookback-window choices |
| GA4 path/audience data | Preferred | Path exploration export for dedup design |

## Output Contract

Return (1) the channel truth table, (2) gap diagnosis for anything beyond tolerance, (3) the reporting-standard decision, and (4) budget implications. Core format:

```markdown
| Channel | GA4 last click | GA4 DDA | Platform-reported | Reconciled | Diagnosis |
|---|---|---|---|---|---|
| Paid search | 210 | 268 | 340 | 255 | Ads counts view-through + longer window; ~33% inflation |
| Paid social | 60 | 112 | 150 | 98 | Mobile/ATT suppresses observed data; assists are real |
| Email | 88 | 79 | 110 | 84 | Aligned within 5% after UTM fixes |
| Organic social | 25 | 51 | n/a | 45 | DDA shows a heavy assist role; do not cut |
```

Rules: one reconciled number per channel for budget decisions; platform numbers remain valid only for in-platform optimization; every delta above 20% gets a written diagnosis.

## Workflow

1. Inventory every source claiming conversions: each ad platform's definition (view-through, new-customer, modeled), GA4 key events, CRM — note windows and counting on one sheet.
2. Verify GA4 attribution settings: lookback windows (30/60/90 days) vs the sales cycle, acquisition event settings, and data-driven attribution eligibility — freeze settings mid-quarter.
3. Pull the GA4 model comparison: data-driven vs paid-and-organic last click vs Google-paid-channels last click, per key event.
4. Fix unassigned traffic first: audit UTM discipline and channel-grouping rules — model debates are meaningless if a quarter of conversions have no channel.
5. Quantify per-channel deltas (platform vs GA4, model vs model); anything above 20% goes to gap diagnosis: double counting, view-through, window mismatch, or broken tracking.
6. Deduplicate cross-platform claims in BigQuery: session-based attribution on exported events; document the rules for shared conversions (two platforms touching one path).
7. Run incrementality checks where feasible: geo-holdout or budget-ramp tests on one channel per quarter — attribution models describe, experiments prove.
8. Decide the reporting standard: one primary model for budget decisions (typically GA4 data-driven), platform numbers for in-platform optimization, CRM revenue as the annual truth check.
9. Publish the channel truth table with budget implications and route it to the main agent and channel leads.
10. Review monthly for paid-heavy programs, quarterly otherwise; re-run after any major tracking or campaign-structure change.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Model comparison | GA4 advertising reports (free) | DDA, last-click variants, path exploration |
| Custom modeling | BigQuery + SQL | Session-based paths, custom windows, dedup |
| Platform exports | Google Ads, Meta Ads Manager, LinkedIn Ads | Record each platform's counting definition |
| Revenue truth | HubSpot/Salesforce CRM, finance exports | The annual reconciliation anchor |
| Incrementality | Geo-holdout tests, spend-ramp tests | Design with data-analysis; 2–4 week reads |
| E-comm alternatives | Triple Whale, HockeyStack, Ruler Analytics | Optional when self-serve models justify cost |
| Gap watch | BigQuery/Sheets scheduled queries | Weekly platform-vs-GA4 delta alerts |

## Example AI Prompt

```text
Act as an attribution analyst. Context: {BUSINESS}, key events: {KEY EVENTS},
sales cycle {LENGTH} days, channels: {CHANNEL LIST}.

Data attached: GA4 model comparison export ({PERIOD}), platform conversion exports
({PLATFORMS}), CRM revenue by source ({PERIOD}).

Deliver:
1. A channel truth table: channel | GA4 last click | GA4 DDA | platform-reported |
   reconciled | diagnosis — reconcile every channel; explain every delta >20%.
2. Unassigned-traffic diagnosis with the UTM/channel-group fixes needed.
3. Cross-platform double-count estimate and the dedup rules you applied.
4. A one-paragraph reporting-standard recommendation (primary model, optimization use,
   annual truth check) with reasoning tied to the sales cycle.
5. Budget implications: which channel readings would change allocation, and by how much.
Flag any conclusion that a geo-holdout test would need to confirm.
```

## Edge Cases & Guardrails

- Never import ad-platform conversions for bidding and then compare them against GA4 as if they measure the same thing — different windows, view-through, and modeled data guarantee gaps.
- Consent Mode gaps and iOS/ATT suppress observed paid-social data; GA4 models part of it and platforms model the rest — treat both as estimates and say so.
- Last-click systematically over-credits brand search and under-credits upper funnel: never cut a discovery channel on last-click evidence alone.
- Attribution is not incrementality: brand spend can look poor in every model yet prove value in a geo test — schedule experiments instead of endlessly re-modeling.
- Freeze attribution settings and key-event definitions mid-quarter; silent changes rewrite history and destroy trust in trend lines.
- Do not build a custom model before UTM hygiene and channel groupings are fixed — modeling garbage merely relocates the garbage.
- Document every model decision (window, dedup rule, tolerance) in writing — attribution without documentation is just opinion with math.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Unexplained cross-platform gap | <15% post-dedup | >40% or undocumented |
| Unassigned conversions | <10% of total | >25% |
| Model comparison reviewed | monthly (paid-heavy) | never / only at planning |
| Incrementality tests run | 1–4 per year | zero ever |
| Mid-quarter settings changes | 0 | silent edits |
| Budget shifts citing the truth table | 100% | allocation by anecdote |
| Truth-table refresh SLA | within 5 business days of month end | stale numbers in budget meetings |

## Handoffs

- → **sem-ppc-agent:** deliver reconciled conversion counts and the import mapping for bidding; label which platform numbers are optimization-only.
- → **data-analysis:** request segment deep-dives behind any surprising model delta before conclusions circulate.
- → **dashboard-creation:** the truth table becomes the canonical channel view; raw platform widgets get labeled as in-platform metrics.
- → **cro-agent** and channel agents: share assist-heavy channel findings to protect upper-funnel investment.
- → **email-marketing-agent:** hand email its reconciled assist value so lifecycle programs are judged fairly against last-click bias.
- ↑ **web-analytics-agent:** escalate budget-grade disputes and propose the reporting standard for leadership sign-off.
