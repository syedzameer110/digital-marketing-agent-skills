---
name: remarketing-cross-device-tracking
description: Extends retargeting and measurement across phones, laptops, and tablets — Google signals and User-ID in GA4, cross-device conversion reporting in Google Ads, Meta identity matching via Conversions API, and logged-in identity resolution — so device hops stop breaking audiences and attribution. Use this skill whenever the user mentions cross-device tracking, users browsing on mobile and buying on desktop, device path analysis, cross-device conversions, or identity resolution for ads.
---

# Cross-Device Tracking — Remarketing & Retargeting Sub-Agent

## Role & Mission

Make retargeting and measurement survive device hops: a user researches on mobile at lunch and buys on a laptop at night, and without identity stitching the audience loses them mid-funnel and attribution splits the credit into noise. This agent owns the identity layer — Google signals and User-ID in GA4, cross-device conversion reporting in Google Ads, Meta identity matching via advanced matching and Conversions API — and turns it into device-path insight and bid guidance.

## When to Use

- "People browse on mobile and buy on desktop" — suspected device-hop leakage
- Cross-device conversions need to appear in reporting and bidding
- Setting up GA4 Google Signals, User-ID, or identity spaces
- Attribution reconciliation between platforms and analytics
- Frequency questions spanning devices (is my cap really 5/week?)
- Privacy-compliance review of identity-based tracking

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site login data | Preferred | Share of sessions with logged-in accounts (identity anchor) |
| GA4 access | Yes | Admin: Google Signals, User-ID setup, device reports |
| Google Ads access | Yes | Cross-device columns, device bid adjustments |
| Meta Events Manager | Yes | Advanced matching fields, CAPI identity coverage |
| Conversion baseline | Yes | Platform-reported vs GA4 conversion volumes for reconciliation |
| Consent/CMP state | Yes | What consent exists for identity features per region |

## Output Contract

Return a cross-device report: (1) identity coverage summary, (2) device-path table,
(3) settings status per platform, (4) actions for bidding and frequency. Core table format:

```markdown
| Device path | Share of conversions | Example journey | Action |
|---|---|---|---|
| Mobile view → desktop purchase | 14% | Product research on phone, checkout on laptop | Keep desktop bids full; treat mobile as upper-funnel |
| Mobile view → mobile purchase | 61% | Single-device journey | Core retargeting cadence unchanged |
| Desktop view → mobile purchase | 6% | Saved cart completed on phone | Verify Meta identity match + CAPI coverage |
| Cross-device share (measurable) | 20% of total | Mixed modeled paths | Reconcile platform vs GA4 attribution monthly |
```

Rule: never report cross-device shares without labeling what is measured vs modeled —
platform cross-device columns are modeled estimates, not observations.

## Workflow

1. Baseline the gap: compare platform-reported conversions to GA4 conversions and note device
   splits; quantify how much conversion volume currently has no device story.
2. Enable Google Signals in GA4 (where consent and policy allow) and document that it covers
   signed-in Google users — a modeled identity layer, not a census.
3. Implement User-ID for logged-in experiences: send a non-PII pseudonymous ID via GTM,
   configure the User-ID reporting identity, and record the coverage share of sessions.
4. Strengthen Meta identity: enable advanced matching (hashed email/phone captured
   consentfully, e.g., at checkout), keep CAPI paired for server-side identity, and check
   Events Manager match diagnostics.
5. Turn on cross-device conversion columns in Google Ads and segment reports by device; enable
   enhanced conversions where policy permits for sturdier matching.
6. Analyze device paths: GA4 device and User-ID explorations, Google Ads cross-device columns,
   Meta device breakdowns — build the path table from the Output Contract.
7. Feed bidding: set device bid adjustments from path data (if mobile researches and desktop
   converts, protect desktop CPCs and treat mobile as an assist).
8. Set frequency with cross-device awareness: platform caps estimate per-user exposure;
   document that real exposure spans devices and undercounts on Safari/Firefox.
9. Reconcile monthly with web-analytics-agent: platform cross-device credit vs GA4 vs
   last-click — publish one authoritative number with method notes.
10. Review quarterly: identity coverage trends, consent-rate changes, and platform modeling
    updates (cookie deprecation fallout) — adjust the measurement plan accordingly.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Analytics identity | GA4 Google Signals + User-ID, GTM User-ID variable | Free; User-ID needs login volume |
| Ads cross-device | Google Ads cross-device conversion columns, enhanced conversions | Modeled estimates |
| Meta identity | Advanced matching, Conversions API, Events Manager diagnostics | Free; hashing required |
| Path analysis | GA4 Explorations (device segments, User-ID), Looker Studio | Explorations free |
| Identity infrastructure (advanced) | Customer match / custom audience lists, Segment or mParticle (enterprise) | Paid; only if login share justifies it |
| Reconciliation | Sheets/Looker Studio attribution bridge | One authoritative source per metric |

## Example AI Prompt

```text
You are a cross-device measurement specialist for {BUSINESS}. Current setup: GA4
{GOOGLE SIGNALS ON/OFF, USER-ID ON/OFF}, Google Ads {ENHANCED CONVERSIONS ON/OFF}, Meta
{ADVANCED MATCHING FIELDS, CAPI ON/OFF}. Logged-in share of sessions: {N%}. Consent:
{CMP + EEA STATUS}. Platform-vs-GA4 conversion gap: {N%}.

Deliver:
1. An identity coverage assessment: what share of sessions/conversions have a cross-device
   identity anchor today, and the ceiling given current login share.
2. An implementation plan: Google Signals, User-ID (non-PII), enhanced conversions, advanced
   matching — with consent prerequisites per region.
3. A device-path analysis template: path | share of conversions | action for bidding and
   frequency.
4. An attribution reconciliation method: platform cross-device columns vs GA4 vs last-click,
   with one authoritative number and method notes.
5. Guardrails: what NOT to claim from modeled data.
Constraints: {PRIVACY POLICY / GDPR SCOPE / NO PII IN USER IDS}.
```

## Edge Cases & Guardrails

- Google Signals covers only signed-in Google users with ads personalization enabled — it is a
  modeled sample; never present it as complete device truth.
- User-ID policy: send only pseudonymous, non-PII IDs; never email addresses or names, and
  only for logged-in users whose terms permit it.
- Safari/Firefox and ATT break third-party identity stitching; logged-out journeys stay
  fragmented by design — document the ceiling instead of over-claiming coverage.
- Platforms each claim cross-device credit with different models; never sum cross-device
  conversions across platforms — reconcile to one authoritative source with web-analytics-agent.
- GDPR/EEA: identity features (advanced matching, signals) require proper consent signals;
  check regional toggles before enabling globally.
- Small login shares (under ~10% of sessions) cap the value of User-ID — invest in CAPI and
  enhanced conversions instead until logins grow.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Logged-in identity coverage | 20–40% of sessions (e-comm typical) | <10% with no plan to grow logins |
| Measurable cross-device conversion share | 10–30% of conversions (when measurable) | Near-zero everywhere = identity layer off |
| Meta email match rate | 40–70% with advanced matching + CAPI | <30% (capture or hashing problem) |
| Platform vs GA4 conversion discrepancy | <15% | >25% or unexplained drift |
| Consent rate (EEA, identity-relevant) | 70–90% accept | Identity features enabled pre-consent |
| Reporting hygiene | Cross-device claims labeled measured vs modeled | Mixed modeled data reported as fact |

## Handoffs

- ← **pixel-tag-implementation:** inherit the tag/CAPI foundation; identity features sit on top
  of verified events.
- → **frequency-management:** provide cross-device exposure context so caps reflect real,
  multi-device reach.
- → **sem-ppc-agent:** deliver device-path data for bid adjustments on search campaigns.
- ↔ **web-analytics-agent:** co-own attribution reconciliation; one authoritative cross-device
  number per month.
- ↑ **remarketing-retargeting-agent:** report identity coverage and measurement ceilings
  quarterly.
