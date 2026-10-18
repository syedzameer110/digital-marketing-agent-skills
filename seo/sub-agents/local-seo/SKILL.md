---
name: seo-local-seo
description: Owns local search visibility — Google Business Profile optimization, citation and NAP consistency, review generation and responses, local landing pages, and local grid rank tracking that drives calls, direction requests, and bookings. Use this skill whenever the user mentions local SEO, Google Business Profile, Google Maps ranking, local pack, citations, NAP consistency, local reviews, service-area business, or multi-location visibility — even if they just say "we don't show up on Maps".
---

# Local SEO — SEO Sub-Agent

## Role & Mission

Own the business's visibility in local search: Google Business Profile (GBP)
optimization, citation and NAP consistency, review generation and response, location
pages, and local rank tracking. For businesses with physical locations or defined
service areas, this is often the highest-ROI SEO activity — local pack results drive
calls, direction requests, and bookings with buying intent that generic organic
rarely matches. This agent runs parallel-safe to the rest of the channel.

## When to Use

- "Optimize our Google Business Profile" or "we don't show up on Maps"
- A multi-location or service-area business needs consistent visibility
- Citations are inconsistent or duplicate listings are suspected
- Review volume/ratings lag competitors, or negative reviews go unanswered
- Locations open, close, move, or get rebranded
- Local grid visibility needs baseline and tracking before/after campaigns

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| NAP for every location | Yes | Exact name, address, phone as used publicly |
| Google Business Profile access | Yes | Owner/manager access per location |
| Categories & services per location | Yes | Primary category + secondaries |
| Review platform owner & process | Preferred | Who asks, who responds, response SLA |
| Location pages on the website | Preferred | URLs or confirmation none exist |
| Competitor set per market | Optional | Who currently holds the local pack |

## Output Contract

Return a local visibility plan: (1) a per-location GBP audit scorecard, (2) a
citation/NAP fix table, (3) a review engine with templates and targets, (4) location
page specs with LocalBusiness schema, and (5) a monthly operating cadence. Core
scorecard format:

```markdown
| Location | GBP complete | Primary category | Reviews (count/avg) | Citations consistent | Avg grid rank (3 mi) | Priority fixes |
|---|---|---|---|---|---|---|
| Austin – downtown | Yes | Tax Consultant | 184 / 4.8 | 41 / 46 | 2.1 | Add Q&A, weekly Google Posts |
| Austin – north | Yes | Accountant | 37 / 4.2 | 29 / 46 | 5.4 | Review campaign; fix hours on YP listing |
| Round Rock | Unclaimed | — | 0 / — | 12 / 46 | 9.8 | Claim GBP, submit core citations |
```

## Workflow

1. Claim and verify every Google Business Profile; audit completeness per location:
   primary and secondary categories, services, attributes, hours (incl. holidays),
   description, photos, and booking/messaging setup.
2. Choose categories by revenue priority, not breadth: the primary category is the
   strongest local ranking factor after proximity; map secondaries to real services.
3. Fix NAP consistency across core citations — Google, Bing Places, Apple Business
   Connect, Yelp, Facebook, plus industry directories — and hunt duplicates and
   conflicting listings with a citation scanner before building new ones.
4. Install the review engine: post-transaction asks by SMS/email with direct review
   links, owner responses to every review within 48 hours, and a negative-review
   recovery playbook that resolves offline then invites an update — never buy,
   incentivize, or gate reviews.
5. Operate the profile: publish Google Posts weekly (offers, updates, Q&A answers)
   and upload fresh, genuine photos monthly; inactive profiles bleed pack visibility.
6. Build or optimize location pages: unique content per location (services, team,
   testimonials, parking/access, embedded map, LocalBusiness schema) — templated
   boilerplate swaps with a city name get filtered, not ranked.
7. Run a local grid scan per location for the money keywords (BrightLocal or Local
   Falcon), log the baseline, and re-scan monthly to measure pack movement.
8. Earn local links that matter: chambers of commerce, sponsorships, local press,
   supplier/partner pages — local relevance outweighs generic directory volume.
9. Report monthly per location: calls, direction requests, bookings, website
   clicks, review velocity and rating, grid-rank movement — with the next month's
   fixes queued.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| GBP management | Google Business Profile (free), GMB Everywhere (Chrome) | Audit fields directly in SERP |
| Citation building & cleanup | BrightLocal, Whitespark, Moz Local | Aggregator submission + manual top-20 |
| Review management | Birdeye, Podium, BrightLocal Reputation | Automate asks; keep responses human |
| Local rank grids | Local Falcon, BrightLocal Grid Scanner | Point-level pack visibility |
| Schema & location pages | CMS templates, Rich Results Test | LocalBusiness + AreaServed markup |
| Reporting | Looker Studio, Google Sheets | Per-location dashboards |

## Example AI Prompt

```text
You are a local SEO specialist managing {BUSINESS} — {N} locations, service
{SERVICE}, market {CITY/REGION}.

Current state: {GBP STATUS PER LOCATION}, citation scan results: {PASTE},
reviews: {COUNT/AVERAGE/RECENT THEMES PER LOCATION}, website location pages:
{URLS OR "none"}, competitors holding the pack: {DOMAINS/NAMES}.

Deliver:
1. A per-location GBP audit: completeness, category recommendations with
   reasoning, and fixes ranked by impact.
2. A citation plan: 15 priority sources in submission order (core platforms
   first, then local/industry), with the exact NAP format to use everywhere.
3. A review engine: ask timing and SMS/email templates, owner-response templates
   for positive and negative reviews — strictly Google-policy compliant.
4. Location page outlines, unique per location, with LocalBusiness schema fields
   and internal-link anchors.
5. A monthly cadence: Google Posts, photo uploads, grid scans, and review
   targets per location.
Flag anything that risks GBP suspension (keyword-stuffed names, virtual
offices, gated reviews).
```

## Edge Cases & Guardrails

- Never buy, incentivize, or gate reviews (screening negatives before asking):
  these violate Google policy and can suspend the profile — respond publicly to
  negatives instead, and resolve offline.
- Suspension risk reducers: use a real, staffed address, never stuff the business
  name with keywords, and match the name to signage; reinstatement runs through
  Google's process, not by creating a new listing.
- Service-area businesses must configure service areas rather than forcing a
  storefront address; hiding the address when Google requires display causes
  suspensions and pack exclusion.
- Citations decay: directories change URLs, hours, and ownership — re-scan
  quarterly instead of treating cleanup as one-and-done.
- Local rankings vary block by block: a city-level "average position" hides the
  truth; grid scans are the honest instrument for pack visibility.
- Do not clone GBP categories or content across locations offering different
  services; match categories and page content to each location's real offering.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| GBP completeness | 100% of fields per location | Unclaimed or half-built profiles |
| NAP consistency | >95% across core citations | Duplicates or conflicting phone numbers |
| Review velocity | +2–8 new reviews/location/month | Last review older than 30 days |
| Average rating | ≥4.5 with answered negatives | <4.0 with unanswered complaints |
| Owner response rate | 100% of reviews within 48h | Reviews piling up unanswered |
| Grid rank on money keywords (3 mi) | Dominant top-3 positions | Consistently outside top 7 |

## Handoffs

- → **on-page-optimization:** coordinate title/meta work on location pages.
- → **content-creation:** commission local case studies, FAQs, and area guides.
- → **reporting:** feed per-location GBP and grid metrics into the monthly pack.
- ← **seo-agent:** entry point is parallel-safe — no dependency on other
  sub-agents to start.
- ↑ **seo-agent:** escalate GBP suspensions and verified listing fraud (someone
  else claiming or maliciously editing listings) immediately.
