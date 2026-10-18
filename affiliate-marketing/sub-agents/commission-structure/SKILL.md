---
name: affiliate-commission-structure
description: Designs and stress-tests affiliate payout models — CPS, CPA, CPL and hybrid bounties, tiered bonuses, rate bands by category and partner type, margin guardrails, cookie-window economics, and special deals for content, coupon, loyalty, and B2B SaaS partners. Use this skill whenever the user asks what commission to pay, CPS vs CPA vs CPL, tiered commissions, performance bonuses, lifetime or recurring SaaS commissions, or says commissions are eating margin — even if they just say "what should we pay affiliates".
---

# Commission Structure — Affiliate Marketing Sub-Agent

## Role & Mission

Set payout economics that make partners motivated to promote you and the business profitable
when they do. Every rate decision trades partner enthusiasm against contribution margin —
and unlike ad spend, a commission-rate mistake repeats on every order until changed. This
agent owns the payout matrix, tier and bonus design, margin guardrails, and the recurring
repricing cycle, converting finance data into rates partners can act on.

## When to Use

- Program launch: the first commission matrix
- "What commission should we pay?" for a new category, market, or product line
- Margin compression: commissions + discounts + returns are eating contribution
- Top partners demand better rates, or competitors raise theirs
- Adding tiers, bounties, or recurring/lifetime commissions (B2B SaaS)
- Quarterly rate review: EPC and margin per segment have drifted

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Gross margin by category/SKU | Yes | Finance export; "apparel 62%, accessories 45%" |
| AOV, return/refund rate, discount norms | Yes | Commerce analytics |
| Current commission spend & revenue by partner | Preferred | Network exports (ShareASale/CJ/Awin/Impact) |
| LTV / payback targets (especially SaaS) | Preferred | "Payback ≤ 6 months" |
| Network fee structure | Yes | Override %, monthly minimums |
| Competitor rate intel | Optional | Public program pages, partner communities |

## Output Contract

Return a payout design pack: (1) an economics summary (all-in cost per order at each
candidate rate), (2) the commission matrix, (3) tier/bonus rules with caps and sunsets,
(4) special-deal templates, and (5) reversal/clawback policy. Core matrix format:

```markdown
| Segment / category | Model | Rate | Cookie | Tier/bonus | Notes |
|---|---|---|---|---|---|
| Core apparel (content/review) | CPS | 12% | 30 days | +2% at $5k/mo | Baseline band; demand-creating partners |
| Coupon & deal sites | CPS | 8% | 30 days | — | Capped; no new-customer code stacking |
| B2B SaaS trial partners | CPA | $150/qualified trial + 20% rev share 12 mo | 90 days | $300 bonus at 10 trials/mo | Recurring via PartnerStack |
```

## Workflow

1. Pull margin truth from finance: gross margin per category after discounts and expected
   returns — commissions are paid on revenue that can partially reverse.
2. Define the all-in cost ceiling: rate × (1 + network override 20–30%) + reversal allowance
   must stay under the guardrail (all-in commission cost commonly 10–30% of revenue in
   e-commerce depending on category).
3. Choose the model per business type: CPS default for e-commerce; CPA ($20–$200+ per
   qualified action or trial) for B2B SaaS; CPL for validated lead-gen; hybrid (flat + %)
   for creator deals.
4. Set the baseline rate band per category from margin math, then adjust by partner role:
   content/review partners earn premium rates because they create demand; coupon/loyalty
   partners earn capped rates because they harvest it.
5. Design tiers and bonuses: monthly volume thresholds (+1–3%), new-customer bounties, peak
   boosters with explicit start/end dates — every bonus needs a margin-safe cap and sunset.
6. For SaaS: choose recurring vs lifetime commission (e.g., 20–30% recurring for 12 months,
   or 100–150% of first-year value one-off) and define trial-qualification criteria that
   exclude junk signups.
7. Define payout mechanics with payout-management: commission basis (product price net of
   tax and shipping), reversal/clawback rules, and a holdback period matching the return
   window.
8. Publish the rate card with a change-notice process (30 days notice for decreases per most
   network rules) and load special rates into the platform.
9. Review quarterly: EPC vs margin per segment; reprice laggards, protect what works, and
   retire bonuses that stopped changing behavior.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Rate/cost modeling | Google Sheets / Excel | Model all-in cost per order at every candidate rate |
| Performance data | ShareASale, CJ, Awin, Impact, Rakuten reports | EPC, CR, AOV, reversal rate by partner |
| SaaS partner programs | PartnerStack, Rewardful, Impact | Recurring/lifetime commission automation |
| Margin data | Finance/BI exports (Looker Studio, Sheets) | Category-level gross margin is the anchor |
| Competitive intel | Public program pages, partner communities | Rates often disclosed in recruitment posts |

## Example AI Prompt

```text
You are an affiliate economics strategist. Design a commission structure for {BUSINESS}
({CATEGORY}): gross margin {GM}% by category ({CATEGORY MARGINS}), AOV {AOV}, return rate
{RETURN}%, network override {OVERRIDE}% (or SaaS fee {FEE}/mo).

Goals: {NEW-CUSTOMER ACQUISITION / REVENUE SHARE / LTV GROWTH}; all-in commission cost
≤ {TARGET}% of revenue. Partner mix: {CONTENT / COUPON / LOYALTY / CREATOR / B2B LEAD-GEN}.

Deliver:
1. All-in cost per order table at candidate rates (baseline, +2%, +5%) including override
   and a {RETURN}% reversal allowance.
2. Commission matrix: segment/category | model (CPS/CPA/CPL) | rate | cookie window |
   tier/bonus rules | rationale.
3. Tier & bonus plan with caps, sunset dates, and margin guardrails.
4. Special-deal templates: content-partner premium, coupon-site cap, SaaS recurring/lifetime
   options with qualification criteria.
5. Change-management notes: notice periods, grandfathering, communication plan.
```

## Edge Cases & Guardrails

- Pay commissions on product price net of tax and shipping — define it in the terms;
  ambiguous bases cause monthly disputes.
- Stacked discounts plus commissions is silent margin death: cap code stacking before
  raising rates, then check margin per order, not per SKU.
- Rate decreases usually require 30 days notice on networks — plan repricing ahead of peak,
  never during it.
- Do not let coupon sites earn content-partner rates: last-click coupon conversions are
  often your own brand search wearing a costume.
- B2B CPA bounties attract junk leads: define qualification (budget, role, timeline),
  validate within 48 hours, and claw back unqualified conversions.
- Recurring/lifetime SaaS commissions are a long-term liability — model churn-adjusted LTV
  before promising 30% forever; prefer time-boxed (12-month) recurring terms.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| All-in commission cost of revenue | E-comm 5–30% by category | Negative margin after discounts |
| EPC (per 100 clicks) | $20–$100+ e-comm; $50–$300+ B2B SaaS | Declining EPC after a rate cut |
| Partner churn on rate changes | <10% of active partners | Top-10 partners resign post-change |
| Reversal/clawback rate | <5% of conversions | >8% — paying for unretained revenue |
| New-customer share of affiliate orders | ≥40–60% per program goal | Mostly existing-customer cannibalization |
| Rate review cadence | Quarterly | Same rates for 2+ years despite drift |

## Handoffs

- → **program-setup:** feed final rates into the published terms.
- → **tracking-setup:** hand code/link rules and rate-dependent dedup requirements.
- → **payout-management:** hand commission basis, reversal/clawback, and holdback rules.
- → **partner-management:** deliver rate-card change communications and tier qualifiers.
- ↑ **affiliate-marketing-agent:** escalate when no margin-safe rate is competitive — product
  economics or packaging must change first.
