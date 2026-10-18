---
name: remarketing-burn-pixels
description: Implements burn pixels and conversion exclusions that automatically remove converted users from retargeting audiences — purchase events, thank-you-page triggers, demo-booked leads, and subscriber signups synced across Google Ads, Meta, and customer match lists. Use this skill whenever the user mentions burn pixel, exclusion audiences, ads still showing after purchase, wasted spend on existing customers, post-conversion suppression, or stopping retargeting to converted leads — even if they never say burn pixel.
---

# Burn Pixels — Remarketing & Retargeting Sub-Agent

## Role & Mission

Implement and audit burn pixels — the conversion events and exclusion rules that automatically remove converted users from retargeting audiences. Every impression served to someone who already bought or booked is the most expensive waste in the channel: it costs premium CPMs, eats frequency headroom needed for real prospects, and tells existing customers the brand does not know them. This agent owns the "stop advertising to people who already said yes" layer.

## When to Use

- "Ads keep showing to people who already purchased"
- Setting up post-conversion suppression for any new campaign (mandatory gate)
- Lead-gen funnels: suppressing demo-booked or qualified leads
- Refunds, returns, or subscription churn need re-entry rules
- Multi-product stores: item-level vs account-level burn decisions
- Quarterly exclusion audit across platforms

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Conversion event map | Yes | Verified purchase/lead/demo_booked events (from pixel-tag-implementation) |
| Thank-you/success page access | Yes | URLs or triggers for page-based burn logic |
| CRM status definitions | Preferred | Lead → MQL → SQL → customer stages for B2B burn points |
| Platform audience access | Yes | Google Ads exclusions, Meta ad set exclusions, customer match |
| Subscription/renewal rules | Optional | Churn re-entry windows for recurring products |
| Refund/return policy | Optional | Whether refunds re-enter acquisition audiences |

## Output Contract

Return a burn-pixel register: (1) summary of what burns where, (2) the register table,
(3) re-entry rules, (4) test evidence. Core table format:

```markdown
| Conversion point | Burn trigger | Platforms covered | Exclusion mechanism | Re-entry rule | Verified |
|---|---|---|---|---|---|
| E-comm purchase | purchase event (value > 0) | Meta, Google Ads | Purchasers 180d audience excluded at ad set/campaign | Replenishable SKUs re-enter cross-sell pool at 90d | Yes (test order 1042) |
| Demo booked | demo_booked event via GTM | Google Ads, LinkedIn | Demo-booked audience excluded; CRM sync removes from match list | Never (sales-owned) | Yes |
| Free-trial signup | trial_start event | Meta | Trialists 60d excluded | Expired trials re-enter at 60d | In QA |
```

Rules: every live retargeting campaign appears in the register with its exclusion mechanism —
a campaign not in the register is a campaign shipping waste.

## Workflow

1. Confirm the conversion events exist and fire reliably (work with pixel-tag-implementation);
   a burn layer on an under-firing purchase event excludes nobody and reads as healthy.
2. Map burn points per business model: e-comm = purchase; lead-gen = demo_booked or SQL (raw
   form fills usually stay in nurture audiences — decide deliberately); subscription = trial
   start and paid conversion.
3. Build converted-user audiences on each platform: Meta custom audience from the purchase/
   lead event, Google Ads audience segments from conversion rules, CRM/customer lists synced
   via customer match weekly.
4. Attach exclusions at campaign and ad-set level for every retargeting campaign; for dynamic
   campaigns, enable purchased-item suppression in DPA/catalog settings as a second layer.
5. Configure GA4 audience removal where used (audiences that drop users on conversion events
   feeding Demand Gen), keeping one mechanism authoritative per platform.
6. Define re-entry rules deliberately: replenishable SKUs cross-sell after a window; churned
   subscribers re-enter; refunds restore acquisition eligibility — document each rule with a
   duration.
7. Test end to end: place a test order / submit a test lead, then confirm the user exits the
   retargeting audience within the platform's propagation window (typically <24–48h) and stops
   seeing ads.
8. Audit view-through noise: confirm "converted" users in platform columns are real
   conversions, not view-through claims on users the burn layer already removed.
9. Publish the register to the shared sheet, wire CRM-to-platform sync (weekly uploads or
   API), and schedule a quarterly audit across all platforms and campaigns.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Burn triggers | GTM (thank-you-page triggers), native platform events | Free |
| Meta suppression | Meta custom audiences from events, ad set exclusions, DPA purchased-item rules | Free with ad account |
| Google suppression | Google Ads audience exclusions, Customer Match sync | Customer match requires policy compliance |
| CRM sync | HubSpot/Salesforce to customer match via weekly upload, Zapier, or API | Zapier free tier limited; API for scale |
| Verification | Test orders/leads, Meta Events Manager Test Events, Tag Assistant | Manual proof beats dashboards |
| Audit tracking | Google Sheets register + Looker Studio converted-user exposure view | Reviewed quarterly |

## Example AI Prompt

```text
You are a burn-pixel and exclusion specialist for {BUSINESS} ({ECOMM / LEADGEN /
SUBSCRIPTION}). Conversion events verified: {EVENT LIST + STATUS}. Platforms with live
retargeting: {META / GOOGLE ADS / LINKEDIN}. CRM stages: {STAGES}. Business rules:
{REPLENISHMENT WINDOW / REFUND POLICY / CHURN RE-ENTRY}.

Deliver:
1. A burn map: conversion point, burn trigger, platforms, exclusion mechanism, re-entry rule.
2. Platform-specific setup steps (Meta ad set exclusions + DPA suppression; Google audience
   exclusions + customer match sync cadence).
3. The B2B decision: which lead stage burns (raw lead vs MQL vs demo_booked) with reasoning
   for our cycle length of {DAYS}.
4. A test protocol: how to prove exclusion propagation in under 48 hours.
5. A quarterly audit checklist for exclusion drift.
Constraints: {PRIVACY / CONSENT NOTES}. Flag any campaign currently missing exclusions.
```

## Edge Cases & Guardrails

- The classic failure: burn logic built on an event that under-fires — exclusions look
  configured but converted users keep seeing ads; verify with test conversions, not setup
  screenshots.
- Do not burn on raw form fills in B2B by default — unqualified leads leave the nurture pool
  and starve marketing-automation; burn at demo_booked/SQL and record the decision.
- View-through conversions can re-credit users the burn layer already removed — read
  converted-user exposure from audience audits, not platform ROAS columns.
- Multi-product stores must decide item-level vs account-level burn: burn the account for
  acquisition campaigns, keep item-level pools for replenishment cross-sell.
- Refunds and returns: define re-entry explicitly or risk permanently excluding willing buyers
  (or re-targeting the annoyed).
- Respect consent and platform rules: exclusions built from CRM data require a lawful basis,
  and customer match policies prohibit sensitive-category use either way.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Converted users served retargeting ads | <2% within 7 days of conversion | Any pattern of post-purchase chase ads |
| Exclusion propagation time | <24–48h across platforms | Multi-day gaps after test conversions |
| Register coverage | 100% of live retargeting campaigns listed | Campaigns missing from the register |
| Wasted spend on converted users | Near $0 on spot audits | >5% of retargeting spend hitting customers |
| Re-entry rule documentation | 100% of burn points documented | Undocumented "it just works" logic |
| Audit cadence | Quarterly, with test evidence | No audit since launch |

## Handoffs

- ← **pixel-tag-implementation:** receive verified conversion events as the foundation of all
  burn logic.
- → **audience-segmentation:** converted-user lists become the seeds for cross-sell and
  replenishment tiers.
- → **marketing-automation-agent:** burn events enroll converted users into post-purchase/
  onboarding flows — coordinate suppression so email and ads do not double-message.
- → **dynamic-retargeting:** confirm purchased-item suppression is active on every catalog
  campaign.
- ↑ **remarketing-retargeting-agent:** report exclusion health monthly; escalate any campaign
  found shipping waste.
