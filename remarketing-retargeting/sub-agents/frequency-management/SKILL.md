---
name: remarketing-frequency-management
description: Caps, monitors, and rotates retargeting exposure so warm audiences convert instead of tuning out — platform frequency caps, cross-campaign overlap consolidation, fatigue detection via CTR decay, creative rotation schedules, and segment-tiered exposure rules. Use this skill whenever the user mentions frequency capping, ad fatigue, banner blindness, seeing ads too often, retargeting complaints, creative rotation, or falling CTR on warm audiences — even if they never say frequency management.
---

# Frequency Management — Remarketing & Retargeting Sub-Agent

## Role & Mission

Control how often warm audiences see retargeting ads so they convert instead of tuning out. Frequency is the channel's central paradox: enough exposure drives the 2–5x CVR lift, but warm audiences are small and premium-priced — over-serving burns budget, depresses CTR, and turns the brand into the one people complain about. This agent owns caps, overlap consolidation, fatigue detection, and the creative rotation calendar.

## When to Use

- "Customers say they see our ads everywhere" or social complaints
- Frequency climbing week over week while CTR falls
- Multiple campaigns/ad sets hitting the same audience (stacked frequency)
- Setting caps at launch for any new retargeting campaign
- Creative refresh planning and fatigue investigations
- Pre-peak-season exposure planning for small pools

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Frequency reports | Yes | Meta Ads Manager, Google Ads (Display/Demand Gen) frequency metrics |
| Campaign/audience map | Yes | Which campaigns serve which audiences, budgets, overlaps |
| Creative inventory | Yes | Live variants per segment and their launch dates |
| CTR/CVR baselines | Yes | 4–8 week baseline per segment for decay math |
| Cap settings access | Yes | Ad set/campaign level cap permissions on each platform |
| Sentiment signals | Preferred | Hide-ad rates, comments, survey verbatims |

## Output Contract

Return a frequency report: (1) summary verdict per segment, (2) the frequency table,
(3) cap/rotation actions, (4) escalation flags. Core table format:

```markdown
| Segment / campaign | Platform | Avg freq (7d) | Cap setting | CTR trend | Action |
|---|---|---|---|---|---|
| Cart Abandoners 7d | Meta | 5.2 | 6/week (ad set) | Stable | Hold |
| Product Viewers 14d | Google Display | 9.4 | Uncapped, 2 stacked campaigns | -28% vs baseline | Cap 4/week + consolidate campaigns |
| Purchasers 180d | Meta | 7.1 | None | -35% | Exclude purchasers; rebuild cross-sell set |
```

Rules: every funded segment carries an explicit cap; any segment with CTR decay above 20%
from baseline gets a rotation or cap action within the week.

## Workflow

1. Pull 7-day and 30-day average frequency by campaign, ad set, and audience across all
   platforms — retargeting exposure stacks across campaigns, so read it combined, not per
   campaign.
2. Set tiered caps by intent heat: hot (cart abandoners, pricing viewers) 5–7/week; warm
   (product viewers) 3–5/week; cool (general visitors, cross-sell) 1–3/week.
3. Apply caps natively: Meta at ad-set level (or Reach & Frequency buying), Google
   Display/Demand Gen per campaign — note Google caps do not span campaigns, so stacking is
   structural.
4. Consolidate overlapping campaigns: merge ad sets chasing the same audience; run one
   campaign per audience tier per platform so caps actually bind.
5. Install fatigue detection: compare weekly CTR and CVR to the 4–8 week baseline; flag decay
   above 20%, and separate rising-CPM-with-flat-CTR (auction pressure) from creative fatigue.
6. Run the rotation calendar: refresh or swap creative every 2–4 weeks per tier; retire
   variants whose CTR decayed beyond 20% even if the calendar says otherwise.
7. Validate incrementality: keep a small holdout (excluded cell) on the biggest segments and
   read conversion-per-impression lift, not just platform ROAS — frequency without
   incrementality is expensive branding.
8. Watch sentiment: hide-ad rates, negative comments, and organic complaints; tighten caps
   when sentiment sours even if CTR holds.
9. Re-audit monthly: cap adherence, overlap changes after new launches, and cross-device
   undercounting (Safari/Firefox undercount users, so real exposure is higher than reported).

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Meta frequency + caps | Meta Ads Manager frequency metrics, ad set caps / R&F buying | Free with ad account |
| Google caps + monitoring | Google Ads frequency settings (Display/Demand Gen), Google Ads Scripts | Scripts free; automate weekly pulls |
| Cross-platform view | Looker Studio + Sheets dashboard | Combined frequency needs manual stitching |
| Fatigue analytics | Platform CTR trends, GA4 engaged-session CVR by audience | Baselines from your own history |
| Sentiment | Meta hide-rate reporting, comment monitoring, Brandwatch/Mention | Mention has free-tier alerts |
| Holdout testing | Geo/audience holdouts via campaign exclusions | Cheap incrementality for small pools |

## Example AI Prompt

```text
You are a retargeting frequency manager. Programs live on {META / GOOGLE / LINKEDIN}.
Current state per segment: {PASTE FREQUENCY + CTR + SPEND TABLE, 4-8 WEEKS}.
Creative inventory: {VARIANTS PER SEGMENT + LAUNCH DATES}. Known overlaps: {CAMPAIGNS
SHARING AUDIENCES}.

Deliver:
1. A frequency verdict per segment: healthy / at-risk / burning (vs a 3-7 per week band).
2. Cap recommendations by intent tier with exact platform mechanics (ad set vs campaign
   level, and where stacking persists).
3. A consolidation plan for overlapping campaigns.
4. A creative rotation schedule: what retires, what refreshes, trigger-based rules.
5. A simple holdout design to test incrementality on the biggest segment.
Constraints: {PEAK SEASON / POOL SIZE / BRAND SENSITIVITY}. Flag any segment where
reported frequency is likely undercounting (Safari/Firefox-heavy audiences).
```

## Edge Cases & Guardrails

- Google's frequency caps apply per campaign, not per account — two campaigns on one audience
  double the cap silently; consolidate before tuning numbers.
- Meta caps bind at the ad-set level; boosted posts and engagement campaigns sit outside your
  caps — coordinate with the social team.
- Safari and Firefox undercount users, so reported frequency understates real exposure for
  privacy-conscious segments — err conservative on caps.
- Frequency is not waste by default: judge with conversion-per-impression and holdout lift,
  not gut feel; high-consideration purchases tolerate 5–7/week, impulse tiers do not need it.
- Do not cap so low the pool never converts (below ~2/week on hot tiers starves the funnel) —
  the fix for fatigue is rotation and exclusion, not starvation.
- Frequency complaints on sensitive products (debt relief, health) escalate fast — cap those
  tiers at the bottom of the band and avoid urgency framing.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Combined average frequency | 3–7 per week | >10/week on any funded segment |
| CTR decay vs baseline | <10% per month | >20% decay at stable frequency |
| Impressions above 10x/week | <5% of impressions | Any audience averaging >10 |
| Hide/negative rate (Meta) | <0.5% of impressions | Rising alongside flat CTR |
| Holdout incremental lift | Retargeting lifts conversions vs holdout (read >1.5x as strong) | Lift near 1x = over-farming |
| Creative refresh cadence | Every 2–4 weeks per tier | Same creative live >8 weeks |

## Handoffs

- → **retargeting-ad-creation:** send refresh briefs and retirement dates on the rotation
  calendar.
- ← **audience-segmentation:** request overlap fixes and pool expansion when caps bind.
- → **display-advertising-agent / social-paid-social-ads:** coordinate exclusions so
  prospecting and retargeting do not stack on the same users.
- ↔ **cross-device-tracking:** reconcile undercounted cross-device exposure when reported
  frequency looks fine but fatigue appears.
- ↑ **remarketing-retargeting-agent:** escalate saturated pools (small audience, high caps,
  decay) as a budget-rebalance case.
