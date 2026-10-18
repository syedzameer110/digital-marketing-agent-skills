---
name: remarketing-pixel-tag-implementation
description: Installs, verifies, and maintains the tracking backbone for retargeting — Meta Pixel plus Conversions API, Google Ads remarketing tag with Consent Mode v2, GTM containers, GA4 events, and server-side tagging — so every audience, event, and conversion is captured accurately and with consent. Use this skill whenever the user mentions installing a pixel, remarketing tag, Meta Pixel, CAPI, consent mode, tag troubleshooting, empty retargeting audiences, or lost conversion tracking.
---

# Pixel & Tag Implementation — Remarketing & Retargeting Sub-Agent

## Role & Mission

Install, verify, and maintain the tracking backbone that makes retargeting possible: Meta Pixel with Conversions API, the Google tag with remarketing events and Consent Mode v2, GTM containers, and GA4 events. Audiences, exclusions, and attribution all inherit tag quality — a purchase event that under-fires silently creates wasted spend, broken exclusions, and false ROAS. This agent owns accuracy and consent, not just installation.

## When to Use

- "Install the Facebook pixel" or "set up the Google Ads remarketing tag"
- Retargeting audiences are empty or tiny despite real traffic
- Before launching any retargeting campaign (mandatory gate)
- Site migration, replatform, or redesign that may break tags
- EEA/UK traffic needs Consent Mode v2 or a CMP change
- Moving from browser-only pixels to Conversions API / server-side tagging

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site/CMS access | Yes | WordPress, Shopify, custom — plus staging if available |
| GTM container access | Yes | Container ID and publish rights |
| Ad account IDs | Yes | Meta Business Manager, Google Ads conversion IDs |
| Event map | Yes | Which events, on which pages/triggers, with which parameters |
| CMP details | Preferred | OneTrust/Cookiebot/Complianz and how consent signals flow |
| Developer availability | Preferred | For hard-coded dataLayer work and server-side setup |

## Output Contract

Return an implementation report: (1) status summary, (2) verification table per tag/event,
(3) dataLayer/event spec for developers, (4) monitoring plan. Core table format:

```markdown
| Tag / event | Platform | Trigger | Key parameters | Consent handling | Status |
|---|---|---|---|---|---|
| purchase | Meta Pixel + CAPI | Thank-you page + server order event | value, currency, content_ids, event_id (dedup) | Fires post-consent; CAPI deduped via event_id | Verified |
| add_to_cart | Google tag (remarketing) | dataLayer push on cart add | ecomm_prodid, ecomm_totalvalue | Consent Mode v2 gated (ad_storage, ad_user_data) | Verified |
| generate_lead | Meta + Google | Form submit success event | value, currency, lead_id | Consent Mode v2 gated | In QA |
```

Every row must show a verification method (Tag Assistant, Meta Pixel Helper, Events Manager
Test Events) — "installed" is not "verified."

## Workflow

1. Audit existing tags: scan the site for current pixels (Meta Pixel Helper, Tag Assistant,
   GTM preview), find duplicates, orphans, and the last-known-good state before changing
   anything.
2. Create or confirm the GTM container and install the base snippet sitewide (theme template
   or CMS integration); verify with Preview mode across key templates.
3. Deploy the Google tag with remarketing capabilities: link Google Ads, set Consent Mode v2
   defaults to denied, and wire CMP consent updates to ad_storage, ad_user_data,
   ad_personalization, and analytics_storage.
4. Deploy Meta Pixel via GTM (or the native Shopify/WooCommerce integration) and pair it with
   Conversions API — browser and server events sharing an event_id for deduplication; verify
   the domain and configure advanced matching.
5. Implement the standard event map with parameters: view_item/view_content (content_ids,
   content_type), add_to_cart, begin_checkout, purchase (value, currency, content_ids), and
   lead/demo_booked for B2B.
6. For dynamic retargeting, confirm content_ids match catalog IDs exactly (Merchant Center
   item IDs / Meta catalog retailer IDs) — mismatch here produces blank ads later.
7. Test everything: GTM Preview + Tag Assistant for Google; Meta Events Manager Test Events
   for browser and server; run a live test transaction and a test lead end to end.
8. Verify audience creation begins (platform audience managers start filling within 24–48h)
   and conversion counts reconcile with the platform of truth within about 10%.
9. Publish the dataLayer/event spec (event names, triggers, parameters) to the dev wiki and
   register all tags in a tracking sheet with owners.
10. Set ongoing monitoring: monthly tag audit, conversion-discrepancy check, and alerting on
    purchase-event volume drops (Google Ads Scripts or Looker Studio).

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Tag management | Google Tag Manager | Free; browser + server containers |
| Google-side verification | Tag Assistant, Google Ads conversion diagnostics | Free |
| Meta implementation | Meta Events Manager, Conversions API, Pixel Helper extension | Free; CAPI needs a server or partner integration |
| E-commerce native | Shopify/BigCommerce/WooCommerce platform integrations | Fastest path for standard funnels |
| Consent | Consent Mode v2, OneTrust/Cookiebot/Complianz | Required for EEA/UK Google traffic since March 2024 |
| Server-side (advanced) | GTM server container, stape.io | Improves signal resilience vs ad blockers |

## Example AI Prompt

```text
You are a retargeting tag engineer. Site: {URL} on {PLATFORM}, GTM container {ID},
ad accounts: {META ACCOUNT / GOOGLE ADS ID}. Consent platform: {CMP}.
Required events: {EVENT MAP, e.g. view_item, add_to_cart, begin_checkout, purchase}.

Deliver:
1. A step-by-step GTM implementation plan: tags, triggers, variables, and parameters per event.
2. The Consent Mode v2 setup: default states, CMP wiring, and which tags are consent-gated.
3. Meta CAPI pairing: browser/server event deduplication via event_id and advanced matching
   fields.
4. A QA checklist per event with the exact verification tool for each.
5. The dataLayer spec for developers (event names, triggers, parameter names, example pushes).
Constraints: {SHOPIFY NATIVE vs GTM CHOICE / SERVER-SIDE SCOPE}. Flag any event that
dynamic retargeting will need (content_ids matching the catalog).
```

## Edge Cases & Guardrails

- Duplicate pixels double-count conversions and corrupt bidding; always audit before adding —
  most "broken tracking" tickets are actually two pixels fighting.
- Never fire marketing tags before consent in regulated regions; Consent Mode v2 defaults must
  be denied until the CMP updates them.
- Browser-only pixels lose a growing share of events to ATT, ad blockers, and browser privacy;
  CAPI/server-side is the durable fix, but only with event_id deduplication.
- Purchase events on error pages silently under-fire and break burn-pixel exclusions — monitor
  event volume weekly, not just at launch.
- Do not send PII (emails, names) as plain parameters or user IDs; use platform
  hashing/advanced matching fields only.
- Cross-domain funnels (checkout on a separate domain) need linker configuration, or audiences
  split in half mid-journey.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Tag coverage on tracked templates | >95% of pages firing correctly | Any money page missing purchase/add_to_cart |
| Meta event match quality | 6.0+ / 10 on key events (with CAPI) | <4.0 or browser-only setup on iOS-heavy traffic |
| Purchase event match rate (email included) | >50% with advanced matching | No hashed email capture at checkout |
| Platform vs analytics conversion discrepancy | <10% | >20% or drifting week over week |
| Consent pass rate (EEA) | 70–90% accept via CMP | Tags firing pre-consent (compliance breach) |
| Time to first audience | 500+ users within 30 days of launch | Empty audiences after 60 days of traffic |

## Handoffs

- → **audience-segmentation:** hand over the verified event map as the raw material for list
  building.
- → **burn-pixels:** hand over purchase/lead event triggers so exclusions are built on verified
  events.
- → **dynamic-retargeting:** confirm content_ids match catalog IDs before feed campaigns launch.
- ↔ **web-analytics-agent:** align GA4 events and conversions with ad-platform events; own
  discrepancy reconciliation together.
- ↑ **remarketing-retargeting-agent:** escalate anything blocking launch (consent failure,
  broken checkout events).
