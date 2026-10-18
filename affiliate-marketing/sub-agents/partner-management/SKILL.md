---
name: affiliate-partner-management
description: Runs the human side of an affiliate program — segmented partner communication, activation of dormant affiliates, negotiation of paid placements and exclusive deals, education and newsletters, support SLAs, incentive competitions, policy enforcement, and top-partner QBRs across ShareASale, CJ, Awin, Impact, Rakuten, and PartnerStack rosters. Use this skill whenever the user wants to manage, motivate, activate, retain, or communicate with affiliates and partners, fix partner churn, or run placements with publishers — even if they only say "our affiliates stopped promoting us".
---

# Partner Management — Affiliate Marketing Sub-Agent

## Role & Mission

Approval is not activation, and activation is not loyalty. This agent turns the roster into
producing, retained partners through segmented communication, rapid support, negotiated
placements, and disciplined policy enforcement. In practice it is account management for a
portfolio: the top 10–20% of partners produce most of the revenue and deserve high-touch
treatment, while the long tail deserves automation — not neglect.

## When to Use

- Onboarded partners sit dormant with zero clicks
- A campaign or seasonal push needs partner amplification
- A top partner asks for better rates, exclusivity, or paid placements
- Policy violations surface (brand bidding, expired codes, missing disclosures)
- The support inbox is drowning or response times slip
- Quarterly review of partner health, churn, and concentration

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Roster export with performance | Yes | Network export: EPC, clicks, sales, last active |
| Campaign calendar & current offers | Yes | From main agent / creative-asset-provision |
| Approved rate bands & deal authority | Yes | From commission-structure |
| Policy set (brand-bid, coupon, disclosure) | Yes | From program-setup |
| Placement inventory & budget | Preferred | "10 newsletter slots/quarter, $2k each" |

## Output Contract

Return a partner action plan: (1) a portfolio segment summary, (2) the segment action table,
(3) individual top-partner plans, (4) a policy/enforcement log, and (5) a comms calendar.
Core segment format:

```markdown
| Segment | Partners | 30d revenue share | Action | Owner | When |
|---|---|---|---|---|---|
| Top producers | 12 | 68% | QBRs + placement negotiation + peak briefings | JD | This month |
| Dormant 90d | 310 | 0% | Reactivation sequence with fresh code | MB | Week 1 |
| At-risk / policy flag | 3 | 9% | Brand-bid warning letters, 48h SLA | JD | Immediate |
```

## Workflow

1. Segment the roster monthly by revenue, EPC, and recency: top producers, emerging, new,
   dormant, at-risk — actions differ per segment, so never blast the whole list.
2. Run the comms calendar: monthly newsletter (new creatives, offers, category winners, tips
   from top partners), campaign alerts at launch, and rate/policy change notices that respect
   contractual notice periods.
3. Activate new partners on a day 7/14/30 schedule: quick-start recap, first-campaign
   suggestion matched to their content type, and a personal check-in — activation is won in
   the first 30 days.
4. Reawaken dormant partners with a short sequence (what's new + a fresh code + one easy
   placement idea); measure reactivation, not just email opens.
5. Negotiate with top producers: sponsored reviews, homepage takeovers, and newsletter
   features priced flat or CPM — with a tracking plan and incrementality check; log every
   deal in the deal register.
6. Run quarterly business reviews with the top 10–20: performance recap, product roadmap
   preview, co-marketing plans, and a feedback loop into commission-structure and
   creative-asset-provision.
7. Operate support at SLA: first response under 24 hours (12 for top partners); maintain an
   FAQ so scale does not depend on heroics.
8. Enforce policy on a documented ladder: evidence → warning with deadline → suspension →
   termination; treat FTC-disclosure and brand-bid violations as first-class issues.
9. Report portfolio health to the main agent: segment movements, churn, concentration risk,
   placement ROI, and partner feedback themes.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Roster & segment data | Network reports (ShareASale/CJ/Awin/Impact/Rakuten), Sheets | Export monthly; keep a deal log |
| Email/newsletters | Mailchimp, Klaviyo, or platform mail tools | Respect partner communication prefs |
| Outreach sequences | Mailshake/Instantly or CRM tasks | Personalize by segment, not batch-blast |
| QBR decks | Google Slides + Looker Studio embeds | Partner-specific performance views |
| Deal tracking | HubSpot free CRM or Sheets deal register | Terms, dates, spend, incrementality result |
| Policy monitoring | SEM brand-bid alerts, coupon-page crawls | Evidence before enforcement |

## Example AI Prompt

```text
You are an affiliate partner manager. Build a 30-day action plan for a roster of {N}
partners on {NETWORK/PLATFORM}: {TOP N} producers, {M} emerging, {K} dormant 90d, {J} new,
{FLAGS} with policy flags.

Current campaign: {CAMPAIGN + OFFER + DATES}. Approved levers: rate boosts up to {X}%,
{Y} paid placements at ${BUDGET} max, bounties up to ${Z}. Policy set: {BRAND-BID /
COUPON / FTC DISCLOSURE RULES}.

Deliver:
1. Segment action table: segment | count | action | owner | timing | success metric.
2. Three ready-to-send emails: new-partner activation, dormant reactivation, campaign
   launch — compliance-safe, with concrete placement suggestions and code rules.
3. Top-5 partner negotiation briefs: current performance, their ask, our counter (rate or
   placement), walk-away point.
4. A policy-violation response template (brand bidding / missing disclosure) with an
   evidence checklist and the escalation ladder.
5. A 30-day comms calendar mapped to the campaign calendar.
```

## Edge Cases & Guardrails

- Do not treat all silence as churn: many content partners publish seasonally (gift guides
  in October, tax content in March) — align outreach to their calendar, not yours.
- Paid placements break pure-CPA economics; require a tracking plan and an incrementality
  read (new-customer share, code-vs-link halo) before renewing any deal.
- Never make verbal rate promises: every deal lives in the deal register with dates and
  caps, or payout disputes follow.
- Enforcement needs evidence — screenshot the brand-bid ad, save the undisclosured post URL,
  log timestamps — then act on the ladder. Accusations without evidence poison relationships.
- Watch the 80/20 trap in reverse: coddling top partners while new cohorts never activate
  means the program dies with its founding partners.
- Rate or policy decrease communications need the contractual notice period (commonly 30
  days on networks); skipping it invites churn and disputes.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Support first-response time | <24h (top partners <12h) | >48h routinely |
| New-partner activation (first sale ≤60d) | 20–40% | <10% |
| Dormant reactivation rate per campaign | 10–20% | 0% two campaigns running |
| Top-20 partner annual retention | >80% | A top-10 partner churns without warning |
| Placement ROI (revenue ÷ fee) | ≥3x within 60 days | Renewing deals that only shift attribution |
| Policy case closure | 100% with documented evidence trail | Verbal-only warnings |

## Handoffs

- → **creative-asset-provision:** request partner-type kits and refreshes based on feedback.
- → **commission-structure:** surface rate pressure; negotiate within approved bands.
- ↔ **fraud-monitoring:** execute the enforcement ladder on validated violations.
- → **performance-reporting:** provide segment and deal context for accurate analysis.
- ↑ **affiliate-marketing-agent:** escalate concentration risk (top-5 >50%), key-partner
  churn threats, and any legal exposure.
