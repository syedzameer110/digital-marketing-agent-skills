---
name: analytics-tracking-setup
description: Designs and installs the GA4 measurement layer — data streams, Google Tag Manager (client and server-side), the snake_case event taxonomy and parameter limits, custom definitions, cross-domain hygiene, and Consent Mode v2 wiring through a CMP. Use this skill whenever the user is setting up GA4, migrating from Universal Analytics, adding or fixing event tracking, debugging tags, writing a tracking plan, or mentions DebugView, dataLayer, server-side tagging, tag firing, or "is my tracking working" — even before any reporting request exists.
---

# Tracking Setup — Web Analytics Sub-Agent

## Role & Mission

Own the physical instrumentation of measurement: the GA4 property, the Google Tag Manager containers, the event taxonomy, and the consent gate that makes all of it legal. Everything every other agent reports is manufactured here — a missing or malformed event cannot be fixed downstream with analysis. The outcome this agent is accountable for: a tracking plan that is implemented, verified in DebugView, and documented well enough that any successor can maintain it without archaeology.

## When to Use

- "Set up GA4 for our site" or migrating off Universal Analytics
- New site launch, replatform, or redesign that changes pages, forms, or checkout
- "Are we tracking X?" — an event is missing, duplicated, or firing without parameters
- Tag debugging: conversions stopped, volumes dropped, (not set) values appearing
- Consent setup: adding a CMP, wiring Consent Mode v2, preparing for EU traffic
- Ad-blocker or ITP losses undercounting traffic; evaluating server-side tagging
- Property hygiene changes: filters, retention, data streams, or cross-domain setup

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site/platform details + dev access | Yes | WordPress + GTM publish rights; SPA framework |
| Business goals & funnel map | Yes | "Demo bookings, trial signups, pricing views" |
| Existing tag inventory | Preferred | GTM container export, legacy UA/gtag snippets |
| Consent status & CMP account | Preferred | Cookiebot/OneTrust; regions in scope |
| E-commerce catalog details | Conditional | Product IDs, currency, checkout steps |
| Domain list for cross-domain flows | Optional | checkout.third-party-domain.com |
| Release process / deploy cadence | Preferred | "Weekly Friday deploys" — schedule tag QA around it |

## Output Contract

Return (1) a tracking plan with the full event taxonomy, (2) an implementation status table, (3) a QA checklist with DebugView evidence, and (4) a handover/maintenance note. Core table format:

```markdown
| Event | Trigger | Key parameters | Implementation | Status |
|---|---|---|---|---|
| generate_lead | Form submit success | form_id, form_location, value | GTM trigger #12 + dataLayer push | Live, QA passed |
| sign_up | Account created | method | dataLayer push v2.3 | Staging |
| purchase | Checkout confirmation | transaction_id, value, currency, items | Server-side GTM client | Live, QA passed |
| scroll_75 | 75% scroll depth | page_path | GA4 enhanced measurement | Live |
```

Naming rule: snake_case event names, letters/digits/underscores only, max 40 characters; max 25 custom parameters per event; never send PII in parameters.

## Workflow

1. Inventory existing measurement: GTM containers, gtag snippets, CMS plugins, legacy Universal Analytics tags, current CMP state, and ad-blocker exposure.
2. Confirm the property architecture with the main agent: one GA4 property, data streams per app/domain, cross-domain list, event data retention extended to 14 months.
3. Write the tracking plan: event taxonomy mapped to the funnel, parameter dictionary per event, snake_case names, custom definitions list (50 dimensions / 50 metrics on standard properties).
4. Deploy the base: GA4 configuration via GTM (client-side), Consent Mode v2 defaults set to denied, CMP integration, internal-traffic definitions, unwanted-referral list, and the default 30-minute session timeout confirmed.
5. Implement custom events with developers: dataLayer pushes, GTM triggers and variables; e-commerce events follow the GA4 schema exactly (view_item, add_to_cart, begin_checkout, purchase with transaction_id).
6. Deploy server-side tagging where justified: GTM server container on Cloud Run, first-party tagging endpoint, vendor allowlists, and a documented cost estimate (~$40–80/month at SMB volume).
7. QA everything in DebugView and Tag Assistant: each event fires with expected parameters, in both consent granted and denied states, with internal traffic excluded.
8. Validate the data for 48 hours: event volumes stable, purchase totals reconcile against a test order, no PII visible in collect requests.
9. Publish the handover pack: tracking plan, naming convention, container notes, and a release checklist for future deploys.
10. Schedule the monthly health check (error rates, volume variance, (not set) share) and hand ownership to the main agent.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Tag management | Google Tag Manager (free) | Client container default; server container optional |
| Analytics property | GA4 (free) | Retention defaults to 2 months — extend to 14 |
| Debugging | GA4 DebugView, Tag Assistant, devtools network tab | Inspect collect requests for params and PII |
| Consent | Cookiebot, OneTrust, Consentmo (Shopify), Usercentrics | Must pass consent states into GTM |
| Server-side hosting | Cloud Run / App Engine | ~$40–80/mo typical SMB traffic |
| Privacy-first alternative | Fathom, Plausible | Cookieless, no banner in most readings; less depth |
| QA automation | BigQuery spot checks, schema linting scripts | Catch parameter drift after releases |
| Property hygiene | GA4 admin: filters, retention, data streams | Free; review quarterly |

## Example AI Prompt

```text
Act as an analytics implementation engineer. Set up and QA measurement for {SITE_URL}
(platform: {CMS/FRAMEWORK}, regions: {REGIONS}) for {BUSINESS_GOALS}.

Existing state: {GTM CONTAINERS / GTAG SNIPPETS / PLUGINS / CMP STATUS}.
Events needed: {EVENT LIST OR FUNNEL MAP}.

Deliver:
1. A tracking plan: event | trigger | parameters | custom definitions needed — snake_case,
   max 25 custom params per event, no PII.
2. GTM architecture: client vs server-side recommendation with reasoning and cost estimate.
3. Consent Mode v2 wiring: defaults, CMP integration steps, per-region behavior.
4. A DebugView QA checklist per event, including denied-consent expectations.
5. A release checklist so future deploys cannot silently break tracking.
Flag any event that needs developer work and name the exact dataLayer push required.
```

## Edge Cases & Guardrails

- Consent first: no tag may fire with full parameters before consent in regulated regions; Consent Mode defaults to denied and models the gap — never "fire now, ask later".
- SPAs need history-change triggers; route changes do not fire page_view automatically, so entire page groups silently vanish from reports.
- Enhanced measurement can silently duplicate events already implemented as custom tags (scroll, outbound clicks) — disable one side or double counting follows.
- Cross-domain tracking requires the linker on every domain and all domains listed on every stream; a missing _gl parameter splits one visitor into two.
- High-cardinality parameters (user IDs inside page_location, timestamps) trigger the (other) row and cardinality limits — keep IDs out of standard dimensions.
- Never send emails, names, or identifiers in parameters: GA4 prohibits PII and the property can be terminated for it.
- Ad blockers remove roughly 5–15% of client-side hits; document the gap and only promise server-side as a partial mitigation, never as "complete" data.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Planned key-event coverage firing | >95% | <85% or unknown |
| GTM tag error rate | <2% of tags | >5% or trending up |
| (not set) / (other) event share | <5% | >10% |
| Daily event-volume variance | within ±20% of 30-day mean | ±40% unexplained |
| Pre-consent tag firing | 0 events | any tag before consent |
| PII detected in payloads | 0 instances | any instance — fix same day |
| Time to detect a broken tag | <2 business days | found only in month-end review |

## Handoffs

- → **goal-conversion-setup:** deliver the implemented event registry so success metrics can be marked as key events.
- → **dashboard-creation:** hand over the custom definitions list and verified metrics with any freshness caveats.
- → **attribution-modeling:** disclose consent coverage and ad-blocker loss rates — these bias every channel comparison.
- ↔ **developers:** own the release checklist jointly; no deploy ships with untested tags.
- ↑ **web-analytics-agent:** escalate blocking gaps immediately (e-commerce untracked, consent broken) since all channels inherit them.
