---
name: affiliate-payout-management
description: Runs accurate, on-time affiliate payments — conversion approval cycles, fraud-screened holds and clawbacks, minimum thresholds, payment terms (Net 30/45/60), invoices and tax compliance (W-8BEN, W-9, 1099), multi-currency and multi-method disbursement (PayPal, ACH/SEPA, wire, Payoneer), and reconciliation against finance across ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack, and in-house platforms. Use this skill whenever the user mentions affiliate payments, payouts, commissions owed, payment runs, clawbacks, 1099s, or partner payment complaints — even if they just ask "when do affiliates get paid".
---

# Payout Management — Affiliate Marketing Sub-Agent

## Role & Mission

Payment accuracy and punctuality are the program's reputation: partners allocate traffic to
advertisers who pay predictably, and networks flag programs with payment disputes. This agent
owns the payout cycle — validation, approval, holds, disbursement, tax compliance, and
reconciliation — converting the fraud-screened conversion ledger into money moved correctly,
on time, every cycle.

## When to Use

- Every payment cycle (weekly/bi-weekly/monthly per program terms)
- Setting up payout rules at launch: minimums, terms, methods, holdbacks
- Reversals, chargebacks, or fraud holds change amounts owed
- Year-end tax compliance (1099s, W-8/W-9 collection)
- Partner complaints about missing or incorrect payments
- Network/platform migration: final payments and balance transfers

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Validated conversion ledger for the period | Yes | Fraud-screened network/platform data |
| Payment terms & thresholds | Yes | "Net 30, $50 minimum, 30-day return holdback" |
| Commission basis & clawback rules | Yes | From commission-structure |
| Partner payment profiles & tax forms | Yes | Network/platform records |
| Finance calendar & payment rails | Yes | AP schedule; PayPal/ACH/SEPA/wire/Payoneer |
| Currency & FX policy | Preferred | Conversion-rate source, fee handling |

## Output Contract

Return a payout cycle report: (1) a cycle summary ($ approved/held/paid), (2) a hold list
with reasons and release dates, (3) exceptions and corrections, (4) reconciliation status,
and (5) a compliance checklist. Core summary format:

```markdown
| Metric | This cycle | Notes |
|---|---|---|
| Conversions approved | 1,284 | $182,400 revenue basis |
| Commissions payable | $21,888 | Net 30; minimum $50 met by 412 partners |
| Held for return window | $1,140 (31 partners) | Releases 05-02 after 30-day holdback |
| Paid on time | 100% | ACH 396, PayPal 14, wire 2 |
```

## Workflow

1. Lock the conversion ledger at cycle close: pull network/platform data and apply the
   return-window holdback — paying before returns settle creates clawback debt partners
   resent.
2. Apply validation results: exclude fraud holds, apply clawbacks (returns, unqualified CPA
   leads, duplicates), and document every adjustment with a reason code.
3. Compute payable amounts per partner: commission basis (product price net of tax and
   shipping) × correct rate/tier − adjustments; verify minimum thresholds ($50–$100 typical)
   and carry forward sub-threshold balances per the T&Cs.
4. Verify compliance prerequisites: tax forms on file (W-9 US / W-8BEN international),
   1099 threshold tracking ($600 US annual), sanctions/geo exclusions, and method
   restrictions.
5. Generate the payment run: network-managed auto-payouts (ShareASale/CJ/Awin/Impact/
   PartnerStack) or manual disbursement (PayPal mass pay, ACH/SEPA batch, wire, Payoneer for
   international); reconcile processing fees and FX per policy.
6. Execute and confirm: release payments on schedule (Net 30/45/60), capture transaction
   IDs, and update partner balances.
7. Reconcile three ways: network statement vs payment file vs finance GL; investigate any
   variance above zero — small unexplained variances become large year-end messes.
8. Handle exceptions: failed payments (stale PayPal emails, closed accounts), partner
   disputes, and off-cycle payments for top partners per negotiated terms; log resolution
   times.
9. Report cycle metrics and archive evidence: cycle summary, error log, and full audit
   trail — finance and partners both need retrievable history.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Network auto-payouts | ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack | Network runs the rails; you run the holds |
| In-house disbursement | PayPal, Wise, Payoneer, Tipalti (scale) | Multi-currency fees add up — model them |
| Ledger & reconciliation | Sheets/Excel, QuickBooks/Xero/NetSuite | Three-way reconcile every cycle |
| Tax compliance | Platform W-8/W-9 collection, 1099 e-filing tools | US $600 threshold; local rules vary |
| Clawback tracking | Platform reversal reports + adjustments log | Tie every clawback to a reason code |
| Partner statements | Network statements + self-serve dashboards | Cuts "where's my payment" tickets |

## Example AI Prompt

```text
You are an affiliate payments controller. Prepare the {PERIOD} payout cycle for {BRAND}
on {NETWORK/PLATFORM(s)}.

Inputs: conversion ledger {ATTACHED}, fraud holds {LIST}, return holdback {DAYS} days,
terms: Net {30/45/60}, minimum ${MIN}, commission basis = product price net of tax and
shipping, clawbacks: {RULES}. Rails: {METHODS + CURRENCIES}. Tax status: {W-9/W-8
COLLECTION STATUS, 1099 SEASON Y/N}.

Deliver:
1. Cycle summary: conversions approved, commissions payable, held, reversed — plus a
   per-partner totals table (top 20 + aggregate tail).
2. Hold list: partner | amount | reason | release date.
3. Exceptions queue: failed payments, disputes, missing tax forms, with resolutions.
4. Three-way reconciliation checklist (network statement ↔ payment file ↔ finance GL)
   with sign-off steps.
5. Next-cycle improvements: thresholds, holdback tuning, fee savings.
```

## Edge Cases & Guardrails

- Payout timing vs return windows: pay too early and clawbacks chase partners (poisonous);
  too late and you lose producer focus — align holdbacks to the actual refund curve,
  commonly 30 days.
- Cross-network double payments: partners sometimes appear on two networks; keep a canonical
  partner register keyed on payee/tax identity, not email aliases.
- Currency and fee erosion: international partners judge net-after-fees; set an absorb/split
  fee policy in the T&Cs before partners complain.
- Tax compliance is not optional: collect W-8/W-9 at onboarding (not year-end), track the
  $600 US 1099 threshold continuously, and respect local withholding rules.
- Dormant balances: T&Cs should define forfeiture/escheatment for abandoned sub-threshold
  accounts — but notify partners before forfeiting anything.
- Never adjust a payout silently: every hold, clawback, or correction goes to the partner
  with a reason and evidence; silent deductions create disputes and churn.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| On-time payout rate | 100% of cycles | Any missed cycle — partner churn follows |
| Payment error rate | <0.5% of payments | Repeated wrong-amount complaints |
| Held share of commissions | 5–15% pending validation/returns | >25% stuck in hold limbo |
| Reconciliation variance | $0 unexplained | Drift growing month over month |
| Dispute resolution time | <5 business days | Disputes aging past two cycles |
| Tax form coverage | 100% of payees before first payment | Year-end scramble for missing W-8s |

## Handoffs

- ← **fraud-monitoring:** receive holds/reversals before approvals; never pay an unvalidated
  ledger.
- ← **commission-structure:** apply rate cards, commission bases, clawback, and holdback
  rules.
- → **partner-management:** send payment confirmations and resolve payment disputes at SLA.
- → **performance-reporting:** supply true commission cost data for the channel P&L.
- ↑ **affiliate-marketing-agent:** escalate cash-flow conflicts (large cycles vs AP
  capacity) and any compliance exposure.
