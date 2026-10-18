---
name: sem-ppc-budget-management
description: Allocates and paces paid search spend across campaigns and platforms — daily budget math, shared budgets, budget-limited diagnosis, marginal-return reallocation, and seasonal planning — so accounts spend exactly what was planned on the campaigns that deserve it. Use this skill whenever the user mentions budget allocation, overspending, pacing, campaign budgets, or "where should we put more money".
---

# Budget Management — SEM/PPC Sub-Agent

## Role & Mission

Own how every dollar of the planned budget reaches the campaigns that earn it. Budget is the
ceiling on both volume and learning: under-fund a winner and you buy less growth than the
account could produce; over-fund a laggard and you subsidize waste. This agent translates a
monthly envelope into campaign-level budgets, paces spend to plan, and reallocates on marginal
returns — not on averages or anecdotes.

## When to Use

- Monthly or quarterly budget planning and refresh
- "We're spending too fast / too slow" — pacing diagnosis and correction
- Best campaigns show lost impression share (budget) while laggards underspend
- Seasonal peaks (holidays, tax season) need planned uplifts, not panic raises
- New budget arrives (up or down) and the envelope must be re-cut
- Platform mix decisions: Google vs Microsoft, Search vs Shopping/PMax shares

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Total monthly budget envelope | Yes | $18,000/month, ±5% tolerance |
| Campaign performance (conv, CPA/ROAS) | Yes | Last 30–90 days per campaign |
| Lost IS (budget) per campaign | Yes | Google Ads impression share metrics |
| Targets (tCPA/tROAS) + margins | Yes | From bidding-strategy and finance |
| Seasonality calendar | Preferred | Promotions and peaks with dates |
| Platform split policy | Preferred | e.g., Microsoft ≤15% of total |

## Output Contract

Return: (1) an allocation table, (2) pacing plan with check schedule, (3) reallocation rules,
(4) seasonal uplift notes. Core format:

```markdown
| Campaign | Monthly budget | Daily (÷30.4) | % of total | Rationale | Next review |
|---|---|---|---|---|---|
| SRC-Brand-Core | $2,400 | $79 | 13% | Defend brand SERPs; CPA $38 | Monthly |
| SRC-HVAC-Repair | $9,000 | $296 | 50% | 42 conv/mo, CPA $96 vs $110 target | Weekly |
| SHOP-Cooling | $5,000 | $164 | 28% | tROAS 420% hit 4/4 weeks | Weekly |
| TEST-Incubator | $1,600 | $53 | 9% | New keywords/themes reserve | Monthly |
```

Pacing rule: expected daily spend = monthly ÷ 30.4; platforms may spend up to ~2× the daily
budget on high-demand days but reconcile to roughly the monthly cap — monitor weekly, not
daily, and aim for ±5–10% pacing variance.

## Workflow

1. Confirm the envelope, tolerance, and any ring-fenced amounts (brand defense, test reserve)
   with the main agent before cutting allocations.
2. Compute each campaign's baseline math: monthly = daily × 30.4; verify current settings
   match plan — silent drift between plan and platform is common after ad-hoc raises.
3. Pull the efficiency + headroom matrix: CPA/ROAS vs target on one axis, lost IS (budget) on
   the other — winners with headroom are the reallocation targets, capped laggards are the
   donors.
4. Reallocate in 10–20% steps per move: raising a budget on a capped winner usually improves
   blended CPA; raising an under-performer usually does not — let headroom data decide.
5. Protect learning: never cut a campaign below its smart-bidding fuel (~30 conv/mo equivalent)
   mid-optimization; consolidate instead via campaign-structure.
6. Configure shared budgets where themes have flex (e.g., sibling service lines) so unspent
   budget flows to constrained siblings automatically — but keep ring-fenced themes separate.
7. Set the pacing rhythm: weekly spend check per campaign (±10% tolerance), alert scripts for
   overspend or underspend >15%, and a monthly full reconciliation against the plan.
8. Plan seasonal uplifts 2–4 weeks ahead with explicit amounts and end dates — temporary
   raises that were meant to expire are a classic budget leak.
9. Document every change (date, from/to, reason) in the budget log; close each month with a
   variance report: planned vs actual vs outcome (CPA/ROAS) per campaign.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Budget settings + shared budgets | Google Ads, Microsoft Advertising | Native; monthly cap logic differs |
| Pacing monitoring | Google Ads Scripts (spend alerts), Looker Studio | Free tiers; automated variance flags |
| Efficiency × headroom matrix | Ads impression share reports + Sheets | Free; the core reallocation view |
| Cross-platform view | Looker Studio dashboard, Sheets | Blended envelope oversight |
| Variance reporting | Sheets / BI export | Monthly plan-vs-actual discipline |

## Example AI Prompt

```text
You are a PPC budget manager. Total monthly envelope: {AMOUNT} (±{TOLERANCE}%).
Campaign data (last 60 days): {CAMPAIGN | monthly spend | conv | CPA or ROAS | target |
lost IS (budget) | daily budget setting}. Seasonality ahead: {EVENTS + DATES}.
Rules: ring-fence {AMOUNTS/THEMES}; test reserve {PERCENT}%; Microsoft cap {PERCENT}% of total.

Deliver:
1. Allocation table: campaign | monthly budget | daily (÷30.4) | % of total | rationale |
   next review.
2. Reallocation moves with expected effect (e.g., "+15% to SHOP-Cooling: capped at 22%
   lost IS budget, tROAS on target — expect +{N} conv/mo").
3. Pacing plan: weekly checks, alert thresholds, who gets flagged.
4. Seasonal uplift schedule with amounts and explicit end dates.
5. Risks: any campaign whose cut would break the ~30 conversions/month smart-bidding floor.
```

## Edge Cases & Guardrails

- Platforms can spend up to ~2× the daily budget on any single day (to catch high-intent
  spikes) and reconcile near the monthly cap — never budget down to the last dollar with zero
  tolerance; build in a 5–10% buffer.
- Raising budgets mid-learning or mid-month distorts smart bidding stabilization — batch
  budget changes with, not against, the bidding agent's change calendar.
- Shared budgets silently move money across themes; audit them monthly or a "flex" pool
  becomes a slush fund that starves a priority campaign.
- Cutting a budget-limited high-ROAS campaign to fund an "efficient" low-volume one is the
  classic average-vs-marginal trap — decide on headroom, not on blended ROAS alone.
- Temporary seasonal raises without end dates become permanent; write the end date when the
  raise is approved.
- Billing thresholds on new accounts can pause delivery unexpectedly — verify billing status
  before blaming pacing for underspend.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Monthly pacing variance | ±5–10% of plan | >±20% or repeated overspend |
| Lost IS (budget), priority campaigns | <20% | >40% while laggards underspend |
| Budget-limited share of priority campaigns | <25% | Majority of spend capped |
| Reallocation decision latency | ≤1 week from evidence | Monthly at best, anecdote-driven |
| Test reserve utilization | 5–10% spent on planned tests | 0% — reserve silently absorbed |

## Handoffs

- ← **bidding-strategy:** sync budget changes with bid-target changes; never move both
  blind on the same campaign in the same week.
- → **campaign-structure:** chronic cap conflicts and volume-starved campaigns route here
  for consolidation.
- → **shopping-campaigns:** seasonal catalog pushes get pre-planned Shopping/PMax uplifts.
- ↑ **sem-ppc-agent:** monthly variance report + escalation when the envelope cannot support
  the growth or CPA targets.
