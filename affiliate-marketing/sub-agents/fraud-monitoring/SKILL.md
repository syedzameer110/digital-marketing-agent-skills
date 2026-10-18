---
name: affiliate-fraud-monitoring
description: Detects and blocks affiliate fraud before it reaches payouts — cookie stuffing, forced clicks, click flooding, brand-bidding violations, incentivized and fake conversions, stolen or leaked promo codes, geo/device anomalies, using click logs, conversion timing, and partner baselines across Impact, Everflow, ShareASale, CJ, Awin, Rakuten, and in-house stacks. Use this skill whenever conversions look suspicious, reversal rates spike, a partner's CR or EPC looks impossible, or anyone mentions affiliate fraud, cookie stuffing, or traffic quality — even proactively before each payout cycle.
---

# Fraud Monitoring — Affiliate Marketing Sub-Agent

## Role & Mission

Protect program economics from conversions that should never be paid. Affiliate fraud is
quiet and cumulative — 2% of conversions leaking monthly is a silent tax that compounds and
erodes finance's trust in the channel. This agent owns the pre-payout validation workflow:
baseline every partner, alert on deviation, investigate with evidence, and hand a clean
ledger to payout-management. Prevention is cheap; clawbacks are painful.

## When to Use

- Every payout cycle: mandatory validation pass before approvals
- A partner's conversion rate or EPC jumps implausibly week over week
- Click-to-conversion times look non-human (seconds, or 0:00)
- The brand team reports competitors' ads on brand terms
- Reversal/chargeback rates rise
- A new partner bursts out of nowhere with high volume

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Click + conversion logs with timestamps/IP/device | Yes | Network reports, platform APIs, Everflow |
| Partner baselines (CR, EPC, AOV, geo mix) | Yes | Rolling 90-day per-partner stats |
| Promo code mapping & redemption data | Yes | From tracking-setup |
| Paid-channel click data | Preferred | For brand-bid and dedup checks |
| Return/chargeback feeds | Preferred | Commerce platform |
| Policy set & enforcement ladder | Yes | From program-setup |

## Output Contract

Return a fraud review pack: (1) a cycle verdict (clean vs flagged counts, $ at risk), (2) the
flagged-conversions table with evidence, (3) partner risk scores, and (4) actions taken with
follow-ups. Core flag format:

```markdown
| Conv/Click ID | Partner | Pattern | Evidence | Risk | Action |
|---|---|---|---|---|---|
| C-88412 | PartnerA | Conversion 4s after click, 3rd this week | Click log 0:04 gap; VPN IP range | High | Hold; request explanation |
| C-88701 | PartnerB | 62 conversions, CR 14% vs 2.4% baseline | Device fingerprint reuse; one metro cluster | High | Suspend; reverse pending |
| C-89022 | PartnerC | Brand-term ad on 03-12 | Screenshot + ad-library capture | Medium | Warning letter; 7-day deadline |
```

## Workflow

1. Build per-partner baselines on a rolling 90 days: conversion rate, EPC, AOV,
   new-customer share, geo/device mix, click-to-sale timing — deviation means nothing
   without a baseline.
2. Automate the alert set: CR >2–3x baseline, conversions under 60 seconds after click,
   identical device fingerprints in bursts, impossible geo jumps, datacenter/VPN/proxy
   traffic spikes, and sudden code redemptions in unaligned geographies.
3. Screen every conversion before the payout lock date: check timing plausibility,
   code-to-partner match, and dedup conflicts with paid channels; tag suspects for hold.
4. Investigate cookie stuffing: conversion paths with implausibly many prior "clicks"
   (hidden or tiny iframes, auto-load pixels), zero visible landing behavior, and click
   floods preceding sales — timing and session data beat gut feel.
5. Investigate brand bidding and forced clicks: capture SEM ad evidence (screenshots,
   ad-library timestamps) and test partner properties for auto-redirects or hidden iframes.
6. Correlate with returns and chargebacks: fraud clusters often reverse later; a rising
   reversal cluster on one partner is corroborating evidence.
7. Act on the enforcement ladder with documented evidence: hold conversions → request
   explanation → warn with deadline → suspend → terminate; reverse only with a solid case,
   and log everything for network disputes.
8. Close gaps with tracking-setup: block unknown codes, tighten code allowlists, add
   IP/device rules, and fix any dedup logic the fraudster exploited.
9. Report monthly: fraud rate vs target (<2% of conversions), $ saved, false-positive rate,
   and top risk patterns — feed patterns back into alert thresholds.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Click/conversion forensics | Impact, Everflow | S2S logs, timing, device data |
| Network validation tools | ShareASale/CJ/Awin/Rakuten fraud flags | Configure network filters; never trust blindly |
| SEM brand-bid detection | Manual SERP checks, ad-library alerts, BrandVerity (enterprise) | Even weekly manual checks catch most cases |
| Code abuse detection | Checkout logs, code redemption exports | Unknown-code blocks + redemption anomalies |
| IP/device intelligence | VPN/proxy detection lists (MaxMind-style) | Score, don't auto-reject — false positives cost partners |
| Case log | Sheets/CRM evidence register | Screenshots, timestamps, decisions |

## Example AI Prompt

```text
You are an affiliate fraud analyst. Review this payout cycle for {BRAND} on
{NETWORK/PLATFORM}. Attachments: conversion ledger {PERIOD}, click logs, 90-day partner
baselines, code redemption export.

Baselines: median CR {X}%, median click-to-sale {Y}s, new-customer share {Z}%.
Schemes to check: cookie stuffing (hidden iframes, click floods), forced clicks,
incentivized signups, leaked/stolen codes, brand bidding, dedup conflicts with
{PAID CHANNELS}.

Deliver:
1. Cycle verdict: clean vs flagged counts and $ at risk.
2. Flagged-conversions table: ID | partner | pattern | evidence | risk (High/Med/Low) |
   recommended action (hold / reverse / warn / suspend).
3. Partner risk scores with the top-5 investigation queue and exact evidence to collect.
4. Gaps to close with tracking (code allowlist, IP/device rules, dedup tweaks).
5. Alert-threshold changes for next cycle. Do not recommend reversal without evidence.
```

## Edge Cases & Guardrails

- False positives cost real money too: a loyal buyer converting 30 seconds after their own
  click is rare but real — score risk and require corroboration (device, geo, history)
  before reversing.
- Cookie-stuffing signatures: conversions preceded by dozens of "clicks", clicks from
  hidden 1×1 iframes, or click storms at page load with no visible interaction.
- Never accuse or terminate without a saved evidence pack (screenshots, logs, timestamps);
  networks and partners will challenge it, and you will lose the dispute and your credibility.
- Brand-bid monitoring must cover the partner's actual geo/language, not just yours —
  violations usually appear in markets you do not check.
- Incentivized traffic often passes CR screens: watch new-customer quality (repeat rate,
  email validity, chargebacks), not just volume.
- Small programs are not exempt: fraud scales down, it does not disappear — a 20-partner
  program still needs the pre-payout screen, just lighter.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Fraud/invalid conversion rate | <2% of conversions | >5% or rising monthly |
| Conversions screened before payout | 100% | Paying before validation |
| Time to detect a scheme | <7 days from first signal | Discovered at quarter-end reconcile |
| False-positive rate on holds | <20% of holds later released | Trust damage from constant false accusations |
| Partner churn from false positives | ~0 | Top partners leaving over disputes |

## Handoffs

- → **payout-management:** deliver the validated ledger with holds/reversals applied before
  approvals.
- → **partner-management:** hand enforcement cases with evidence for the ladder and comms.
- → **tracking-setup:** request gap fixes (code allowlist, IP/device rules, dedup changes).
- → **performance-reporting:** flag contaminated data periods and partner exclusions.
- ↑ **affiliate-marketing-agent:** escalate systemic patterns (network-wide leakage, legal
  exposure, partner account takeover).
