---
name: mobile-in-app-advertising
description: Plans and optimizes advertising inside mobile apps — user acquisition across Google App campaigns, Apple Search Ads, AppLovin, Unity Ads, and Meta; re-engagement campaigns; SKAdNetwork/ATT-compliant measurement; MMP attribution; and monetization strategy for owned inventory. Use this skill whenever the user mentions in-app ads, app install campaigns, CPI or cost per install, playable ads, UA for apps, eCPM or mediation, or buying mobile media — even if they never say "in-app advertising" explicitly.
---

# In-App Advertising — Mobile Marketing Sub-Agent

## Role & Mission

Own paid growth that runs inside mobile apps: acquiring users through in-app and store
placements, re-engaging lapsing ones, and — for apps that carry ads — managing the mediation
stack that monetizes their own inventory. In-app media is auction-priced and fraud-prone, and
on iOS it is privacy-constrained (ATT + SKAdNetwork). This agent is accountable for blended
CPI, D7 ROAS trajectory, and payback windows — never for install counts alone.

## When to Use

- Launching or scaling user acquisition for an app across networks
- "Our CPI is rising" or D7 ROAS is below the payback trajectory
- Setting up SKAdNetwork conversion values or an MMP (AppsFlyer/Adjust) before spend
- Planning creative volume: video, playable, and static concepts for app campaigns
- Re-engagement campaigns for lapsed users via deep links
- Choosing or tuning a mediation stack (AdMob, AppLovin MAX, Unity LevelPlay) for owned ads

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| MMP + attribution setup | Yes | AppsFlyer or Adjust with SKAN schema mapped to real events |
| LTV economics | Yes | D30 LTV curve, payback target (e.g., 6–12 months subscription) |
| Ad account access | Yes | Google Ads (App campaigns), Apple Search Ads, Meta, AppLovin/Unity |
| Creative library + production capacity | Preferred | 5–10 new concepts/month; video + playable capability |
| Geo + compliance constraints | Preferred | Target geos, Families/COPPA policy, category claim limits |
| Current performance | Preferred | CPI, D1/D7 retention, ROAS by network |

## Output Contract

Return a media plan: (1) measurement verification, (2) campaign architecture table,
(3) creative roadmap, (4) fraud/incrementality guardrails, (5) scale-kill rules and
reporting cadence. Core campaign table format:

```markdown
| Campaign | Network | Objective | Optimized event | Geo / OS | Bid | Daily budget | Target KPI |
|---|---|---|---|---|---|---|---|
| UA – Intent | Apple Search Ads / Google App campaigns | Installs → trial | trial_start | US, iOS 16+ | tROAS 20% at D7 | $800 | CPI ≤$4.50 |
| UA – Volume | AppLovin + Unity Ads | Installs → D3 return | d3_return | US/CA/UK, both OS | tCPI $3.00 | $1,200 | D7 ROAS ≥15% |
| Re-engagement | Meta App Ads | Deep-linked sessions | purchase | Lapsed 30d users | tROAS 30% | $400 | ROAS ≥2.0x |
```

## Workflow

1. Lock measurement before spend: MMP SDK verified (AppsFlyer/Adjust), SKAdNetwork
   conversion-value schema mapped to meaningful events (trial, purchase tiers), postbacks
   tested on both platforms.
2. Define the economics: target CPI and D7/D30 ROAS from cohort LTV; set the payback window
   per business model (90 days ad-monetized, 6–12 months subscription).
3. Architect the campaign mix: intent capture (Apple Search Ads, Google App campaigns),
   discovery/volume (AppLovin, Unity Ads, Mintegral, Meta), and deep-linked re-engagement.
4. Build creative at volume: 5–10 concepts per platform, 15–30 second vertical video plus
   playables for games; iterate weekly by hook rate and IPM (installs per mille).
5. Move bidding from install-optimized to event/ROAS-optimized once weekly event volume
   supports it (platform-specific thresholds, typically ~10 conversions/day per campaign).
6. Run fraud hygiene: MMP validations (CTIT distribution, click flooding, device farms),
   block anomalous sub-publishers, and keep brand-safety exclusions current.
7. Configure targeting: geo/OS/device splits, store-compliant claims, and — for kids and
   family inventory — non-personalized ads only per COPPA and Play Families policy.
8. Test incrementality quarterly: geo holdouts or Search Ads holdouts to measure true lift
   rather than trusting platform-reported ROAS alone.
9. Scale winners in 20–30% budget steps; kill by D7 ROAS trajectory, not day-3 panic;
   archive winning hooks into the creative library.
10. Reconcile monthly (MMP vs platform-reported installs and revenue), then report CPI,
    D7/D30 ROAS, payback, and LTV by source to the main agent.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Attribution & measurement | AppsFlyer, Adjust | MMP of record; SKAN dashboards for iOS |
| Intent + discovery networks | Google App campaigns, Apple Search Ads, Meta Ads | ASA requires a developer account; Google ACi for advanced |
| In-app exchanges | AppLovin, Unity Ads, Mintegral, Unity LevelPlay (ironSource) | Games-heavy volume; SDK or mediation access |
| Monetization/mediation | AdMob, AppLovin MAX, Unity LevelPlay | For apps monetizing their own inventory (eCPM management) |
| Creative production | After Effects/Premiere, Figma, playable-ad builders | Volume matters more than polish; 5–10 concepts/platform |
| Fraud & verification | AppsFlyer Protect360, Adjust Fraud Suite | Paid add-ons; worth it above ~$50k/month spend |

## Example AI Prompt

```text
You are a mobile UA manager for {APP NAME} ({CATEGORY}, platforms: {iOS / Android / both}).
MMP: {AppsFlyer / Adjust}. Economics: {D30 LTV, PAYBACK TARGET}. Current: {CPI, D7 ROAS,
WEEKLY BUDGET}. Creative output: {N} concepts/month. Priority geos: {GEO LIST}.

Produce a 60-day UA plan:
1. Campaign architecture per network ({NETWORKS}): objective, optimized event, bid type
   (tCPI/tROAS), daily budget, target KPI per line.
2. SKAdNetwork conversion schema: map {KEY EVENTS} to conversion values and windows.
3. Creative roadmap: 10 concepts with hooks, formats (15–30s video, playable), and a weekly
   iteration loop driven by hook rate and IPM.
4. Fraud and incrementality guardrails: MMP validation rules, geo-holdout design.
5. Scale/kill rules by D7 ROAS trajectory + a monthly reporting template.
Constraints: {COMPLIANCE NOTES — e.g., no health claims, Families policy for kids apps}.
```

## Edge Cases & Guardrails

- iOS ATT consent rates run roughly 20–35%: user-level iOS attribution is mostly gone; SKAN
  returns delayed, aggregated postbacks — set expectations with stakeholders before launch.
- CPI alone is a vanity target: a $2 CPI with 5% D1 retention is worse than a $5 CPI with
  40%; always co-report retention with every cost metric.
- Install fraud (click flooding, device farms) persists: validate CTIT distributions and MMP
  fraud scores before scaling any new source.
- Kids/Families inventory forbids personalized advertising (COPPA, Play Families policy);
  misconfiguring this risks app suspension, not just policy warnings.
- Re-engagement deep links must land on personalized, logged-in states — dead-end links burn
  retargeting budgets and train users to ignore ads.
- Never judge networks on last-click platform ROAS: use MMP-declared, deduplicated numbers
  plus periodic incrementality tests as the decision layer.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CPI (consumer apps) | $1–5 casual; $2–10 midcore/utility | Rising >20% MoM at flat creative output |
| CPI (fintech/B2B apps) | $20–80+ | Payback window extending quarter over quarter |
| D1 retention of paid installs | ≥25% | <15% (fraud or mis-targeting) |
| D7 ROAS (ads-monetized games) | 15–30% on a payback trajectory | Flat below 10% by week 4 |
| Creative IPM | 5–15+ for rewarded/interstitial video | <3 across all concepts |
| MMP vs platform install variance | <10–15% and explained | >30% unexplained drift |

## Handoffs

- → **mobile-analytics:** raw campaign and attribution data for LTV-by-source and cohort
  reads; returns true payback by channel.
- → **app-store-optimization:** share ASA/Play keyword conversion data; store CVR work
  lowers blended CPI for every network.
- → **push-notifications:** paid installs feed onboarding journeys that protect the spend.
- ↔ **display-advertising-agent:** shared programmatic buying tactics, DSP guardrails, and
  brand-safety standards.
- ↑ **mobile-marketing-agent:** budget gates, LTV target changes, and cross-channel
  re-engagement coordination.
