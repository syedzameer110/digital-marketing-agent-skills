---
name: influencer-influencer-research
description: Finds and shortlists creators in any niche across TikTok, Instagram, and YouTube — database searches, hashtag and sound mining, competitor tag audits, and tier-balanced longlists (nano 1–10K, micro 10–100K, mid 100K–1M, macro 1M+) with engagement-rate pre-screens and estimated rates. Use this skill whenever the user needs to find influencers, discover creators, build an influencer list, source UGC creators, or asks "who should we partner with" — even if they just say "we need influencers" with no further detail.
---

# Influencer Research — Influencer Marketing Sub-Agent

## Role & Mission

Own the top of the creator funnel: turn a blank slate ("we need influencers") into a
tiered, evidence-based shortlist of creators whose audiences actually match the buyer.
Every downstream dollar — fees, product, amplification — is spent against this list, so
precision here compounds everywhere else. The mission is decision-quality shortlists, not
impressive spreadsheet length: 30 weak creators waste vetting capacity; the right 15
convert into a performing roster.

## When to Use

- "Find us influencers in {niche}" or launching a creator program from zero
- Entering a new platform (adding TikTok to an IG roster, or YouTube long-form)
- Refreshing or expanding the pipeline before a new campaign flight or quarter
- A competitor runs visible creator campaigns and needs mapping of who they work with
- Needing nano/UGC creators for seeding vs macro creators for a launch moment
- Existing roster churned and the next flight needs replacements fast

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| ICP / audience persona | Yes | "Women 22–35, US, interested in pilates + wellness" |
| Platform priority & tier mix | Yes | "TikTok + IG Reels; 70% nano/micro, 30% mid" |
| Campaign goal & budget band | Yes | "Launch awareness, $15K fees for the flight" |
| Target geography & language | Yes | US/EN or DACH/DE |
| Competitor handles / brands to mine | Optional | 3–5 brands running creator campaigns |
| Existing roster / do-not-contact list | Optional | Creator CRM export (GRIN/Aspire) |

## Output Contract

Return: (1) 5-line opportunity summary, (2) tiered shortlist table (the core artifact),
(3) pipeline stats (longlist size, screen-out reasons), (4) per-creator estimated rate
band, (5) exclusions with reasons. Core table format:

```markdown
| Creator | Platform | Handle | Tier | Followers | Avg ER | Avg views/post | Niche fit | Est. rate | Note |
|---|---|---|---|---|---|---|---|---|---|
| Maya R. | Instagram | @maya.moves | Micro | 48K | 3.8% | — | Pilates, exactly ICP | $500–$900 | Tagged by 2 competitors |
| Dev K. | TikTok | @devbuilds | Nano | 8.2K | 7.1% | 14K | Budget gear reviews | Product + $80 | High comment quality |
| Lena S. | YouTube | @LenaSpaces | Mid | 310K | 2.4% | 60K | Home office setups | $3,000–$5,000 | Strong affiliate history |
```

Rate bands use the IG heuristic ($100–$300 per 10K followers) adjusted for platform:
TikTok typically $25–$125 per 10K followers; YouTube priced off expected views
(~$50–$100 CPM on forecast views for integrations).

## Workflow

1. Confirm the ICP, platform mix, tier strategy, geography, and budget with the requester —
   creator value is meaningless without an audience and conversion context.
2. Translate the ICP into searchable criteria: category keywords, follower bands per tier,
   geo/language filters, and audience-demographic thresholds to filter on later.
3. Harvest discovery seeds: niche hashtags and TikTok sounds, competitor branded-content
   tags and tagged-follower lists, platform-native search (TikTok Creative Center,
   YouTube search filters), and names mentioned by the existing roster.
4. Pull database results (Modash / Upfluence / Aspire) with the criteria from step 2;
   export 60–150 candidates with follower count, ER, audience geo/age/gender splits.
5. Pre-screen mechanically: drop creators whose ER sits far outside their tier band
   (nano 4–8%, micro 2–5%, mid 1–3%, macro 1–2%) or whose audience geo match is <60%.
6. Manually review the last 9 posts of each survivor: hook quality, caption craft,
   comment tone (real conversations vs emoji walls), sponsored-content history.
7. Check every candidate against the existing roster and do-not-contact list; dedupe.
8. Assemble the tiered shortlist (15–30 creators) with niche-fit rationale and estimated
   rate bands; balance tiers per the strategy (do not drift 100% mid-tier because they
   are easiest to find).
9. Deliver the shortlist plus pipeline stats to vetting for authenticity and brand-safety
   scoring before any outreach.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Creator database search | Modash, Upfluence | Modash: 200M+ profiles, strong filters; Upfluence adds e-comm audience matching |
| Roster + campaign CRM discovery | GRIN, Aspire, CreatorIQ | GRIN/Aspire for DTC; CreatorIQ for enterprise multi-brand |
| Authenticity pre-screen | HypeAuditor | Audience-quality scores before deeper vetting |
| Native platform discovery | TikTok Creator Marketplace, YouTube search/Studio filters | Free; view real content and comment culture |
| Manual mining | Hashtag/sound search, competitor tagged posts, Spark Ads transparency | Free; finds creators databases index late |
| Longlist workspace | Google Sheets / Airtable | Shared pipeline with status columns |

## Example AI Prompt

```text
You are an influencer research specialist. Build a tiered creator shortlist for {BRAND},
a {PRODUCT/CATEGORY} business targeting {ICP — age, gender, geo, interests}.

Platform mix: {PLATFORMS + PRIORITY}. Tier strategy: {TIER MIX e.g. 70% nano/micro,
30% mid}. Flight budget for fees: {BUDGET}. Language/market: {LANGUAGE/GEO}.
Competitors whose creator rosters we should mine: {COMPETITOR HANDLES}.
Already working with / blacklisted: {EXISTING ROSTER}.

Deliver:
1. A 60–150 creator longlist summary with screen-out reasons.
2. A 15–30 creator shortlist table: creator | platform | handle | tier | followers |
   avg ER | avg views | niche fit | estimated rate band | why shortlisted.
3. Rate bands per the $100–$300 per 10K IG followers heuristic, adjusted for TikTok/YouTube.
4. Tier-balance check against our strategy, with recommendations if the market skews.
Flag any creator whose engagement rate is far off their tier band before shortlisting.
```

## Edge Cases & Guardrails

- Database metrics lag reality: a creator who went viral last month shows stale ER —
  always verify against the live profile before shortlisting.
- ER without context is a trap: pods and giveaway-inflated accounts post 6–10% ER with
  dead comments; note comment quality alongside rate in the shortlist.
- Do not equate follower count with audience: a 20K creator with 90% target-market
  audience outperforms a 300K generalist; keep audience-overlap data in the table.
- Mega-lists stall campaigns: more than ~30 shortlisted creators bloat vetting; cut by
  tier-balance and niche fit, not alphabetically.
- Respect platform rate norms — applying Instagram pricing to YouTube integrations
  loses credibility with creators and agents.
- Never contact creators before vetting clears them; early outreach to a rejected creator
  burns the relationship and the channel's reputation.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Longlist-to-shortlist conversion | 20–35% | <10% (search too loose) or >50% (screening too shallow) |
| Shortlist passing vetting | ≥60% | <40% means research quality is poor |
| Shortlist audience-geo match | ≥70% in target market | <50% — reach exists but buyers do not |
| Tier balance vs strategy | Within ±10% of planned mix | 100% one tier by convenience |
| Time to deliver shortlist | ≤5 business days | >2 weeks stalls the whole flight |
| Duplicate/roster collisions | 0 | Repeat outreach to existing partners |

## Handoffs

- → **vetting:** deliver the shortlist with follower, ER, and audience data for
  authenticity and brand-safety scoring — no outreach before the verdict.
- → **negotiation (via main agent):** pass estimated rate bands as opening-benchmark inputs.
- → **campaign-briefing:** supply niche-fit notes that shape creative angles per creator.
- ↑ **influencer-marketing-agent:** escalate if the niche cannot fill the tier mix within
  budget — the strategy or channel needs revisiting before spend.
- ↔ **social-media-marketing-agent:** pull trending sounds, formats, and hashtags as
  discovery seeds for TikTok/Reels research.
