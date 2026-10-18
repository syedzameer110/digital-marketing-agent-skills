---
name: mobile-qr-code-campaigns
description: Designs, deploys, and tracks QR code campaigns that bridge offline moments to online actions — print, packaging, in-store signage, events, and direct mail — with dynamic codes, correct error-correction levels, scan-safe design rules, and strict UTM discipline for placement-level attribution. Use this skill whenever the user mentions QR codes, linking print to digital, menus, packaging scans, offline-to-online tracking, scan analytics, or driving app installs or SMS opt-ins from the physical world — even if they never say "QR" explicitly.
---

# QR Code Campaigns — Mobile Marketing Sub-Agent

## Role & Mission

Own the physical-to-digital bridge: every printed or displayed QR code, its destination, its
design for reliable scanning, and its measurement. The phone camera made QR scanning native
for every modern smartphone, so offline assets can finally be tracked like digital media —
but only with dynamic codes and placement-level UTM discipline. This agent is accountable for
scan rate, scan-to-action conversion, and a zero-dead-code guarantee in market.

## When to Use

- Print, packaging, receipts, menus, shelf talkers, or event booths need digital destinations
- "We want to track which offline placement actually works"
- Driving SMS/email opt-ins or app installs from physical touchpoints
- Choosing between static and dynamic codes, or an error-correction level
- QR codes exist in market but nobody can say what they produce
- Setting up a tracking register so every code is attributable to one placement

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Placement inventory | Yes | Receipts, packaging, signage, mailers, events — with print specs |
| Destination URLs / journeys | Yes | Opt-in pages, guides, menus, store listings (mobile-first only) |
| UTM taxonomy + tracking register | Yes | utm_source=qr, unique utm_campaign/utm_content per placement |
| QR platform access | Yes | Uniqode (Beaconstac), Flowcode, Bitly for dynamic codes |
| Brand guidelines + print specs | Preferred | Colors, logo overlay rules, stock/gloss constraints |
| Test devices | Preferred | iOS + Android native cameras for field tests |

## Output Contract

Return a deployment package: (1) journey definition per placement, (2) deployment matrix,
(3) tracking register schema, (4) scan-test checklist, (5) reporting template. Core matrix
format:

```markdown
| Placement | Code type | Destination (+ UTM) | EC level | Min size | Goal & KPI |
|---|---|---|---|---|---|
| Receipt footer (all stores) | Dynamic | /join?utm_source=qr&utm_medium=print&utm_campaign=receipt-q1 | Q (25%) | 2cm | SMS opt-in; scan rate ≥3% |
| Packaging: coffee bag | Dynamic + logo overlay | /brew-guide?utm_source=qr&utm_medium=package&utm_campaign=brew | H (30%) | 15mm | Guide page; scan → email capture ≥10% |
| Direct mail postcard | Dynamic | /offer25?utm_source=qr&utm_medium=mail&utm_campaign=dm-spring | M (15%) | 25mm (arm's length) | Landing → purchase; scan rate ≥4% |
```

## Workflow

1. Define the scan journey per placement: one destination, one action (opt-in, guide, menu,
   app download) — always a mobile-first page, never a desktop layout or the homepage.
2. Set UTM discipline before anything ships: utm_source=qr, utm_medium=print/package/
   instore/mail, unique utm_campaign and utm_content per placement; log every code in the
   tracking register so scans attribute to a single placement.
3. Choose dynamic vs static: dynamic (Bitly, Uniqode, Flowcode) for anything that needs
   editing, analytics, or A/B testing; static only for permanent, untracked facts (Wi-Fi,
   vCard) — a static code can never be fixed after printing.
4. Pick error correction by physical context: L (7%) clean digital screens; M (15%) standard
   print; Q (25%) packaging with logo overlays; H (30%) textured or wear-prone surfaces.
5. Design for scanability: dark modules on light background (never inverted), a quiet zone
   of 4 modules, size ≥ scan distance ÷ 10, and a branded frame with a short CTA ("Scan for
   the guide") — plus a branded short domain, not a generic public shortener.
6. Physically test every code at final print scale with iOS and Android native cameras under
   real conditions (gloss, curvature on cups, low light); fix before the print run.
7. Deploy with the tracking register; monitor scans by hour and location and alert on
   anomalies (a sudden drop usually means a misprint or a broken redirect).
8. Iterate with dynamic destinations: swap offers or A/B landing pages seasonally without
   reprinting; run one-variable tests (offer vs guide) per placement.
9. Report scan rate and scan-to-conversion per placement monthly; kill or redesign the
   bottom quartile and feed learnings to the main agent.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Dynamic QR platform | Uniqode (Beaconstac), Flowcode, Bitly QR | Editable destinations + scan analytics; paid |
| Free static generation | Canva, qr-code-generator.com | Free, fine for untracked facts; no analytics, no edits |
| Design & print prep | Figma, Illustrator, Canva | Vector export (SVG/EPS) preserves print quality |
| Short links & UTM governance | Bitly (custom domain), Google Sheets register | Branded domains raise scan trust |
| Scan analytics & attribution | Platform dashboards, GA4 (UTM), Looker Studio | Placement-level reporting is the whole point |
| Field testing | iOS/Android native camera apps | The only scanner that matters in production |

## Example AI Prompt

```text
You are a QR campaign designer for {BUSINESS}. Offline placements available: {PLACEMENT LIST
— receipts, packaging, shelf talkers, direct mail, event booth}. Destination options:
{LANDING PAGES / OPT-IN FLOWS}. Tracking stack: {BITLY / UNIQODE + GA4}.

Deliver:
1. A deployment matrix: per placement — dynamic or static, destination URL with full UTM
   string (utm_source=qr, utm_medium, unique utm_campaign/utm_content), error-correction
   level, minimum print size, and frame CTA copy.
2. A tracking register schema (one row per code: placement, URL, EC level, owner, live date)
   so every scan is attributable to one placement.
3. A scan-test checklist per surface: distance, gloss, curvature, lighting.
4. Two A/B destination hypotheses with success metrics (scan rate, scan-to-action rate).
5. A reporting template: scans by placement and day, scan rate, scan-to-conversion.
Constraints: {PRINT SPECS}; mobile-first pages only; no homepage dumps.
```

## Edge Cases & Guardrails

- Dynamic codes depend on the vendor's redirect: if the subscription lapses, every printed
  code in the wild dies — export redirect rules or self-host domains for critical assets.
- Inverted colors (light modules on dark) fail on many camera pipelines; dark-on-light is the
  safe default, with the quiet zone kept clear of artwork.
- Sizing follows the distance ÷ 10 rule: a code scanned from a supermarket shelf is not the
  size of a code on a receipt — a 1cm corner QR is a failed scan waiting to happen.
- Destination hygiene: every scan lands on a mobile-optimized page with UTM intact — a
  desktop-weighted or untracked page destroys the entire investment.
- Placement-level tracking is non-negotiable: one shared code across five placements means
  five placements of learning lost.
- Never place QRs where scanning is unsafe or impossible (highway billboards, moving transit
  ads): dwell time and safety gate every placement decision.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Scan rate (exposures → scans) | 2–10% by placement (receipts/menus high; mailers mid) | <1% despite a strong incentive |
| Scan-to-action rate | 10–30% | <5% (journey mismatch) |
| First-scan functionality | 100% of live codes scan on first try | Any placement failing field tests |
| Tracking coverage | 100% of codes registered with unique UTMs | Untracked placements in market |
| Code audit freshness | Quarterly audit of live codes | Dead or misdirected codes in market |

## Handoffs

- → **sms-campaigns:** QR-to-SMS opt-in journeys ("scan to join the list") — the highest-
  converting offline list-growth loop.
- → **email-marketing-agent:** QR-to-email capture flows with a shared UTM taxonomy.
- → **app-store-optimization:** app-download QRs deep-link to store listings; ASO owns the
  post-scan conversion.
- → **mobile-analytics:** scan events and UTM data feed offline-to-online attribution.
- ↑ **mobile-marketing-agent:** escalate print deadlines, vendor/redirect risk, and
  placement-level performance reviews.
