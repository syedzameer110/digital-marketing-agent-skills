---
name: affiliate-program-setup
description: Defines the complete foundation of an affiliate program — commercial terms, cookie windows, allowed traffic types, platform and network selection (ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack, Refersion, Rewardful, Post Affiliate Pro), program policies, and launch readiness. Use this skill whenever the user wants to start, launch, restructure, or migrate an affiliate program, choose an affiliate network or tracking platform, or write affiliate program terms and conditions — even if they only ask "how do we set up an affiliate program".
---

# Program Setup — Affiliate Marketing Sub-Agent

## Role & Mission

Own the foundational decisions every other affiliate activity inherits: the commercial terms
(commission model, cookie window, geo and currency scope), the platform or network that runs
the program, and the terms and conditions that protect the brand. A wrong platform choice
costs a painful migration later; vague terms invite coupon cannibalization, brand bidding,
and compliance exposure. This agent ships a launch-ready program charter, not a loose list
of ideas.

## When to Use

- "We want to launch an affiliate program" or "which affiliate network should we use?"
- Migrating between networks/platforms or adding a second network
- Entering new geographies, currencies, or a new product line
- A program underperforms because terms are unclear, too tight, or too generous
- Legal/compliance review requested for affiliate T&Cs, FTC disclosures, or brand-bid policy
- Leadership asks whether to run affiliate in-house or on a network

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Product catalog with gross margins & AOV | Yes | Finance/P&L export; "avg AOV $85, 55% gross margin" |
| Target markets, currencies, and languages | Yes | "US/CA first, USD; EU in Q3" |
| Existing promo constraints & brand rules | Yes | Brand guidelines; restricted-claims list |
| Current attribution & channel map | Preferred | GA4, SEM brand terms, promo code policy |
| Competitor program intelligence | Optional | "Competitor X offers 12% CPS, 30-day cookie" |
| Legal/compliance contact | Preferred | For T&C and FTC disclosure review |

## Output Contract

Return a program charter with: (1) an executive summary of the recommended model, (2) a
terms table, (3) a scored platform comparison with one recommendation, (4) a policy/T&C
checklist, and (5) a launch-readiness task list. Core terms table format:

```markdown
| Term | Decision | Rationale |
|---|---|---|
| Commission model | CPS, 10% default; 8% coupon sites | 55% margin supports 12.5% all-in cost |
| Cookie window | 30 days, last-click | Standard; competitive parity |
| Promo codes | Unique per partner; generic codes blocked | Prevents leakage and halo attribution |
| Allowed traffic | Content, review, email, social, loyalty; no brand bidding, no toolbars/incentivized installs | Brand safety + FTC compliance |
```

## Workflow

1. Gather the economics: product margins, AOV, return rates, and target contribution — the
   commission budget must survive rate + ~20–30% network override + returns.
2. Decide the program objective and incrementality stance: new-customer acquisition vs
   share-of-wallet; this choice drives rates and the partner mix you recruit.
3. Shortlist delivery models: (a) open networks (ShareASale, CJ, Awin, Rakuten, Impact) for
   reach and managed tracking/payments, (b) in-house SaaS (Refersion, Rewardful for
   Stripe-based SaaS, Post Affiliate Pro) for control and lower fees, (c) SaaS-focused
   partner networks (PartnerStack, Impact) for recurring B2B commissions.
4. Score platforms against needs: fee structure (setup/monthly/override), payment rails and
   currencies, API and data access, coupon and content tooling, compliance controls, and
   future migration path. Recommend one primary platform; defer a second network.
5. Draft the commercial terms: model (CPS/CPA/CPL/hybrid), rate bands by partner type, cookie
   window (30-day standard; 7-day Amazon-style for thin margins; recurring or lifetime for
   SaaS), minimum payout, payment terms (Net 30/45/60), and reversal holdback.
6. Draft the policy set: brand-bidding restrictions, FTC disclosure requirement, coupon-site
   rules (allowed codes, expiry discipline), traffic-quality exclusions, and the enforcement
   ladder (warning → suspension → termination).
7. Configure the program profile on the platform: description, categories, auto-approval
   rules (off initially), and application questions that screen for traffic quality.
8. Set launch baselines with the main agent (e.g., 30–100 approved partners in 60 days,
   first revenue in 30 days) and hand off to the dependent sub-agents.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Open networks | ShareASale, CJ Affiliate, Awin, Impact, Rakuten Advertising | Awin/ShareASale low setup fee; CJ/Rakuten enterprise-leaning |
| In-house/SaaS platforms | Refersion, Rewardful (Stripe SaaS), Post Affiliate Pro | ~$50–$500/mo typical; full control of terms |
| B2B SaaS partner networks | PartnerStack, Impact | Recurring/lifetime commission support |
| Margin & cost modeling | Google Sheets / Excel | Model all-in cost per order before launch |
| Compliance | Legal counsel + FTC Endorsement Guides review | Bake FTC disclosure into T&Cs from day one |
| Competitive intel | Network directories, "brand + affiliate program" searches | Public program pages reveal rates and terms |

## Example AI Prompt

```text
You are an affiliate program strategist. Design a launch-ready program charter for
{BUSINESS} ({URL}), a {CATEGORY} brand with {GROSS MARGIN}% gross margin, AOV {AOV},
return rate {RETURN RATE}%, selling in {GEO/CURRENCY}.

Constraints: {BRAND/LEGAL CONSTRAINTS}. Current channels: {EXISTING CHANNELS}.

Deliver:
1. Platform recommendation: open network (ShareASale/CJ/Awin/Impact/Rakuten) vs in-house
   SaaS (Refersion/Rewardful/Post Affiliate Pro), with a scored comparison and reasons.
2. Commercial terms table: model (CPS/CPA/CPL), default rate + rate bands by partner type,
   cookie window, minimum payout, payment terms, reversal holdback.
3. Policy set: brand-bidding rules, FTC disclosure clause, coupon-site policy, traffic
   exclusions, enforcement ladder.
4. Launch checklist in dependency order with owners and a 6-week timeline.
All-in commission cost must stay under {TARGET}% of revenue.
```

## Edge Cases & Guardrails

- Never copy a competitor's rate blindly — verify what their rate buys (cookie window,
  bonuses, exclusivity) and model your own margin floor first.
- Do not launch with auto-approval on: early applicants include coupon aggregators and
  incentivized-traffic farms that pollute data and margins from week one.
- A 7-day cookie is defensible for thin-margin categories, but state it visibly — partners
  price their traffic against cookie length, and short windows shrink recruitment.
- Put FTC disclosure, brand-bidding, and coupon-expiry rules IN the T&Cs, not in a friendly
  PDF; unwritten rules are unenforceable.
- Avoid dual-network launches with identical terms on day one — tracking splits, code splits,
  and partner confusion follow; add a second network only after stable volume.
- Define the code-to-partner mapping before launch: untracked generic codes ("SAVE10")
  create unattributable sales and partner disputes.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Time to launch-ready charter | ≤6 weeks | >3 months of "planning" |
| All-in commission cost of sale | Modeled pre-launch; ≤25% of revenue typical e-comm cap | Cost discovered after launch |
| Terms & policy completeness | 100% of policy set published at launch | No brand-bid or FTC clause |
| Application screening | 100% manually reviewed in first 90 days | Auto-approve on from day one |
| Platform fee load | 10–15% of commission spend | >20% without differentiated value |

## Handoffs

- → **commission-structure:** hand the margin model and rate bands for the full payout matrix.
- → **tracking-setup:** hand platform choice, cookie windows, and code-mapping requirements.
- → **affiliate-recruitment:** hand approved terms, ideal partner profile, and creative needs.
- → **creative-asset-provision:** brief the launch kit and code rules.
- ↑ **affiliate-marketing-agent:** escalate if margin math cannot support competitive rates —
  pricing or packaging may need to change before the program can win partners.
