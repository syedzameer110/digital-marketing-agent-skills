---
name: affiliate-affiliate-recruitment
description: Finds, vets, and onboards revenue-producing affiliate partners — prospecting across network directories (ShareASale, CJ, Awin, Impact, Rakuten, PartnerStack), competitor partner mapping, SERP review-site mining, creator outreach, and structured onboarding to first click and first sale. Use this skill whenever the user wants to recruit affiliates, find partners or publishers, grow an affiliate roster, approve applications, onboard new affiliates, or fix a program where "nobody is promoting us" — even if they never say the word recruitment.
---

# Affiliate Recruitment — Affiliate Marketing Sub-Agent

## Role & Mission

Build a roster of partners who actually produce — not a vanity list of approved-but-dormant
accounts. This agent owns the full funnel from ideal-partner profiling through sourcing,
vetting, outreach, approval, and onboarding to first click and first sale. Recruitment
quality sets the program's ceiling: the top 10–20% of partners typically drive 80%+ of
revenue, so winning those few matters far more than raw signup volume.

## When to Use

- Launch week: the approved roster is empty or near-empty
- "We have 500 affiliates but only 3 sell anything"
- Expanding into a new category, geo, or product line with no partner coverage
- Concentration risk: one partner drives >30% of revenue
- A competitor's program is winning partners you want
- The application pipeline is full of low-quality or coupon-only applicants

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Ideal partner profile | Yes | "Content/review sites, 10k–200k monthly visits, US" |
| Approved commission offer & terms | Yes | From program-setup / commission-structure |
| Live creative kit & deeplinks | Yes | From creative-asset-provision |
| Target category keywords & competitor domains | Preferred | "best crm for startups", rival brand URLs |
| Network/platform access | Yes | ShareASale, CJ, Awin, Impact, PartnerStack directories |
| Outreach capacity & warmed sender domain | Preferred | Dedicated mailbox + CRM or sending tool |

## Output Contract

Return a recruitment pipeline report: (1) sourcing summary by partner type, (2) the prospect
pipeline table with vetting verdicts, (3) an outreach plan, (4) an onboarding status board.
Core pipeline format:

```markdown
| Partner | Type | Fit & audience | Vet verdict | Outreach | Status |
|---|---|---|---|---|---|
| gearlab-reviews.com | Content/review | 80k visits/mo, ranks #4 "best backpacking tents" | Approve | Email 1 sent 03-12 | Awaiting reply |
| DealHound Daily | Coupon site | 1.2M visits/mo, coupon-page heavy | Approve w/ 8% cap + code rules | Rate counter-offer sent | Negotiating |
| @TrailTesters (YouTube 95k) | Creator | 40k avg views, high-intent gear reviews | Approve — bounty deal | DM + email sent | Onboarded, first click |
```

## Workflow

1. Profile ideal partners by funnel role: reviewers and content sites for research intent,
   comparison/listicle sites, coupon/deal sites for bottom-funnel volume, loyalty/cashback
   publishers, and creators for awareness-to-conversion.
2. Source prospects from five veins: network directories (Awin/Impact/ShareASale/CJ/
   PartnerStack category listings), competitor partner mapping (Ahrefs/Semrush backlink and
   organic gap on competitor review pages), SERP mining of "best {category}" and
   "{brand} review/coupon" queries, creator search (YouTube/TikTok/Instagram in-category),
   and inbound applications.
3. Vet every prospect before outreach: traffic authenticity, audience/market fit, brand
   safety, FTC disclosure practice, geography, and promo methods (brand bidding? toolbar?
   incentivized installs?).
4. Enrich and prioritize: model EPC potential = their traffic × your CR × AOV × commission;
   stack-rank the list and cap weekly outreach volume to protect reply quality.
5. Run 3–4 touch outreach sequences over two weeks, leading with THEIR audience and a
   concrete earnings scenario ("40k monthly readers × our 3.2% CR × $28 EPC"), never with
   your brand story.
6. Negotiate placement deals where justified: flat-fee or CPM for sponsored reviews and
   newsletter slots with proven partners; keep pure-CPA as the default frame.
7. Approve and onboard within 48 hours: acceptance email, quick-start guide (top links, top
   creatives, code rules, brand-bid policy, FTC disclosure requirements), and a first
   campaign suggestion matched to their content.
8. Run activation follow-ups at day 7/14/30 for partners with zero clicks; recycle
   non-responders after one re-contact cycle; log every touch in the CRM.
9. Report weekly on the funnel: sourced, vetted, contacted, approved, activated (first
   click), producing (first sale) — then hand active partners to partner-management.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Network directories | Awin, Impact, ShareASale, CJ, PartnerStack | Filter by category, geography, traffic type |
| Competitor partner mapping | Ahrefs, Semrush (backlink/organic gap) | Paid; reveals who ranks and links for review terms |
| SERP & publisher mining | Google search operators, BuzzSumo | Free tiers; find listicle and coupon pages |
| Creator discovery | YouTube/TikTok search, Modash or HypeAuditor (optional) | Check disclosure habits while vetting |
| Outreach & CRM | Google Sheets + Mailshake/Instantly, HubSpot free CRM | Warm the sending domain; cap daily sends |
| Contact enrichment | Hunter.io, Apollo.io | Free tiers limited; verify deliverability |

## Example AI Prompt

```text
You are an affiliate recruitment specialist. Build a prospect pipeline for {BRAND}
({CATEGORY}, AOV {AOV}, offer {RATE}% CPS, cookie {WINDOW} days, live on {NETWORK/PLATFORM}).

Ideal partners: {PARTNER TYPES + SIZE/GEO}. Do-not-contact list: {EXCLUSIONS}.
Competitor partners to consider: {COMPETITOR REVIEW SITES / PUBLISHERS}.

Deliver:
1. 40–60 qualified prospects across 5 partner types — table: partner | type | audience &
   traffic estimate | fit rationale | vet verdict | suggested approach (CPA vs flat-fee
   placement).
2. A 3-touch email sequence per partner type, leading with their audience and a modeled
   earnings scenario, including FTC-compliant language and our brand-bidding rules.
3. An onboarding kit outline: quick-start steps, top deeplinks, code rules, disclosure
   requirements, and day 7/14/30 activation follow-ups.
```

## Edge Cases & Guardrails

- Never bulk-approve applications: coupon aggregators and incentivized-traffic networks
  inflate approval counts but often deliver cannibalized or fraudulent conversions.
- Set the coupon-site policy before they ask: allowed codes, exclusions, and rate caps —
  otherwise "brand + coupon" SERPs route your own customers through them unpriced.
- Brand-bidding rules go into onboarding, not later — include the SEM exclusion list and
  monitoring consequences in the acceptance email.
- Flag partners whose traffic is 90%+ your brand name: they capture demand rather than
  create it; treat as bottom-funnel with capped rates.
- Recruit for coverage, not volume: two strong review sites per key "best {category}" SERP
  beat 200 dormant signups.
- Run an inactive-partner re-permission cycle regularly; a silently bloating roster of dead
  accounts distorts reporting and platform fees.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Vetting pass rate | 40–70% of sourced prospects | >90% — screening is theater |
| Outreach reply rate | 10–25% cold; 30%+ via warm network intros | <5% after 200 sends |
| Application approval rate (vetted) | >90% | Approving everyone to inflate counts |
| Time to first click | <14 days post-onboard for active partners | Weeks of zero clicks after joining |
| Activation rate (first sale ≤60 days) | 20–40% of onboarded | <10% — onboarding is broken |
| Top-5 partner revenue concentration | <50% | One partner >30–40% of revenue |

## Handoffs

- → **partner-management:** transfer activated partners with segment tags and placement notes.
- → **creative-asset-provision:** request partner-type kits when onboarding reveals gaps.
- ← **tracking-setup:** confirm deeplinks and codes work BEFORE onboarding anyone.
- ← **commission-structure:** negotiate only within approved rate bands; escalate special deals.
- ↑ **affiliate-marketing-agent:** escalate when the offer/EPC is too weak to recruit at
  target volume — terms need repricing, not more outreach.
