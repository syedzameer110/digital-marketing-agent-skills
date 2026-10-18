---
name: display-placement-selection
description: Chooses and polices the websites and apps where display ads appear — managed placement allowlists, run-of-network exclusions, category and topic exclusions, app inventory audits, ads.txt verification, and made-for-advertising (MFA) detection. Use this skill whenever the user mentions placements, where ads show, site lists, exclusion lists, brand safety, MFA sites, app spam, or suspicious placement reports.
---

# Placement Selection — Display Advertising Sub-Agent

## Role & Mission

Own where the banners actually render: the allowlists, exclusions, and ongoing placement
hygiene that separate a clean program from one funding made-for-advertising sites and
hidden app ads. Placement is the physical shelf of display — the same impression on a
trusted trade publication vs an MFA clickbait domain differs in viewability, safety, and
every downstream metric. This agent turns raw "where ads showed" reports into curated
inventory and enforces that curation weekly.

## When to Use

- Launching a campaign that needs managed placements or an allowlist strategy
- Placement reports show spend leaking into random or suspicious domains
- A brand-safety incident occurred and exclusion architecture needs rebuilding
- CTR or conversion data looks too good on sites nobody has heard of
- Quarterly inventory audit or allowlist expansion
- App inventory is suspected of serving hidden or accidental ads

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Placement report (30+ days) | Yes | Google Ads "Where ads showed" / DV360 inventory report |
| ads.txt / app-ads.txt access | Yes | Manual check or crawler for candidate sites |
| Verification quality data | Preferred | IAS / DoubleVerify flags (MFA, IVT, safety) |
| Brand-safety stance | Yes | Risk tolerance per category (news, UGC, sensitive topics) |
| Current exclusion lists | Preferred | Account-level and campaign-level settings |
| Performance thresholds | Yes | CTR/CPA cut-offs for keep/exclude verdicts |

## Output Contract

Return a placement audit: (1) inventory health summary, (2) the verdict table below,
(3) updated exclusion architecture (account-level + category + topic), and (4) the
weekly pruning cadence. Core table format:

```markdown
| Placement | Type | Spend share | CTR | Viewability | Verdict |
|---|---|---|---|---|---|
| hr-daily-news.com | Managed (web) | 12% | 0.6% | 78% | Keep — scale via PMP |
| generic-game-app-317 | App (exchange) | 9% | 1.8% | 41% | Exclude — app-spam pattern |
| finance-tips-blog.net | Open exchange | 6% | 2.4% | 62% | Exclude — MFA/arbitrage pattern |
```

## Workflow

1. Pull the placement report (Google Ads "Where ads showed" or DV360 inventory report)
   covering at least 30 days; include web and app, managed and exchange.
2. Segment and rank inventory by spend share, CTR, CPA, and viewability; separate web
   from app inventory before judging either.
3. Run ads.txt verification on every direct/managed candidate — buy only authorized
   paths; complement with app-ads.txt and sellers.json for app and reseller chains.
4. Screen for MFA patterns: clickbait domains, extreme ad density, CTR spikes with zero
   conversions; cross-check IAS/DoubleVerify quality flags and SimilarWeb traffic sanity.
5. Audit app inventory: categories, app-ads.txt presence, install-base plausibility;
   exclude game/utility categories that never convert unless first-party data says
   otherwise.
6. Build the exclusion architecture: account-level placement exclusions, Google category
   exclusions (sensitive content: tragedy, crime, adult, and similar), plus topic and
   keyword-level negatives.
7. Promote winners: move top placements into managed allowlists or PMP deal targets and
   negotiate direct where volume justifies it.
8. Institute a weekly pruning cadence with hard cut-offs — e.g., exclude placements with
   CTR >2% and zero conversions (accidental-click/fraud signature) — and log every
   verdict so decisions survive team turnover.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Placement reports | Google Ads "Where ads showed", DV360 inventory report | Weekly exports are the core evidence base |
| Authorized-path checks | ads.txt / app-ads.txt / sellers.json review | Manual or crawler-based; unauthorized = out |
| Media-quality flags | IAS, DoubleVerify quality reports | MFA, IVT, and brand-safety incident data |
| Traffic-quality context | SimilarWeb, SEMrush | Sanity-check "premium" site claims before allowlisting |
| Exclusion management | Google Ads account-level exclusions, DV360 inventory lists | Centralize; never scatter exclusions per campaign |
| Verdict log | Google Sheets | Version the allowlist; record evidence per verdict |

## Example AI Prompt

```text
You are a display placement auditor. Analyze this placement report for {BRAND}
(campaign: {CAMPAIGN NAME}, period: {DATE RANGE}).

Attached: {PLACEMENT REPORT EXPORT / IAS-DV QUALITY FLAGS}.
Brand-safety stance: {LOW / MEDIUM / HIGH RISK TOLERANCE}. Keep/exclude thresholds:
CTR {X}% / viewability {Y}% / CPA {Z}.

Deliver:
1. Verdict table: placement | type (web/app, managed/exchange) | spend share | CTR |
   viewability | verdict (keep / watch / exclude) with one-line evidence.
2. MFA and app-spam suspects: what pattern triggered each flag.
3. Recommended exclusion architecture: account-level sites, category exclusions, topic
   and keyword negatives.
4. Allowlist expansion candidates with ads.txt verification status.
```

## Edge Cases & Guardrails

- High CTR is not automatically good — 2%+ CTR with zero conversions usually means
  accidental clicks or fraud, not interest; investigate before celebrating.
- News and user-generated inventory requires an explicit brand-safety stance plus
  category exclusions before any allowlisting; "premium" branding is not verification.
- ads.txt is table stakes but not fraud-proof — verify app-ads.txt and sellers.json to
  catch app fraud and reseller chains.
- Do not over-narrow: a fully managed-only program loses reach economics; balance
  allowlists against a curated, well-excluded open exchange.
- Prune by evidence, not superstition — excluding on CPA with tiny sample sizes kills
  future winners; require a minimum impression threshold before verdicts.
- Keep exclusions centralized at account level; scattered per-campaign lists drift and
  leave holes open.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Spend in verified/planned placements | >90% | Majority of impressions on unplanned domains |
| MFA share of impressions | <5% | >10% or rising month over month |
| Managed vs open-exchange CTR premium | Managed ≥1.5x open | No difference — allowlist adds nothing |
| Viewability on kept placements | >70% | <60% despite pruning |
| Weekly pruning cadence adherence | 100% of weeks during flights | Reviews skipped while spend runs |

## Handoffs

- → **display-programmatic-buying:** deliver the cleaned inventory list and PMP/allowlist
  targets for line-item construction.
- → **display-viewability-optimization:** hand over placement-level viewability data so
  quality fixes target the right shelves.
- → **display-performance-reporting:** log exclusion and allowlist changes with dates so
  CTR/CPA shifts can be attributed to inventory changes.
- → **remarketing-retargeting-agent:** share the exclusion architecture — retargeting
  campaigns inherit the same brand-safety floor.
- ↑ **display-advertising-agent:** escalate active brand-safety incidents (ads next to
  harmful content, fraud bursts) immediately with evidence attached.
