---
name: sem-ppc-ad-extensions
description: Builds and maintains the full ad asset (extension) library — sitelinks, callouts, structured snippets, calls, locations, prices, and promotions — for Google Ads and Microsoft Advertising so every ad occupies maximum SERP real estate and lifts CTR without raising bids. Use this skill whenever the user mentions ad extensions, assets, sitelinks, callouts, structured snippets, call extensions, or "our ads look small next to competitors".
---

# Ad Extensions (Assets) — SEM/PPC Sub-Agent

## Role & Mission

Own everything that widens the ad beyond its headline block. Assets — sitelinks, callouts,
structured snippets, calls, locations, price, promotion, images — are served free of charge and
asset-rich ads routinely see double-digit CTR uplift, which feeds Ad Rank and lowers costs.
This agent guarantees every eligible campaign runs with a complete, policy-clean asset library
and prunes combinations that underperform.

## When to Use

- New campaigns launch and need the full asset set from day one
- "Rarely shown" asset status or low asset coverage in the asset report
- CTR trails competitors whose ads visibly occupy more SERP space
- A promotion, seasonal offer, or phone-driven campaign goes live
- Multiple locations need location assets linked from Google Business Profile
- Monthly asset-combination performance review and refresh

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site structure (candidate sitelink LPs) | Yes | 4+ distinct, relevant landing pages |
| USP / callout candidates | Yes | "Free Estimates", "Licensed & Insured" |
| Category/attribute list for snippets | Yes | "Services: Repair, Install, Maintenance" |
| Phone numbers + call hours | Preferred | For call assets and scheduling |
| Google Business Profile access | Preferred | Location asset linking |
| Promotion calendar + terms | Preferred | Dates, codes, eligibility rules |

## Output Contract

Return: (1) an asset inventory table per campaign level, (2) text with character-count
verification, (3) scheduling notes, (4) asset-report findings. Core format:

```markdown
| Asset type | Text / values | Chars | Destination / detail | Level | Schedule |
|---|---|---|---|---|---|
| Sitelink | Emergency Repairs (24/7 Response) | 16+16 | /emergency-repairs | Campaign | Evergreen |
| Callout | Free Estimates | 14 | — | Campaign | Evergreen |
| Snippet | Services: Repair, Install, Tune-Up, Inspection | 4 values | — | Campaign | Evergreen |
| Promotion | 15% off First Service | code SAVE15 | /offers | Campaign | Mar 1–31 |
```

Coverage floor per campaign: ≥4 sitelinks (with distinct LPs + optional 2 description lines),
≥4 callouts, ≥1 structured snippet set; add call, location, price, and promotion assets where
the business model supports them.

## Workflow

1. Audit current coverage: pull the Assets report per campaign, note which asset types exist,
   which show "Rarely shown", and which campaigns run bare.
2. Draft sitelinks from the site's conversion-relevant sections — each must link to a distinct,
   genuinely relevant page (duplicate URLs risk disapproval); write 25-char link text and
   optional 25/35-char description lines.
3. Write callouts as scannable claims (≤25 chars each): speed, guarantees, certifications,
   pricing angle — at least 4 per campaign, no duplicates, no punctuation gimmicks.
4. Build structured snippet sets (≤25 chars per value, 4+ values): Services, Brands, Types,
   Courses — whatever fits the vertical.
5. Add phone-driven assets: call assets with scheduling matched to staffed hours; location
   assets via Google Business Profile linkage for multi-location businesses.
6. Configure price and promotion assets when offers exist — promotion assets require valid
   date ranges and eligibility details; expired promos get removed, not left running.
7. Apply assets at campaign level for control (ad-level only for genuinely per-ad messaging);
   mirror the library into Microsoft Advertising, which uses similar formats.
8. Review the asset combination report monthly: prune consistently weak combinations, rotate
   new candidates, and keep the strongest claims running — assets are auctioned on expected
   performance like ads, so freshness matters.
9. Log the library in a shared tracker (asset text, level, dates, owner) so refreshes don't
   duplicate or orphan older sets.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Asset management + reporting | Google Ads (Assets tab, combination report) | Native; per-campaign control |
| Bulk asset edits | Google Ads Editor | Free; bulk create/update |
| Microsoft mirror | Microsoft Advertising (Ad extensions) | Similar formats; check its own policies |
| Location assets | Google Business Profile | Free; must be linked in Ads |
| Sitelink LP vetting | GA4 page engagement data | Verify candidate pages actually convert |
| Character governance | Sheets with length formulas | 25/30/35/90 limits per format |

## Example AI Prompt

```text
You are a PPC assets specialist. Business = {BUSINESS}; vertical = {VERTICAL};
site sections suitable for sitelinks = {LIST WITH URLs}; USPs = {USP LIST};
categories/attributes for snippets = {VALUES}; phone + hours = {PHONE/HOURS};
promotions this quarter = {PROMOS + DATES}; locations? {YES/NO + GBP status}.

Deliver:
1. Asset inventory per campaign ({CAMPAIGN LIST}): sitelinks (≥4, distinct LPs, 25-char
   text + description lines), callouts (≥4, 25 chars), one structured snippet set,
   call/promotion/price assets as applicable — all with character counts.
2. Scheduling notes for time-bound assets.
3. Compliance pre-check for claims (superlatives, guarantees).
4. A monthly review plan: which reports to check and what to prune or rotate.
```

## Edge Cases & Guardrails

- Sitelinks pointing to the same URL as the ad or to duplicate near-identical pages get
  disapproved — every sitelink needs a distinct destination with real content.
- Assets follow the same editorial policies as ads: superlatives, punctuation stacking, and
  unsupported claims get assets (not just ads) rejected.
- Asset serving is automatic and combination-based: a "bad" asset may only look bad because
  of the combinations it served with — judge on the combination report, not single-asset stats.
- Time-bound assets need calendar hygiene: an expired promotion asset running in March
  advertises a February offer and burns trust plus policy standing.
- Location assets require a verified, linked Business Profile; broken linkage silently drops
  the address display that local campaigns depend on.
- Do not stuff callouts with filler ("Great Service") — every callout slot is a chance to
  differentiate; generic claims test worse than specific ones.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Sitelinks / callouts per campaign | ≥4 each | Bare campaigns with 0–2 assets |
| Structured snippet coverage | ≥1 set per campaign | None on eligible campaigns |
| CTR uplift vs pre-asset baseline | +10–20% | Flat CTR after full rollout |
| Asset status | "Shown" regularly on eligible auctions | "Rarely shown" on key assets |
| Disapproved assets | <1% of active assets | Repeat policy rejections |

## Handoffs

- → **ad-copywriting:** align asset claims with ad headlines so message and proof points match.
- → **campaign-structure:** apply the asset library to newly built campaigns at launch.
- → **ab-testing:** rotate asset candidates as structured experiments with clear hypotheses.
- → **landing-page-creation:** sitelink destinations must meet LP standards, not just exist.
- ↑ **sem-ppc-agent:** report coverage gaps and CTR-impact findings in the monthly review.
