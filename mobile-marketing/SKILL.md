---
name: mobile-marketing-agent
description: Orchestrates the mobile marketing workflow: SMS campaigns, push notifications, app store optimization (ASO), in-app advertising, location-based marketing, QR code campaigns, and mobile analytics. Use this skill whenever the user wants to run text message campaigns, engage app users, improve app store rankings, market a mobile app, set up geofencing or geotargeting, bridge offline to online with QR codes, track app retention, or mentions TCPA consent, SMS open rates, or D1/D7/D30 retention — even if they never say "mobile marketing" explicitly.
---

# Mobile Marketing — Main Agent (Command Hub)

## Channel Overview

Mobile is the only marketing channel that lives in the customer's pocket, and it shows in
the numbers: over 90% of SMS messages are opened, most within minutes of delivery — compare
email's 20–25% opens spread over days. A consented SMS list is the fastest-acting owned
audience in marketing, and push notifications reach opted-in app users for near-zero marginal
cost. That immediacy cuts both ways: the same device hosts the customer's attention and the
regulatory exposure. Mobile is the most compliance-heavy channel in this library — TCPA in
the US (prior express written consent for marketing texts, quiet hours 8am–9pm recipient
local time), GDPR/ePrivacy consent in the EU, carrier filtering on top of both — so this hub
treats consent infrastructure as a first-class deliverable, never as paperwork. An SMS
program that wins the click but loses the lawsuit is a failed program.

Where does mobile win versus neighboring channels? On time-sensitive offers, physical-world
journeys (stores, events, packaging), and owned-audience reach with no algorithm between
you and the customer. It loses on deep-consideration, desktop-heavy B2B evaluations — route
those to email, SEO, and SEM — and it punishes frequency abuse faster than any other
carrier-mediated channel.

Strategy branches on one question: does the business have an app? App-first businesses own
rich engagement surfaces (push, in-app messages, deep links) and invest in ASO, paid user
acquisition, and D1/D7/D30 retention cohorts. No-app businesses (most retail, restaurants,
local services, B2B) still win on mobile through SMS plus web touchpoints, QR codes bridging
physical moments, and geotargeted ads. Time-to-results: SMS campaigns move within days, push
and lifecycle programs show lift in 2–6 weeks, in-app UA optimizes in 2–4 weeks, and ASO
compounds over 1–3 months. Costs: SMS runs $0.005–$0.03 per message at wholesale plus
platform fees; push is cheap at scale but requires the app; in-app media is auction-priced
(CPI $1–5 for consumer apps, far higher for finance/B2B). The unit economics are what make
or break the channel: message cost is trivial, so quality of consent and of targeting — not
volume — decides profitability.

## Agent Hierarchy

```text
mobile-marketing-agent (command hub)
└── sub-agents/
    ├── sms-campaigns/              → promotional & transactional texts, TCPA/CTIA guarded
    ├── app-store-optimization/     → ASO: keywords, metadata, creatives, ratings
    ├── push-notifications/         → opt-in lock-screen engagement & retention journeys
    ├── in-app-advertising/         → ads inside apps: UA, re-engagement, monetization
    ├── location-based-marketing/   → geofencing, geotargeting, geo-conquesting, visit lift
    ├── qr-code-campaigns/          → offline-to-online bridges with UTM discipline
    └── mobile-analytics/           → app usage, funnels, retention cohorts, attribution
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| sms-campaigns | Promotional or transactional texts, list growth, abandoned-cart, win-backs | Consent records, offer calendar, segments, platform access (Twilio/Attentive/Postscript/Tatango) | None (entry point); no send without documented consent |
| app-store-optimization | App launch, installs plateau, listing conversion or keyword gaps | Store listing URLs, keyword ranks (AppTweak/Sensor Tower), review sentiment (AppFollow), creative assets | mobile-analytics (baseline metrics) |
| push-notifications | App has an install base; engagement or D1/D7 retention slipping | SDK integration status (Firebase Cloud Messaging/OneSignal/Braze), segments/behavior events, deep-link map | mobile-analytics; app-store-optimization (install quality) |
| in-app-advertising | Buying installs/re-engagement inside other apps, or monetizing own inventory | MMP (AppsFlyer/Adjust), ad accounts, creative volume, CPI/ROAS targets | mobile-analytics (attribution before spend) |
| location-based-marketing | Store visits, geofenced triggers, radius-targeted ads, conquesting | Location list, consent flags, ad platform + footfall measurement | sms-campaigns or push-notifications (message layer) |
| qr-code-campaigns | Print, packaging, in-store signage, events; bridging offline to online | Destination URLs + UTM taxonomy, artwork specs, QR platform | None (parallel-safe) |
| mobile-analytics | Instrumentation, dashboards, funnel/retention reviews, attribution reconciliation | SDK access, event taxonomy, app builds, MMP + GA4 | None (entry point — feeds every other sub-agent) |

## End-to-End Workflows

### Workflow A — Omnichannel Retailer: Offline-to-Mobile Revenue Engine (weeks 1–8)

1. **mobile-analytics** sets the measurement foundation before any campaign: UTM taxonomy
   for every offline placement, GA4 + platform dashboards, and revenue attribution rules.
   Output: tracking plan + baseline dashboard.
2. **sms-campaigns** builds the consented list: TCPA-compliant opt-in language at checkout,
   GDPR double opt-in for EU contacts, and a welcome flow with a first-purchase offer.
   Output: consent architecture + welcome journey.
3. **qr-code-campaigns** bridges physical moments: dynamic QR codes (unique per placement)
   on receipts, shelf talkers, and packaging, each landing on the SMS opt-in page with full
   UTM discipline. Output: QR deployment matrix + tracking register.
4. **location-based-marketing** adds proximity pressure: geofenced ads around own stores and
   geo-conquesting near competitor locations, measured on store-visit lift.
   Output: location campaign plan + lift measurement design.
5. **push-notifications** covers the app install base: onboarding journeys and cart-hold
   triggers for users the SMS program cannot reach. Output: push opt-in rate + journey suite.
6. **sms-campaigns** runs the revenue calendar: abandoned-cart nudges at 1 hour, weekly
   offers inside quiet hours, frequency-capped at 2–4 promotional sends/month.
   Output: sends, CTR, opt-out rate, revenue per message.
7. **mobile-analytics** closes the loop monthly: opt-in growth, attributed revenue by
   placement, scan-to-opt-in rates. Decision: re-tune placements (steps 3–6) by ROI.

### Workflow B — App Launch & Install Quality Sprint (weeks 1–10)

1. **mobile-analytics** instruments before the first dollar of spend: event taxonomy
   (signup, activation, purchase), Firebase/Amplitude SDK, MMP with SKAdNetwork schema.
   Output: verified event stream + retention dashboard.
2. **app-store-optimization** maximizes organic conversion: keyword map, metadata rewrite,
   screenshot/video creative, ratings prompt strategy. Output: optimized listings.
3. **in-app-advertising** buys scale: Google App campaigns + Apple Search Ads for intent,
   AppLovin/Unity/Meta for volume — all optimized to activation events, not raw installs.
   Output: campaigns with CPI and D7 ROAS targets per network.
4. **push-notifications** protects the spend: pre-permission primer, D0–D7 onboarding
   journeys, deep-linked triggers tied to the activation event.
   Output: opt-in strategy + onboarding journey portfolio.
5. **qr-code-campaigns** bridges offline launch moments: posters, packaging, and event
   assets deep-link to the store listing or an install-attributed landing page.
   Output: QR deployment matrix with per-placement UTMs.
6. **mobile-analytics** reads D1/D7/D30 cohorts by source; low-retention sources are cut,
   winning keywords and creatives feed back to steps 2–3. Decision: reallocate budget to
   sources with the best retention-adjusted LTV. Cycle repeats monthly.

### Workflow C — Quarterly Retention & LTV Cycle (recurring)

1. **mobile-analytics** cohort review → identify churn-risk segments and highest-LTV sources.
2. **push-notifications** re-engagement journeys for churn-risk app segments.
   Output: win-back journey set with holdout measurement.
3. **sms-campaigns** VIP and replenishment flows for highest-LTV segments (SMS where push
   opt-in failed, consent permitting). Output: VIP calendar + revenue per message read.
4. **location-based-marketing** visit-frequency campaigns for lapsed in-store customers.
   Output: visit-lift study vs control.
5. **in-app-advertising** re-engagement campaigns deep-linking lapsing app users to
   personalized screens. Output: re-engagement ROAS by segment.
6. **mobile-analytics** measures retention lift and LTV movement; a quarterly compliance
   audit (consent records, quiet hours, STOP handling) closes the cycle before the next.
   Decision: keep, fix, or kill each retention lever based on incremental lift.

## KPI Dashboard

North-star metric: **mobile-attributed revenue per month** — last-touch SMS/push revenue plus
UA-attributed revenue, reconciled through the MMP and GA4. Engagement metrics are leading
indicators only; they never justify spend on their own.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| SMS click-through rate | Attentive/Postscript/Twilio | Weekly | 5–15% |
| SMS opt-out rate per campaign | SMS platform | Weekly | <2% (investigate above 2%) |
| SMS delivery rate | Platform + carrier logs | Weekly | ≥95% |
| SMS list growth (net) | SMS platform | Monthly | +5–10% per month |
| Push opt-in rate | OneSignal/Braze/FCM | Monthly | Android 40–70%, iOS 20–50% |
| Push CTR | Platform | Weekly | 0.5–2% (deep-linked triggers 2–5%) |
| Push delivery failure rate | Platform | Weekly | <2% |
| D1 / D7 / D30 retention | Amplitude/Mixpanel/Firebase | Weekly | D1 25–40%, D7 10–20%, D30 5–10% |
| Store listing conversion (view → install) | App Store Connect / Play Console | Monthly | 25–35% blended |
| Cost per install | AppsFlyer/Adjust | Weekly | $1–5 consumer; $20–80+ finance/B2B |
| Store-visit lift (geo campaigns) | GroundTruth/Google Ads | Monthly | +3–10% vs control |
| QR scan-to-action rate | QR platform + GA4 | Monthly | 10–30% of scans |
| SMS revenue per message (e-comm) | Platform + GA4 | Monthly | $0.10–$0.50+ |
| UA payback window | AppsFlyer/Adjust | Monthly | ≤90 days ads-monetized; ≤6–12 months subscription |
| Crash-free users | Firebase Crashlytics | Weekly | ≥99.5% |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $1,000–$2,500 | 50% SMS platform + message fees, 20% tools (analytics/ASO), 20% creative & print/QR production, 10% test reserve |
| $2,500–$7,500 | 40% lifecycle (SMS + push platform), 25% UA media (in-app + store ads), 20% tools, 15% creative |
| $7,500–$20,000 | 35% paid UA media, 30% lifecycle platforms, 20% tools/MMP, 15% creative + dev for deep links |
| $20,000+ | 40% paid UA, 25% lifecycle, 20% tools/data, 15% creative and engineering support |

Allocation principles:

- Consented SMS opt-ins and push tokens are compounding owned assets; media rents attention —
  fund list growth before acquisition spend.
- Compliance tooling (consent capture, quiet-hours enforcement, STOP handling, 10DLC
  registration) is a fixed cost of doing business, never a nice-to-have.
- Pay for measurement before media: an MMP plus dashboard stack costs a fraction of one week
  of unattributed spend.
- Reserve ~10% for structured tests: send times, creative concepts, offers, new placements.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| SMS/lifecycle strategy & compliance | In-house marketer | Brand voice and legal accountability stay internal |
| SMS platform ops & automation | In-house or platform CSM | Template work is repeatable; Attentive/Postscript offer managed services |
| ASO | Specialist freelancer/agency | Niche tooling (AppTweak, Sensor Tower) + store-policy fluency |
| In-app UA media | Agency or in-house paid buyer | Needs daily optimization across networks |
| Geofencing/footfall campaigns | Specialist agency | DSP access + validated visit-lift measurement |
| QR/print production | In-house designer or freelancer | Fast turnaround, low strategic risk |
| Analytics instrumentation | In-house dev + analyst | SDK work belongs with engineering; insight stays close to the business |

## Reporting Cadence

- **Weekly (in-house, 30 min):** sends, SMS CTR and opt-outs, push CTR and opt-in rate,
  CPI and D7 ROAS, D1 retention, delivery and crash incidents. Decision: pause failing
  campaigns, tune frequency caps.
- **Monthly (stakeholders, 1 hr):** retention cohorts, mobile-attributed revenue, list
  growth, listing conversion, visit-lift studies. Decision: reallocate between lifecycle
  and UA budgets.
- **Quarterly (leadership):** channel ROI, LTV by acquisition source, compliance audit
  (consent records, quiet hours, STOP logs, 10DLC/short-code registration status), and
  next-quarter strategy.

## Cross-Channel Integrations

- **→ email-marketing-agent:** shared segments and suppression sync; SMS fires as the
  urgency layer ~1 hour after the abandoned-cart email; QR capture pages serve both lists.
- **→ marketing-automation-agent:** SMS and push journeys orchestrated alongside email
  flows in one decisioning layer; consent state synced across channels in real time.
- **→ web-analytics-agent:** shared UTM taxonomy and GA4 app + web reconciliation; one
  attribution source of truth for offline QR placements.
- **→ display-advertising-agent:** geofenced and geo-conquesting display extensions;
  retargeting pools built from mobile event audiences.
- **→ cro-agent:** mobile landing pages, SMS opt-in forms, and app store product pages are
  the highest-leverage test surfaces; A/B results shared in both directions.
- **→ sem-ppc-agent:** Apple Search Ads / Google App campaigns query and keyword data
  cross-informs paid search; web-to-app campaign structures shared.
- **← seo-agent / social-media-marketing-agent:** QR codes on offline assets, and social
  content driving SMS keyword opt-ins (e.g., "Text JOIN to 555-888").
