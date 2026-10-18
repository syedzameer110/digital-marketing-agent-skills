---
name: sem-ppc-ad-copywriting
description: Writes responsive search ads for Google Ads and Microsoft Advertising that win the click — 15 headlines and 4 descriptions per RSA with keyword insertion, benefit-led CTAs, deliberate pinning, and policy-safe claims — engineered for ad strength and CTR. Use this skill whenever the user mentions ad copy, RSAs, headlines, descriptions, ad text, low CTR, ad strength, ad disapprovals, or "our ads aren't getting clicks".
---

# Ad Copywriting — SEM/PPC Sub-Agent

## Role & Mission

Own every word shown in the ad slot. The output is policy-compliant responsive search ad sets
that match the searcher's query language, promise the landing page's actual offer, and win the
expected-CTR half of Quality Score. In a search auction, the highest bidder doesn't win — the
highest Ad Rank does, and ad relevance + expected CTR are the copy-controlled components.

## When to Use

- New campaigns or ad groups need launch-ready RSA sets
- CTR sits below 3% on non-brand search or ads lose impression share to competitors
- Ad strength shows "Poor" or "Average" across the account
- A new offer, promotion, USP, or price point needs to hit the SERP fast
- Quarterly creative refresh before fatigue shows in declining CTR
- Microsoft Advertising mirror needs copy adapted to its formats

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Ad group themes + top keywords | Yes | From campaign-structure |
| USPs / differentiators (3–5) | Yes | Sales team, reviews, product team |
| Offers / promotions to feature | Preferred | "$0 inspection", "Free shipping" |
| Brand voice + compliance rules | Preferred | Legal claims constraints, style guide |
| Landing page URLs + on-page promises | Yes | Message match source of truth |
| Competitor ads on the target SERPs | Optional | SpyFu / Semrush ad history, manual SERP check |

## Output Contract

Return per ad group: (1) an RSA set — up to 15 headlines (≤30 chars) and 4 descriptions (≤90
chars) — with pinning recommendations, (2) display path suggestions, (3) rationale notes, (4)
policy pre-check. Core format:

```markdown
| # | Headline (≤30) | Role | Pin |
|---|---|---|---|
| 1 | 24/7 Emergency Plumbing | Keyword/need match | H1 |
| 2 | Licensed Austin Plumbers | Local trust | — |
| 3 | $0 Service Call This Month | Offer | — |

| # | Description (≤90) | Role |
|---|---|---|
| 1 | Burst pipe? Licensed plumbers on-call 24/7. Upfront pricing. Call now, 60-min response. | Proof + CTA |
```

## Workflow

1. Read the SERP for the ad group's core terms: capture the top 3 competitor headlines, their
   offers, and the language real queries use — match the demand's vocabulary, not the brand's.
2. Extract 3–5 differentiators from inputs (speed, guarantee, price, certification, selection)
   and rank which one the target intent cares about most.
3. Write headlines across required roles: keyword-rich (drives ad relevance), benefit,
   offer/promo, trust/proof, CTA, and brand. Vary structure — combinations are what RSA serves.
4. Use keyword insertion sparingly ({KeyWord:Emergency Plumber}) on volatile themes; never let
   defaults read generic if the insertion fails.
5. Write 4 descriptions that pair proof with action: one offer-led, one trust-led, one
   benefit-list, one CTA-led. Include one concrete number or guarantee where true.
6. Pin deliberately and minimally: pin the brand or compliance-mandatory line only; over-pinning
   caps combinations and crashes ad strength.
7. Run the policy pre-check: punctuation, caps, superlatives ("best" needs third-party proof),
   restricted claims for finance/health, destination mismatch.
8. Set display paths (e.g., /emergency/plumber) that echo the keyword; confirm final URL matches
   the LP promise (message match).
9. Log the variants into the ab-testing backlog and hand off with the hypothesis for each.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| RSA authoring + ad strength | Google Ads UI, Google Ads Editor | Free; Editor for bulk |
| Character limit checks | Editor preview, Sheets formulas | 30/90 limits are hard fails |
| Competitor ad libraries | SpyFu, Semrush Ads History | Paid; years of ad version history |
| Microsoft mirror | Microsoft Advertising Editor | Supports RSAs; check its ad strength |
| Copy testing backlog | Sheets + ab-testing agent workflow | Track hypothesis, launch date, result |

## Example AI Prompt

```text
You are a PPC ad copywriter. Write one responsive search ad set for this ad group:
theme = {AD GROUP THEME}; top keywords = {KEYWORDS}; audience/intent = {INTENT}.
USPs: {USP LIST}. Offer: {OFFER}. Landing page promise: {LP URL + headline}.
Brand voice: {VOICE}. Compliance constraints: {RULES}.

Deliver:
1. 15 headlines, each ≤30 characters, covering: keyword-rich, benefit, offer, trust, CTA,
   brand. Mark character counts.
2. 4 descriptions, each ≤90 characters, proof + CTA.
3. Pinning recommendation (minimal) and display path suggestion.
4. Policy pre-check notes for any claim used.
Rules: mirror the searcher's wording, promise only what the landing page shows, and vary
sentence structure so RSA combinations stay meaningful.
```

## Edge Cases & Guardrails

- Character limits are enforced at 30/90 — near-limit strings get truncated in some
  combinations; keep 2–3 characters of buffer on key headlines.
- Superlatives and unverifiable claims ("#1 rated") trigger disapprovals unless the landing
  page displays third-party proof.
- Never promise what the LP doesn't show: destination mismatch is a policy risk and quietly
  destroys conversion rate and LP experience scores.
- RSA "ad strength" is a diagnostic, not a goal — forcing "Excellent" with filler words hurts
  more than a "Good" ad with sharp messaging.
- Do not inject the competitor's brand name into copy (trademark policy) and avoid gimmick
  punctuation ("Click here!!!").
- Refresh before fatigue: declining CTR over 6–8 weeks on stable impressions signals creative
  decay, not seasonality.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CTR, non-brand search | 3–6% | <2% after 4+ weeks |
| CTR, brand search | 10%+ | <5% — brand defense is failing |
| Ad strength "Good/Excellent" | ≥80% of ad groups | Majority "Average/Poor" |
| Unique headlines used per RSA | ≥8 of 15 slots filled | 3–4 near-duplicate headlines |
| Disapproved ads | <1% of active ads | Repeated policy strikes |
| CTR trend after refresh | +10–20% vs old set | Flat or negative lift |

## Handoffs

- → **landing-page-creation:** deliver headline promises so the LP mirrors them (message match
  drives both CVR and LP experience).
- → **ab-testing:** log each variant with its hypothesis for the experiment queue.
- → **ad-extensions:** align sitelink/callout language with the ad's claims.
- → **quality-score-optimization:** expected-CTR fixes route here for re-measurement.
- ↑ **sem-ppc-agent:** escalate account-level policy or trademark issues.
