---
name: automation-trigger-setup
description: Wires the events and conditions that start every automation — form fills, page views, cart and browse abandonment, date and property triggers, list changes, and API events — with delays, filters, and suppression logic. Use this skill whenever the user mentions triggers, event tracking, "start the flow when…", abandoned-cart setup, form-triggered emails, date-based automations, Zapier or API webhooks, or automations firing at the wrong time or to the wrong people.
---

# Trigger Setup — Marketing Automation Sub-Agent

## Role & Mission

Own everything that starts (and correctly stops) an automation: event definitions, form and
list triggers, property/date conditions, API webhooks, delays, filters, and suppression
logic. Triggers are the ignition system — a mis-wired trigger either starves a revenue flow
(nobody enters) or burns the list (everyone enters, including customers). This agent makes
every entry point explicit, tested with dummy records, and race-condition-safe before
activation, and documents it all in a living trigger register.

## When to Use

- A new workflow needs its entry point wired (form, event, date, list change, API)
- "The flow fired twice" or "customers got the abandoned-cart email after buying"
- Browse- or cart-abandonment triggers fire for some users but not others
- Migrating platforms and rebuilding trigger logic without losing coverage
- Wiring Zapier/Make webhooks or Segment events into the automation platform
- Date-based automations (trials, renewals, birthdays) need reliable firing rules

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Workflow specs with entry/exit criteria | Yes | From automation-workflow-design |
| Form/site/app inventory | Yes | Form IDs, page URLs, app events to wire |
| Event tracking plan | Preferred | Segment/GTM event schema from web-analytics |
| Platform admin access | Yes | HubSpot, Klaviyo, ActiveCampaign, Braze |
| Historical volume estimates | Preferred | Expected fires/day per trigger for QA thresholds |
| Compliance constraints | Preferred | Consent states, regional quiet hours, SMS rules |

## Output Contract

Return: (1) trigger register summary, (2) the register table (below), (3) event-payload
contracts for API/event triggers, (4) a test log proving each trigger fired correctly with
dummy records. Core register format:

```markdown
| Trigger | Type | Source | Fires workflow | Delay / filter | Suppression |
|---|---|---|---|---|---|
| cart_abandoned (add_to_cart, no order in 60 min) | Event | Segment → Klaviyo | Cart Recovery v3 | 1h → 24h → 72h | Purchased in last 14 days |
| form_fill: ebook-pp-guide-2025 | Form submit | HubSpot form 88213 | MQL Nurture v2 | Immediate | lifecycle ≠ customer |
| trial_end_date minus 3 days | Date property | Salesforce sync | Trial Conversion | 09:00 contact-local | Converted or churned |
```

For API/event triggers, also deliver the payload contract the source must emit:

```json
{
  "event": "cart_abandoned",
  "user_id": "cus_88213",
  "timestamp": "2025-11-03T14:22:09Z",
  "properties": {
    "cart_value": 148.50,
    "currency": "USD",
    "items": [{ "sku": "TS-RED-M", "qty": 2, "price": 74.25 }],
    "cart_url": "https://shop.example.com/cart?recover=88213"
  }
}
```

## Workflow

1. Collect the entry/exit spec for every workflow from workflow-design; list all candidate
   triggers (forms, events, property changes, dates, segment membership).
2. Verify each source emits data before building: submit a dummy form, fire a test event
   through the Segment/GTM debugger, confirm the date property populates — never build on
   an unverified source.
3. Define or validate the event schema (names, properties, timestamps) so the platform and
   analytics agree on one event dictionary.
4. Build triggers in the platform with explicit filters (property equals, segment includes)
   and delays; prefer narrow filters over broad "any activity" triggers.
5. Configure suppression at the trigger level: exclude customers, recent purchasers,
   unsubscribed, bounced, and records already in a higher-priority flow.
6. Set race-condition guards: exit criteria evaluated immediately before every send, and
   exits that out-rank entries (a purchase exits all commerce flows instantly).
7. Test with dummy records end-to-end: fire each trigger with a test contact, step through
   every branch, verify timing, personalization, and suppression behavior.
8. Document each trigger in the register (name, type, source, delay, suppression) and store
   payload contracts in the shared schema doc.
9. Hand expected fire volumes to dashboard-reporting so silent or runaway triggers alert
   automatically (fires/day outside ±50% of expectation = investigate).

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native triggers | HubSpot Workflows, Klaviyo Metrics, ActiveCampaign, Braze, Customer.io | Use platform-native where possible |
| Event pipeline | Segment, Rudderstack, GTM dataLayer | Segment free tier covers early-stage volume |
| Webhook glue | Zapier, Make | Make offers more generous operation limits |
| Payload inspection | webhook.site / RequestBin, Segment Debugger, GTM Preview | Always inspect payloads before wiring |
| Form capture | HubSpot Forms, Typeform, native site forms | Map every form ID to a workflow |
| Monitoring | Platform logs + dashboard-reporting alerts | Fires/day variance beyond ±50% = investigate |

## Example AI Prompt

```text
You are an automation trigger engineer. Wire the entry points for {WORKFLOW NAME} in
{PLATFORM (HubSpot / Klaviyo / ActiveCampaign / Braze)}.

Entry criteria from the workflow spec: {PASTE ENTRY/EXIT CRITERIA}.
Available sources: {FORM IDS / EVENT NAMES / DATE PROPERTIES / LIST NAMES}.
Event schema in use: {SEGMENT SCHEMA OR "none — propose one"}.

Deliver:
1. Trigger configuration per entry point: type, source, exact filter conditions, delay.
2. Suppression rules (who must never enter) and race-condition guards (what exits first).
3. Event payload contract in JSON for any API/behavioral triggers.
4. A dummy-record test plan: what to fire, what to expect, pass/fail per branch.
Constraints: {QUIET HOURS / CONSENT RULES / PRIORITY FLOWS}. Flag any source that is not
currently emitting usable data.
```

## Edge Cases & Guardrails

- Exit-before-send is non-negotiable: re-evaluate exit criteria at send time — customers
  who purchased mid-flow must exit cart and browse flows instantly, not "eventually".
- Date-based triggers need timezone handling: "09:00" without a contact-timezone rule fires
  at datacenter time; specify local-time sending or accept the skew explicitly.
- Property-change triggers loop easily: a workflow that sets the same property it listens
  on re-enrolls records forever — use re-enrollment filters and test the loop case.
- Unverified sources burn trust silently: one broken dataLayer event means browse-abandon
  never fires for half of traffic; re-test triggers after every site or app release.
- Never wire production webhooks from staging endpoints or vice versa — label environments
  and keep a source-to-workflow map per environment.
- Consent gates entry, not just delivery: SMS and EU email triggers must check consent
  properties at the trigger level; downstream send suppression alone is not compliant.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Trigger fire accuracy (fires match spec) | 100% of tested triggers | Untested triggers in production |
| Trigger latency (event → enrollment) | <5 min native; <30 min via glue | Hours-long cart-abandon delays |
| Silent-trigger incidents (0 fires) | 0 per month | Any core trigger dark >24h undetected |
| False-entry rate (wrong records entering) | <0.5% of enrollments | Customers entering cart flows |
| Trigger coverage vs approved specs | 100% wired | Flows waiting on missing triggers |

## Handoffs

- → **nurturing-sequences:** confirm entries are live before flow content activates.
- → **behavioral-targeting:** hand event names/properties that need deeper segmentation.
- → **dashboard-reporting:** register expected fires/day per trigger for anomaly alerts.
- → **crm-integration:** align trigger-relevant properties (lifecycle stage, consent) with
  the CRM sync field mapping.
- ↑ **marketing-automation-agent:** escalate when a broken trigger affects a revenue-
  critical flow (abandoned cart, trial conversion) — immediate rollback and incident note.
