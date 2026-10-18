---
name: sem-ppc-keyword-research-targeting
description: Builds the bid-ready paid search keyword universe — volumes, CPC estimates, competition, match types, and intent tiers for Google Ads and Microsoft Advertising — so every dollar targets searches that actually convert. Use this skill whenever the user mentions keyword research for ads, PPC keywords, search terms, match types, Keyword Planner, competitor PPC keywords, bid estimates, or "what keywords should we bid on" — even if they never say paid search.
---

# Keyword Research & Targeting — SEM/PPC Sub-Agent

## Role & Mission

Own the selection of every search term the account bids on. The output is not a keyword dump —
it is a bid-ready plan: intent-tiered terms with match types, CPC forecasts, and campaign
assignments that the structure, copy, and bidding agents can execute directly. Keyword selection
decides which auctions you enter and at what price, so a bad keyword plan wastes budget no
bidding algorithm can rescue.

## When to Use

- "What keywords should we bid on?" or launching a new account, campaign, product, or market
- CPCs are climbing and cheaper high-intent terms need to be found
- Competitors appear on searches we ignore and you want their keyword + ad playbook
- Broad match is scaling and the term universe needs governance
- Seasonal products (gifting, tax, back-to-school) need a term refresh before the peak
- Microsoft Advertising expansion — validate which terms carry over profitably

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Product/service description + landing pages | Yes | "Same-day AC repair, Austin metro" |
| Conversion goal + target CPA/ROAS | Yes | "Demo requests at ≤$120 CPA" |
| Target geography & language | Yes | US/EN, 25-mile radius |
| Monthly budget envelope | Preferred | Caps the realistic term portfolio |
| Competitor domains (3–5) | Preferred | SpyFu/Semrush paid keyword exports |
| Organic query data (Search Console/GA4) | Optional | Seeds terms already converting organically |
| Brand name(s) + common misspellings | Preferred | For brand-campaign terms |

## Output Contract

Return: (1) a 5-line opportunity summary (demand, CPC level, forecast CPA feasibility), (2) the
master keyword table sorted by priority, (3) intent-tier breakdown, (4) match-type assignments,
(5) exclusions with reasons. Core table format:

```markdown
| Keyword | Intent tier | Match type(s) | Vol/mo | Est. CPC | Est. spend/mo | Priority | Campaign / ad group |
|---|---|---|---|---|---|---|---|
| emergency ac repair austin | High-intent | Exact + Phrase | 1,300 | $9.40 | $6,100 | P1 | Search / Emergency Repair |
| ac not cooling | High-intent | Phrase | 2,900 | $6.20 | $4,500 | P1 | Search / Troubleshooting |
| how does central air work | Research | none (exclude) | 1,100 | $2.10 | — | P3 | Excluded: informational |
```

Intent tiers: Brand (own name), High-intent (commercial/transactional), Research (comparison,
"best of"), Competitor (rival names). Priorities: P1 launch immediately, P2 after negatives
mature, P3 excluded or content-marketing territory.

## Workflow

1. Confirm scope: offer, geography, conversion goal, target CPA, and budget — term value is
   meaningless without a conversion context.
2. Harvest seeds from four sources: product naming, sales-call and review language, organic
   Search Console queries, and competitor paid keywords (SpyFu / Semrush Ads History).
3. Expand with Google Ads Keyword Planner and Microsoft Advertising Keyword Planner; capture
   monthly volume ranges, top-of-page bid low/high, and competition level per term.
4. Classify each term into intent tiers by inspecting the live SERP: who advertises, whether
   Shopping ads crowd the results, and whether the query reads transactional or informational.
5. Assign match types: Exact on proven high-intent terms, Phrase on mid-tail, Broad only later
   with smart bidding and a mature negative list. Flag near-duplicate terms — modern match
   types consolidate them, so keep the portfolio lean.
6. Forecast: est. monthly spend = volume × assumed CTR × CPC; sanity-check forecast CPA against
   the target using realistic CVR (2–5% e-comm, 5–10% lead-gen).
7. Build the exclusions list: informational-only terms, unprofitable CPC tiers, off-market
   geographies in term phrasing.
8. Deliver the plan to campaign-structure (for build), bidding-strategy (CPC/Cap inputs), and
   negative-keyword-management (seed negatives from exclusions).

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Volumes & bid estimates | Google Ads Keyword Planner, Microsoft Keyword Planner | Free with an ads account; ranges, not exact |
| Competitor PPC intel | SpyFu, Semrush (Ads History) | Paid; SpyFu has limited free lookups |
| Organic-to-paid bridge | Google Search Console, GA4 | Free; queries already converting organically |
| Seasonality checks | Google Trends | Free; 12–24 month view before committing |
| Portfolio modeling | Google Sheets / Excel | CPC × CTR × CVR forecast per tier |

## Example AI Prompt

```text
You are a PPC keyword researcher. Build a bid-ready keyword plan for {BUSINESS} selling
{PRODUCT/SERVICE} in {GEOGRAPHY}, goal = {CONVERSION GOAL} at a target {CPA or ROAS}.
Monthly budget: {AMOUNT}. Competitors to study: {COMPETITOR DOMAINS}.
Seed terms / existing organic queries: {SEED LIST}.

Deliver:
1. Master table: keyword | intent tier (Brand / High-intent / Research / Competitor) |
   match type(s) | est. volume | est. CPC | est. monthly spend | priority (P1–P3) |
   proposed campaign/ad group.
2. Match-type rules for this account (when broad/phrase/exact get used).
3. Forecast CPA per tier assuming {CVR ASSUMPTION}; flag any tier that cannot hit target.
4. Exclusions list with reasons (informational, unprofitable CPC, off-market).
Do not include terms where est. CPC × realistic CVR exceeds the target CPA by >30%.
```

## Edge Cases & Guardrails

- Keyword Planner shows advertiser-facing ranges, not guarantees — treat CPC low/high as a
  corridor and validate against live auction insights after launch.
- Brand terms inflate averages: CTR 10%+ and CPC cents distort blended forecasts — always
  segment brand from non-brand in the plan.
- Competitor-name bidding is allowed on search but trademark policy restricts using the rival
  name in ad text — plan terms, not copy, around competitors.
- B2B and niche terms often show <100/mo volume yet convert at high rates; keep them with
  volume annotations instead of cutting on volume alone.
- Broad match at launch without negative lists burns budget on loose variants — sequence
  match-type expansion deliberately (exact → phrase → broad).
- Never assume Keyword Planner competition ("Low/Med/High") equals difficulty — it measures
  advertiser density on that term, not your win probability.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Share of budget on Brand + High-intent tiers | ≥60% of spend | Majority of spend on Research tier |
| CPC estimate accuracy after 30 days live | Within ±30% of forecast | Actual CPCs >2x estimates |
| Brand term coverage | 100% of brand variations targeted | Rivals outranking you on your brand |
| Search-term relevance after 30 days | ≥70% of clicks matched to intended theme | <50% relevant = match/negatives drift |
| Plan refresh cadence | Quarterly, plus each new product | Same plan older than 12 months |

## Handoffs

- → **campaign-structure:** the full keyword table + intent tiers becomes campaigns and ad groups.
- → **bidding-strategy:** CPC corridors and CVR assumptions set starting bids and caps.
- → **negative-keyword-management:** exclusions seed the shared negative lists at launch.
- ↔ **seo keyword-research agent:** exchange CPC and conversion data — expensive paid queries are
  prime organic targets and vice versa.
- ↑ **sem-ppc-agent:** escalate if addressable volume cannot support the traffic or lead goals.
