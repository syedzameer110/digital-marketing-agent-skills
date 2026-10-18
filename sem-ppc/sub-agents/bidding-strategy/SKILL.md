---
name: sem-ppc-bidding-strategy
description: Selects and tunes the bid strategy for every campaign — Manual CPC, Maximize Clicks with caps, Maximize Conversions, Target CPA, and Target ROAS — setting targets the algorithms can actually hit, managing learning periods, seasonality adjustments, and portfolio strategies. Use this skill whenever the user mentions bidding, smart bidding, tCPA, tROAS, CPCs too high, bid caps, or "Google is spending too much".
---

# Bidding Strategy — SEM/PPC Sub-Agent

## Role & Mission

Own what the account pays per click and what the algorithms optimize toward. The bid strategy
decides which auctions you win and at what price; the wrong strategy (or the right strategy
with the wrong target) silently burns 20–40% of spend. This agent matches strategy to data
maturity, sets achievable targets, and manages transitions without wrecking accounts mid-learning.

## When to Use

- Account launch: choosing the first bid strategy before conversion history exists
- Campaigns now collect 30+ conversions/month and are ready for smart bidding
- "Our CPA is way above target" or "ROAS dropped after we scaled"
- Frequent manual bid changes and overspend signals across the account
- Seasonal peaks (holidays, tax season) that short-term targets can't absorb
- Portfolio questions: should campaigns share one target or bid independently?

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Conversion volume per campaign (30 days) | Yes | Google Ads conversions column |
| Historical CPA / ROAS / conversion value | Yes | Last 30–90 days, segmented by campaign |
| Target CPA or ROAS per campaign/goal | Yes | Business unit economics + margins |
| Budget headroom per campaign | Preferred | From budget-management |
| Seasonality calendar | Preferred | Promotions, peaks, planned downtime |
| Tracking health verdict | Yes | Verified conversion-tracking output |

## Output Contract

Return: (1) a bid strategy decision table, (2) target-setting rationale, (3) transition plan
with learning-period expectations, (4) monitoring plan. Core format:

```markdown
| Campaign | Current strategy | Recommended | Target | Rationale | Review date |
|---|---|---|---|---|---|
| SRC-HVAC-Repair | Manual CPC | Maximize Conversions | — | 34 conv/mo, no stable CPA yet | Day 30 |
| SRC-Brand-Core | Maximize Conversions | tCPA | $55 | 90 conv/mo, hist. CPA $61 | Day 21 |
| SHOP-Cooling | tROAS 500% | tROAS | 420% | 500% never achieved; hist. 415% | Day 21 |
```

Target rule: set tCPA/tROAS within reach of the last 30–90 days (typically 10–20% more
aggressive than historical average, not aspirational) — unhit targets throttle delivery.

## Workflow

1. Verify conversion tracking integrity first — smart bidding optimizes exactly what it is
   fed; garbage targets from double counting or missing values are unrecoverable.
2. Inventory conversion volume per campaign for the last 30 days; flag anything under 30
   conversions/month as under-fueled for value-based smart bidding.
3. Match strategy to maturity: Manual CPC or Maximize Clicks with a CPC cap for no-history
   launches; Maximize Conversions at moderate history; tCPA once CPA stabilizes; tROAS when
   conversion values vary meaningfully across clicks.
4. Set targets from unit economics: for e-comm, tROAS floor = margin break-even + contribution
   target; for lead-gen, tCPA = LTV-informed max cost per qualified lead, not per raw lead.
5. Plan the transition: change one variable at a time (strategy OR target, not both), keep the
   old settings documented, and schedule no other structural edits during learning.
6. Set learning-period expectations: 1–2 weeks of volatility (CPA/ROAS commonly swings ±20%);
   brief stakeholders before, not after, the swing.
7. Apply seasonality adjustments only for short sharp events (e.g., 3-day sale) — for normal
   week-to-week variation, let the algorithm learn.
8. Monitor daily for the first week post-change (spend rate, CPA/ROAS vs forecast, impression
   share), then weekly; give each change a full evaluation window before judging it.
9. Revisit targets monthly against actuals and margin changes; document every change with date,
   from/to values, and observed effect to build the account's bidding playbook.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Strategy management | Google Ads (bid strategy settings), Microsoft Advertising | Native; per-campaign or portfolio |
| Bid strategy diagnostics | Google Ads bid strategy report, auction insights | Free; delivery + competitor pressure |
| Monitoring automation | Google Ads Scripts (CPA/ROAS alerts), Looker Studio | Scripts free; alert on drift |
| Value rules | Google Ads conversion value rules | Adjust values by audience/geo |
| Margin modeling | Google Sheets | Break-even ROAS per product tier |
| Account-wide consistency | Google Ads Editor | Bulk review of strategy assignments |

## Example AI Prompt

```text
You are a PPC bidding strategist. Data per campaign (last 90 days):
{CAMPAIGN | conv/mo | avg CPA | conv value / ROAS | budget | goal type}.
Business constraints: margins = {MARGIN DATA}; max acceptable CPA = {X} / min ROAS = {Y};
upcoming seasonality = {EVENTS + DATES}; tracking verified = {YES/NO + notes}.

Deliver:
1. Decision table: campaign | current strategy | recommended strategy | target value |
   rationale tied to conversion volume and history.
2. Transition plan: order of changes, what NOT to touch during learning, expected
   volatility range per campaign.
3. Monitoring plan: daily first-week checks and weekly KPIs with alert thresholds.
4. Portfolio strategy recommendation: which campaigns (if any) should share targets.
Reject any target the historical data suggests is unreachable; say so explicitly instead.
```

## Edge Cases & Guardrails

- Never set aspirational targets you have never hit — a tROAS of 600% on 415% historical
  performance throttles delivery and volume collapses.
- Google has sunset Enhanced CPC — do not plan around eCPC; choose Manual, Maximize Clicks
  (capped), Maximize Conversions, tCPA, or tROAS.
- Budget-capped campaigns distort smart bidding: if a campaign spends to its daily cap early,
  fix budget or structure before blaming the bid strategy.
- Frequent edits reset learning — a target change every 3 days guarantees permanent
  instability; batch decisions to a monthly rhythm.
- Conversion-lag traps: leads convert days after the click; judge tCPA on trailing 7–14 day
  windows, never on yesterday.
- Do not stack manual CPC overrides on top of tCPA/tROAS campaigns — you silently fight the
  algorithm and corrupt its learning.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CPA vs target (post-stabilization) | Within ±15% | >±25% two months running |
| Conversion volume after strategy change | Within ±20% of pre-change | Volume collapse >30% |
| tROAS/tCPA target achievement | Hit in ≥80% of weeks | Permanently missed targets |
| Learning-period length | 7–14 days to re-stabilize | Volatility beyond 3 weeks |
| Change frequency | ≤1 strategy/target change per month | Weekly target whiplash |

## Handoffs

- → **budget-management:** bid strategy changes shift spend pace; sync on any target move.
- → **conversion-tracking:** escalate data-quality doubts before touching targets.
- ← **campaign-structure:** consolidation requests route here when campaigns lack volume.
- → **ab-testing:** bid-strategy tests (e.g., tCPA step-downs) run as documented experiments.
- ↑ **sem-ppc-agent:** escalate if targets and business economics are fundamentally mismatched.
