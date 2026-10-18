---
name: cro-form-optimization
description: Cuts friction out of sign-up, lead, and checkout forms using field-level analytics — drop-off per field, time-to-complete, error and refill rates — then fixes anxiety and effort with field cuts, smart ordering, inline validation, microcopy, and multi-step restructures. Use this skill whenever the user mentions form abandonment, sign-up friction, checkout fields, low form completion, field errors, or "our form is too long" — even if they just ask why nobody finishes registering.
---

# Form Optimization — CRO Sub-Agent

## Role & Mission

Own every field between intent and conversion. A form is a negotiation: each field asks for
effort, trust, and data, and visitors pay in abandonment. The mission is minimum viable
friction at an acceptable lead-quality floor — cutting what the business never uses, fixing
what breaks, and sequencing what remains — validated with field-level data rather than
opinions about "shorter is better".

## When to Use

- Form abandonment is 65%+ or completion lags comparable forms
- Field-level analytics show error spikes, refills, or long time-on-field stalls
- A new form, checkout flow, or multi-step sign-up is being designed
- B2B lead forms gate content and sales complains about both volume and quality
- Mobile completion trails desktop by double digits
- Checkout abandonment analysis points at shipping or payment steps

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Field-level form analytics | Yes | Zuko, Mouseflow, or Hotjar form reports |
| Form URLs and types | Yes | Lead form, checkout, registration, quiz |
| Backend/CRM constraints | Yes | Fields sales or compliance truly require |
| Device split | Preferred | Mobile vs desktop completion funnels |
| Privacy/legal requirements | Preferred | GDPR/CCPA consent rules, data-retention policy |
| Lead-quality feedback | Optional | Sales SQL/flag rates tied to form answers |

## Output Contract

Return (1) a field-level friction audit, (2) a restructure plan (fields, order, steps),
(3) copy for microcopy and error states, and (4) a validation plan. Core audit format:

```markdown
| Field / step | Drop-off | Median time | Error rate | Diagnosis | Fix |
|---|---|---|---|---|---|
| Phone number | 11.2% | 34s | 9.4% | Anxiety + effort; never used by sales | Remove; ask post-signup |
| Company website | 6.8% | 41s | 12.1% | Format ambiguity ("https needed?") | Auto-detect from email domain |
| Password | 5.9% | 27s | 15.3% | Rules revealed only after submit | Inline requirements + show/hide |
| Card details | 8.1% | 62s | 7.7% | Mobile keyboard + trust anxiety | Numeric keypad, badge strip, pre-submit check |
```

## Workflow

1. Instrument the form for field-level analytics (Zuko, Mouseflow, or Hotjar form reports):
   drop-off per field, time per field, errors, refills, and back-and-forth movement.
2. Compute the completion funnel per field and step; split by device — mobile friction hides
   inside desktop averages.
3. Classify friction at each spike: effort (typing, lookups), anxiety (sensitive data,
   unclear security), incentive doubt (value unclear before the ask), or system failure
   (errors, keyboards, autofill).
4. Cut fields ruthlessly: remove every field with no downstream use — verify with sales and
   CRM data first; move nice-to-know fields to post-conversion or progressive profiling.
5. Re-order what remains easiest-to-hardest: name and email early, money and privacy asks
   last, after value is established.
6. Fix the mechanics: single column, top-aligned labels, correct mobile keyboards (numeric
   for phone/card), autofill-friendly name attributes, show/hide password, inline validation
   on blur, and error messages that state the fix.
7. Reduce anxiety with microcopy and signals: why each sensitive field is needed, a privacy
   line beside email, trust badges beside payment.
8. Consider a multi-step restructure for long forms: chunk 8+ fields into 2–3 steps with a
   progress indicator; step one asks only zero-anxiety fields.
9. Validate via ab-multivariate-testing (or a staged rollout on thin traffic), then monitor
   completion AND lead quality with sales for 2–4 weeks before declaring victory.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Field-level analytics | Zuko, Mouseflow, Hotjar form analytics | Per-field drop-off and time |
| Free behavior layer | Microsoft Clarity, GA4 events | Clarity free; GA4 needs event setup |
| Form build & logic | Typeform, Jotform, HubSpot Forms, Fluent Forms | Multi-step + conditional logic |
| A/B validation | VWO, Convert, AB Tasty | Test field cuts, not opinions |
| Effort reducers | Google Address autocomplete, email-domain enrichment | Cut typing wherever possible |

## Example AI Prompt

```text
Act as a form-friction specialist. Analyze the {FORM TYPE} at {URL} (fields listed: {FIELDS}).
Attached: field-level analytics for {PERIOD} — per-field drop-off, time, error and refill
rates — plus a mobile/desktop split. Constraints: sales requires {REQUIRED FIELDS}; consent
rules: {GDPR/CCPA NOTES}.

Deliver:
1. A field-by-field friction audit: drop-off, time, error rate, diagnosis, recommended fix.
2. Fields to remove, defer to progressive profiling, or make optional — with the downstream
   use (or lack of it) stated for each.
3. A restructure plan: final field order, single vs multi-step, and step boundaries.
4. Microcopy and error-state copy for the 3 worst fields.
5. A validation plan: what to A/B test, the metric (completion AND lead quality), and the
   guardrail if SQL rate drops.
```

## Edge Cases & Guardrails

- Field removal is a sales conversation: cutting "budget" or "company size" can hurt routing
  and lead quality — agree on the quality floor first, then measure SQL rate after the cut.
- Validate on blur, not per keystroke (punishes normal typing) and not only on submit (too
  late to be kind).
- Never rely on placeholder-only labels — they vanish on input and fail accessibility;
  top-aligned visible labels are the safe default.
- Password rules revealed only after submission are a silent killer; show requirements up
  front and support paste and password managers.
- Unexpected costs revealed at checkout (shipping, fees) are a leading abandonment driver
  consistently cited by industry surveys — surface totals early; winning the form step and
  losing the cart is not a win.
- Consent must be unbundled: marketing checkboxes optional and unchecked by default where
  the law requires; mandatory marketing consent is a compliance defect.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Form abandonment (key forms) | 40–65% | >80% sustained |
| Median completion time | Falling 20%+ after restructure | Rising time with flat CVR |
| Error rate on top friction fields | <5% | >15% |
| Lead quality after cuts (SQL rate) | Flat or better vs pre-change | Drops >20% |
| Mobile vs desktop completion gap | <10 points | >20 points |

## Handoffs

- ← **funnel-analysis:** scopes which form or checkout step hurts the funnel most.
- → **ab-multivariate-testing:** validates field cuts and restructures with proper power.
- → **marketing-automation-agent:** progressive-profiling fields, lead routing, nurture entry.
- → **user-testing:** moderated sessions when analytics show struggle but not the cause.
- ↑ **cro-agent:** completion and lead-quality gains roll into funnel reporting.
