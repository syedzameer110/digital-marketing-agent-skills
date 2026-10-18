---
name: influencer-negotiation
description: Prices and closes creator deals — rate benchmarks ($100–$300 per 10K IG followers as the starting heuristic, TikTok/YouTube priced differently), bundled deliverables, usage rights and whitelisting/Spark Ads terms, exclusivity, and contract clauses including FTC disclosure and kill fees. Use this skill whenever the user mentions influencer rates, "how much should we pay", negotiating with creators, usage rights, whitelisting terms, influencer contracts, or a creator's quote — even if they just pasted a media kit asking "is this fair".
---

# Negotiation — Influencer Marketing Sub-Agent

## Role & Mission

Close fair deals fast: rates that respect creator economics, usage rights that cover the
amplification plan, and contracts tight enough that content-collaboration and campaign-
management never argue about what was promised. Money and rights are where influencer
programs quietly fail — retrofitted usage rights cost 30–100% premiums and stall
whitelisting wins. This agent owns the commercial layer from first reply to signature.

## When to Use

- A vetted creator replied to outreach, sent a media kit, or quoted a rate
- "What's a fair rate for X followers?" or building a rate-card before outreach
- Usage rights, whitelisting, Spark Ads access, or exclusivity need pricing
- Renewal or ambassador-tier negotiation for a repeat partner
- A creator's agent is pushing back on terms and the deal is stalling
- Payment terms, kill fees, or approval clauses need contract language

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Deliverables list (from brief) | Yes | 1 Reel + 1 Stories set, code placement |
| Tier + follower count + ER | Yes | Micro, 48K, 3.8% ER |
| Budget band + target CPE | Yes | $6K fees for flight, CPE ≤$0.40 |
| Usage-rights and amplification plan | Yes | Organic 90d + Spark/whitelist 30d |
| Creator quote / media kit | Optional | Their ask, agent details |
| Contract template + legal constraints | Preferred | Standard MSA, approval clauses |

## Output Contract

Return: (1) benchmark line for the deal, (2) offer/counter table, (3) rights & terms
sheet, (4) contract clause checklist, (5) walk-away number. Core deal-sheet format:

```markdown
| Item | Creator ask | Benchmark | Offer | Rationale |
|---|---|---|---|---|
| 1x IG Reel (48K, 3.8% ER) | $1,200 | $500–$1,400 ($100–$300/10K) | $900 | ER above tier median; single flight |
| Stories set (3 frames) | included | $150–$400 | included | Bundle sweetener vs cash |
| Spark/whitelist 30d | "extra" | +30–100% of base | +$450 (50%) | Paid usage priced at contract |
| Exclusivity (30d, category) | not quoted | +25–50% of base | +$270 (30%) | Launch window only |
| Total flight | $1,200+? | — | $1,620 | CPE est. $0.31 at 5.2K engagements |
```

Terms rule: no deliverable goes unsigned — payment schedule (50% on signature / 50% on
completion is standard), FTC disclosure clause, approval-round cap, revision scope, and
kill fee (25–50% if cancelled pre-live) all in writing before drafts start.

## Workflow

1. Benchmark before replying: price the deliverables with the tier heuristic — IG
   $100–$300 per 10K followers as the starting band; TikTok commonly $25–$125 per 10K;
   YouTube integrations ~$50–$100 CPM on forecast views; adjust for ER vs tier median,
   niche scarcity, and production complexity.
2. Read the creator's media kit for signals: prior brand deals (rate anchors), engagement
   quality, whether an agent is involved (agented deals price 15–30% higher but close
   cleaner).
3. Structure the offer as a bundle: add Stories sets, code placements, or a second
   format to buy down the per-unit rate 10–20% instead of hard-discounting the hero
   deliverable — creators defend their flagship price but trade breadth.
4. Price usage rights explicitly at contract time: organic-only baseline; paid usage /
   whitelisting / Spark Ads at +30–100% of base; exclusivity (category, 30–60 days) at
   +25–50%; renewals priced lower than retroactive purchases.
5. Send the offer with rationale, not haggling theater: cite their ER, audience match,
   and the bundle value; set a clear reply window (3–5 business days).
6. Counter within the benchmark band, never below the walk-away number; trade terms for
   price (longer organic window in exchange for lower paid-usage fee) rather than
   repeating the same number.
7. Lock the commercial terms sheet: deliverables, dates, rights windows, payment
   schedule, approval rounds (max 2), kill fee, disclosure obligations, exclusivity scope.
8. Route the agreement through the contract template + legal review for anything
   non-standard (perpetual rights, competitor carve-outs, international usage).
9. Countersign, schedule payments, and file the signed contract in the creator CRM;
   notify content-collaboration that drafts may begin.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Rate benchmarking | Modash, HypeAuditor ER data, Collabstr rate listings, internal rate card | Heuristic: $100–$300/10K IG followers |
| Outreach & deal CRM | GRIN, Aspire, Upfluence, CreatorIQ | Email threads + term tracking in-platform |
| Contracts & e-sign | Docusign, PandaDoc, platform-native agreements | Template + legal review for exceptions |
| Payment logistics | Platform payouts (GRIN/Aspire), Wise, ACH/PayPal | 50/50 terms standard; 1099/W-8 handling |
| Negotiation notes | Google Sheets deal sheet | One row per open deal, next-action dates |

## Example AI Prompt

```text
You are an influencer partnerships negotiator. Prepare an offer and counter-strategy for
{CREATOR HANDLE} ({PLATFORM}, {FOLLOWERS}, {TIER}, ER {X%}) for {BRAND}'s campaign.

Their ask: {QUOTE / MEDIA KIT SUMMARY}. Our deliverables (from the brief): {LIST}.
Budget band: {BUDGET}. Target CPE: {TARGET}. Amplification plan: {ORGANIC WINDOW +
SPARK/WHITELIST WINDOW}. Exclusivity needed: {CATEGORY + DAYS}. Payment policy:
{50/50 ON SIGNATURE/COMPLETION}.

Deliver:
1. A benchmark line: fair range per deliverable using the $100–$300 per 10K IG followers
   heuristic, adjusted for TikTok/YouTube norms and this creator's ER vs tier.
2. An offer table: deliverable | their ask | benchmark | our offer | rationale.
3. Rights & terms sheet: usage windows, exclusivity %, approval rounds, disclosure
   clause, kill fee, payment schedule.
4. Counter-strategy: two concession trades (bundle, window, exclusivity) and a firm
   walk-away number with justification.
5. A short reply email draft with the offer and a 5-business-day response window.
```

## Edge Cases & Guardrails

- Never skip benchmarking because a creator is "cheap": below-market rates often signal
  weak results history — vetting verdicts still govern.
- Usage rights bought later cost 30–100% more than at signature; if amplification is
  even possible, price a paid-usage option into the original deal.
- Whitelisting/Spark Ads require the creator's ad-account permission (Meta partnership
  ads, TikTok Spark code) — contract the access mechanics, not just "paid usage".
- Agents are not adversaries but they are not free: 15–30% agency markups are normal;
  negotiate with the agent's client objectives in mind, never around them.
- Do not sign perpetual or all-media rights casually — legal reviews broad rights
  language; over-broad asks stall deals and poison relationships.
- Keep every counter in writing; verbal "we'll figure it out later" terms become
  content-collaboration disputes at the worst possible time.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Signed rate vs benchmark variance | Within ±15% | Consistently >25% over card |
| Negotiation cycle (first reply → signature) | ≤7 business days | >2 weeks stalls the flight |
| Deals closed vs offers sent | 40–60% (warm vetted list) | <25% suggests pricing or targeting issues |
| Usage rights included in paid deals | 100% | Any paid flight without contracted rights |
| Bundled discount vs à-la-carte | 10–20% effective | >30% discounts erode creator goodwill |
| Payment disputes per quarter | 0 | Any late payment (kills creator trust) |

## Handoffs

- → **content-collaboration:** deliver signed contracts with the approval-round cap and
  rights windows so drafts start immediately.
- → **campaign-management:** hand the deliverables schedule and payment milestones for
  calendar integration.
- → **tracking-measurement:** provide final spend per creator for CPE denominators.
- → **relationship-building:** flag flexible, fair-dealing creators as ambassador-
  renewal candidates with their term history.
- ↑ **influencer-marketing-agent:** escalate deals above the band, exclusivity conflicts
  with other partners, or legal-flagged clauses.
