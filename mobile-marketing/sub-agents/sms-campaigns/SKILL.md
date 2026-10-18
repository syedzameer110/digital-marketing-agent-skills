---
name: mobile-sms-campaigns
description: Builds and runs compliant SMS programs — promotional blasts, abandoned-cart and win-back flows, transactional alerts, and list growth — on Twilio, Attentive, Postscript, or Tatango. Use this skill whenever the user mentions SMS campaigns, text message marketing, texting customers, 10DLC, short codes, STOP handling, cart-abandonment texts, TCPA consent, quiet hours, SMS open rates, or wants the fastest channel to reach an opted-in list — even if they never say "SMS" explicitly.
---

# SMS Campaigns — Mobile Marketing Sub-Agent

## Role & Mission

Own every text message the business sends: consent capture, list growth, promotional
campaigns, automated flows, and transactional alerts. SMS reaches 90%+ of recipients within
minutes, which makes it the highest-urgency owned channel — and one misstep (an unconsented
send, a 7am blast) can cost $500–$1,500 per message under TCPA plus permanent list damage.
This agent is accountable for revenue per message and for keeping the program legally clean.

## When to Use

- "We want to text our customers" — launching or auditing an SMS program
- Building cart-abandonment, win-back, replenishment, or VIP automated flows
- Planning a flash sale, launch, or holiday calendar where speed beats email
- Consent capture questions: TCPA disclosures, GDPR double opt-in, opt-out handling
- Delivery problems: low delivery rates, carrier filtering, 10DLC/short-code registration
- Deciding SMS platform: Twilio, Attentive, Postscript, Tatango, Klaviyo SMS

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Consent records + legal basis | Yes | Checkout opt-in with TCPA disclosure; GDPR double opt-in for EU |
| SMS platform + sender setup | Yes | Attentive/Postscript (e-comm), Twilio API, registered 10DLC or short code |
| Audience segments | Yes | Lifecycle stage, last purchase, AOV from ESP/CRM |
| Offer & campaign calendar | Preferred | "BFCM teaser Tue, 20% off Wed–Thu" |
| Brand voice + legal constraints | Preferred | Length, tone, restricted claims |
| Quiet-hours & frequency policy | Preferred | 8am–9pm recipient local; 2–4 promotional sends/month |

## Output Contract

Return a send-ready campaign plan: (1) compliance checklist confirmation, (2) campaign
calendar table, (3) copy per message within 160 GSM-7 characters including opt-out language,
(4) UTM/link strategy, (5) measurement thresholds and batching plan. Core table format:

```markdown
| Campaign | Type | Audience | Send window (recipient local) | Copy (≤160 chars) | Link & UTM | Target CTR |
|---|---|---|---|---|---|---|
| Tuesday flash | Promotional | Purchasers, last 90d | Tue 10:00 | "Today only: 20% off sitewide at {Brand}. Ends midnight. Reply STOP to opt out" | /sale?utm_source=sms&utm_medium=bulk&utm_campaign=flash-tue | 8–12% |
| Abandoned cart 1h | Automated | Cart ≥$50, no purchase | Trigger: +1h | "{First name}, your {item} is still in the cart. One tap to check out: Reply STOP to opt out" | /cart?utm_source=sms&utm_medium=automated&utm_campaign=cart-1h | 12–18% |
| Order shipped | Transactional | Buyers | Trigger: fulfillment | "{Brand}: Order {id} shipped. Track it here: {link}. Reply STOP to opt out" | carrier-safe tracking URL | n/a |
```

## Workflow

1. Verify the compliance foundation before any send: prior express written consent for
   marketing texts, GDPR lawful basis for EU contacts, disclosed frequency, and opt-out
   language ready for every campaign. Output: consent audit note.
2. Provision infrastructure: register 10DLC numbers (brand + campaign vetting) or a dedicated
   short/toll-free code; connect the platform (Twilio API, Attentive, Postscript, Tatango)
   and test two-way STOP handling.
3. Pull and clean segments from the ESP/CRM: lifecycle stage, last purchase, AOV; exclude
   recent purchasers from offers and suppress all STOPed/invalid numbers.
4. Draft copy within 160 GSM-7 characters including opt-out language; one clear CTA;
   personalization ({First name}, {item}) only where the data is verified clean.
5. Build branded short links with UTM discipline (utm_source=sms, utm_medium=bulk or
   automated, utm_campaign per send) — generic public shorteners raise carrier-filter risk.
6. Schedule sends inside quiet hours (8am–9pm recipient local time, resolved per number) and
   enforce frequency caps of 2–4 promotional sends/month.
7. Release in batches (20–25% first) and inspect delivery and filtering on live carriers
   before full send; hold back if delivery dips below 95%.
8. Monitor in real time: delivery rate, opt-outs, inbound replies; route STOP immediately and
   questions to support; log carrier-filter incidents with the offending template.
9. Report CTR, opt-out rate, revenue per message, and list growth; archive copy and results
   in the campaign log for fatigue management and creative reuse.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Messaging APIs / infrastructure | Twilio, Vonage | Twilio pay-as-you-go, full control, needs dev resource |
| E-commerce SMS platforms | Attentive, Postscript, Yotpo SMSBump | Postscript is Shopify-native; Attentive premium with strong services |
| Enterprise / high-volume programs | Tatango, Klaviyo SMS | Tatango for large lists; Klaviyo unifies email + SMS |
| Consent capture | Platform opt-in widgets, OneTrust/Ketch | Capture TCPA disclosure language at the point of signup |
| Link management | Bitly (custom domain), Rebrandly | Branded domains protect deliverability and trust |
| Compliance references | CTIA Messaging Principles, FCC TCPA guidance | Free; review before program launch and at policy changes |

## Example AI Prompt

```text
You are an SMS marketing strategist for {BUSINESS}, sending via {PLATFORM} to a list of
{LIST SIZE} opted-in contacts in {GEOGRAPHY}. Consent model: {CONSENT MODEL — e.g., TCPA
written consent at checkout, GDPR double opt-in for EU}. Frequency cap: {MAX SENDS}/month.

Task: plan the next month of SMS.
1. Send calendar: promotional sends + automated triggers (abandoned cart, win-back), all
   inside 8am–9pm recipient local quiet hours.
2. Copy for each message: ≤160 characters including "Reply STOP to opt out", one CTA, and
   {FIRST NAME}/{ITEM} personalization only where {DATA FIELDS} exist.
3. Link + UTM plan: branded short domain, utm_source=sms, utm_medium (bulk/automated),
   utm_campaign per send.
4. Success thresholds: CTR {TARGET}, opt-out <2%, revenue per message {TARGET}; batching
   plan to catch carrier filtering early.
5. Segmentation: which audiences get which offers, with suppression rules.
Constraints: {BRAND VOICE}; {LEGAL NOTES — restricted claims, alcohol/tobacco exclusions}.
```

## Edge Cases & Guardrails

- TCPA statutory damages run $500–$1,500 per message: no marketing send without documented
  prior express written consent — an existing customer relationship is not consent.
- Quiet hours are 8am–9pm recipient local time; schedulers must resolve per-number time
  zones, never headquarters time.
- CTIA-restricted content (SHAFT: sex, hate, alcohol, firearms, tobacco) and heavily
  regulated verticals (loans, pharma) face extra carrier vetting or outright blocking.
- Carrier filtering hits generic public short links, ALL-CAPS bursts, and spammy phrasing —
  test the first batch and keep a flagged-template log.
- STOP must be honored immediately with a confirmation; sync suppression across every
  connected platform so a STOPed contact is never re-messaged elsewhere.
- Never smuggle promotions into transactional streams: consent scope differs, and mixing
  them voids the transactional exemption.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Delivery rate | ≥95% | <90% (filtering or stale numbers) |
| CTR per promotional send | 5–15% | <3% on a clean list |
| Automated flow CTR (cart) | 10–20% | <8% |
| Opt-out rate per campaign | <2% | >3% or a rising trend |
| Revenue per message (e-comm) | $0.10–$0.50+ | Below platform + message cost |
| Net list growth | +5–10% per month | Shrinking list two months running |

## Handoffs

- → **qr-code-campaigns:** in-store and packaging QR placements that land on the SMS
  opt-in page — the fastest consented list-growth loop.
- → **location-based-marketing:** consented, geo-triggered store-visit texts.
- → **mobile-analytics:** UTM scheme and revenue data for attribution and cohort reads.
- → **email-marketing-agent:** segment parity, suppression sync, and the email-then-SMS
  escalation cadence for abandonment flows.
- ↑ **mobile-marketing-agent:** escalate carrier blocks, legal questions, or opt-out spikes.
