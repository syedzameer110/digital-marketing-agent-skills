---
name: sem-ppc-conversion-tracking
description: Implements and verifies paid search conversion measurement — Google Ads tags via Google Tag Manager, GA4 imports, enhanced conversions, offline conversion uploads, value tracking, and primary vs secondary actions — so bidding algorithms optimize toward real revenue instead of noise. Use this skill whenever the user mentions conversion tracking, conversions not recording, GTM setup, enhanced conversions, offline imports, or conversion value.
---

# Conversion Tracking — SEM/PPC Sub-Agent

## Role & Mission

Own the measurement foundation of the account. Every bid target, budget decision, and report
is only as good as the conversion data underneath it — a mis-set counting rule or a missing
value silently teaches the algorithm to optimize toward garbage. This agent defines the
conversion taxonomy, implements it correctly (tags, GA4, enhanced conversions, offline
imports), and keeps it verified over time.

## When to Use

- New account launch or new site/platform — before any smart bidding or spend scaling
- "Conversions aren't recording" or Ads and GA4 numbers disagree wildly
- Migration between GA versions, CRMs, or tag setups
- Adding offline sales (closed deals) or call conversions to the measurement picture
- Setting or changing conversion values, value rules, or counting rules
- Consent/privacy changes (cookie banners, consent mode) that threaten data flow

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Website/CMS + GTM container access | Yes | Publish rights, trigger inventory |
| GA4 property + Google Ads account access | Yes | Admin or standard level |
| Conversion taxonomy from the business | Yes | Lead, qualified lead, sale, call |
| Values available per conversion | Preferred | Transaction values, lead values |
| CRM / offline sales process | Preferred | gclid capture, import schedules |
| Legal/consent requirements | Preferred | Cookie banner, consent mode status |

## Output Contract

Return: (1) a conversion action specification table, (2) implementation steps per action,
(3) a verification checklist with test results, (4) a monitoring plan. Core spec format:

```markdown
| Action | Type | Source | Counting | Value | Primary? | Status |
|---|---|---|---|---|---|---|
| Purchase | Website (ecommerce) | GA4 ecommerce event | Every | Transaction value | Yes | Verified 05-12 |
| Qualified Lead | Website (form) | GTM form submit | One per click | $120 fixed | Yes | Verified 05-12 |
| Call >60s | Call from ads | Ads call tracking | One per call | $45 | Yes | Verified 05-13 |
| Newsletter signup | Website | GA4 import | One per click | $0 | No (secondary) | Live |
```

Rule: primary actions feed bidding; secondary actions report only. One source of truth per
action — either native Ads tags or GA4 import, never both for the same event.

## Workflow

1. Define the taxonomy with the business: every outcome worth paying for, its stage, and its
   value (transaction revenue for e-comm; close-rate-weighted values for lead types).
2. Choose the source of truth per action: native Google Ads tags (fastest for Ads bidding) or
   GA4 key events imported to Ads (unified with analytics) — document the choice to prevent
   later double counting.
3. Implement site actions via Google Tag Manager: form submits, purchase events with value +
   transaction ID, click-to-call, chat starts; use dataLayer ecommerce events for stores.
4. Enable enhanced conversions (hashed first-party email/phone) to recover consent-era gaps;
   align consent mode with the site's cookie banner.
5. Configure counting and windows: one-per-click for lead actions, every-conversion for
   e-comm purchases; set view-through and click windows deliberately, not at defaults blindly.
6. Set values: dynamic transaction values, fixed or tiered lead values, value rules for
   geo/audience adjustments where economics differ.
7. Wire offline conversions: capture gclid (or enhanced conversion IDs) into the CRM, then
   schedule imports of closed-won deals so bidding optimizes toward revenue, not raw forms.
8. Verify end-to-end: Tag Assistant/GTM preview, real test submissions and test purchases,
   conversions visible in Ads within the expected lag, values matching.
9. Stand up monitoring: weekly conversion-volume anomaly checks, monthly GA4-vs-Ads
   discrepancy report (<10% tolerance), and a change log for any tracking edit.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Tag implementation | Google Tag Manager | Free; versioned, testable |
| Site analytics | GA4 | Free; key events + import source |
| Ads-side measurement | Google Ads conversion goals + enhanced conversions | Native |
| Verification | Tag Assistant, GTM preview, test transactions | Free; never ship unverified |
| Offline imports | Google Ads conversion uploads / CRM connectors | gclid-based, scheduled |
| Monitoring | Google Ads Scripts (zero-conversion alerts), Sheets log | Free; catch silent breakage |

## Example AI Prompt

```text
You are a PPC measurement engineer. Set up conversion tracking for {BUSINESS} on
{PLATFORM/CMS}. Conversion taxonomy: {LIST WITH STAGES AND VALUES}. Tools available:
{GTM? GA4? CRM? call tracking?}. Consent status: {BANNER/CONSENT MODE DETAILS}.
Goal: smart bidding on {PRIMARY GOAL} by {DATE}.

Deliver:
1. Conversion action spec table: action | type | source (native Ads vs GA4 import) |
   counting rule | value model | primary or secondary.
2. Implementation steps per action (GTM triggers/variables, dataLayer requirements,
   enhanced conversion setup, offline import process with gclid capture).
3. Verification checklist: test steps, expected observations, pass criteria per action.
4. Monitoring plan: weekly anomaly checks, monthly GA4-vs-Ads discrepancy tolerance (<10%),
   and the change-log format.
Flag any action with missing or unreliable values and propose the value model to use.
```

## Edge Cases & Guardrails

- Double counting is the classic failure: the same form firing both a native Ads tag and a
  GA4 import inflates conversions and ruins tCPA — one source of truth per action.
- Conversion lag misleads daily reads: leads and purchases land days after clicks; judge
  performance on trailing windows and teach the reporting cadence this fact.
- Never make low-value vanity events (page views, video plays) primary — smart bidding will
  happily buy them instead of leads.
- Form spam pollutes lead counts and corrupts bidding; filter obvious spam before counting
  (honeypots, timing checks) and track spam rate.
- Enhanced conversions and consent mode need correct legal configuration — do not quietly
  disable consent features to "fix" tracking gaps.
- Test on real triggers, not Tag Assistant alone: an actual form submission, an actual test
  purchase with visible value in the Ads UI, is the only acceptable verification.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Tag/action coverage | 100% of taxonomy implemented & verified | Any primary action unverified |
| GA4 ↔ Ads conversion discrepancy | <10% | >20% or unexplained drift |
| Conversions with values attached | 100% of primary actions | Value-less tROAS attempts |
| Offline import freshness | Weekly or faster | Never imported / months stale |
| Spam share of tracked leads | <10% | Growing form-spam share |
| Tracking change log | Every edit documented | Silent untracked edits |

## Handoffs

- → **bidding-strategy:** verified data + conversion volume unlocks smart bidding decisions.
- → **budget-management:** value-based reporting feeds marginal-return reallocation.
- → **shopping-campaigns:** purchase values and Merchant Center conversion linkage.
- → **web-analytics-agent:** hand off the taxonomy, events, and consent configuration for
  unified analytics governance.
- ↑ **sem-ppc-agent:** escalate any data-integrity failure immediately — all decisions pause.
