---
name: influencer-marketing-agent
description: Runs influencer and creator marketing end to end — discovering creators, vetting audiences for authenticity, briefing campaigns, negotiating rates and usage rights, co-creating content, managing timelines, measuring CPE and attributed sales, and building ambassador programs. Use this skill whenever the user mentions influencer campaigns, creators, TikTok/Instagram/YouTube partnerships, UGC creators, brand ambassadors, influencer rates, sponsored posts, whitelisting, or Spark Ads — even if they never say "influencer marketing" explicitly.
---

# Influencer Marketing — Main Agent (Command Hub)

## Channel Overview

Influencer marketing is a trust-based channel: the brand borrows credibility a creator has
already earned with a specific audience. It wins where paid ads underperform — product
launches that need social proof, DTC and e-commerce categories driven by lifestyle
aspiration, app installs, and audiences (Gen Z, niche hobbyists, B2B practitioners) who
skip or distrust traditional advertising. The trade-offs are uneven scale (you buy reach
one human at a time), measurement friction (attribution runs on codes, links, and
whitelisted ads rather than clean platform pixels), and creator risk — one bad actor can
become a brand-safety incident.

Work in creator tiers, because economics and expectations differ sharply per tier:

| Tier | Followers | Typical IG engagement | Typical cost per post |
|---|---|---|---|
| Nano | 1–10K | 4–8% | Product-only to $100 |
| Micro | 10–100K | 2–5% | $100–$1,000 (heuristic: $100–$300 per 10K IG followers) |
| Mid | 100K–1M | 1–3% | $1,000–$10,000 |
| Macro / celebrity | 1M+ | 1–2% | $10,000–$250,000+ |

TikTok and YouTube price differently: TikTok rates per follower are usually lower than
Instagram ($25–$125 per 10K followers) and sophisticated creators price off expected views;
YouTube integrations run roughly $50–$100 CPM against forecast views, or $2,000–$50,000+
per dedicated video. Nano and micro creators deliver the highest engagement rates and the
cheapest cost per engagement; macro buys reach moments and prestige, not efficiency.

Platform choice matters as much as tier. Instagram Reels and TikTok dominate short-form
reach and whitelisting efficiency; YouTube long-form carries the deepest integration trust
and the longest content shelf life — a good integration keeps pulling views for years.
Most programs run two platforms well rather than four thinly, and each platform carries
its own measurement nuances: story metrics are perishable (24-hour expiry), short-form
engagement is better judged against views than followers, and YouTube conversions often
surface days later as branded search.

Time-to-results is realistic but front-loaded: a contracted creator typically goes live
1–3 weeks after signing; sales lift is measurable during a 2–4 week flight; always-on
programs compound over 3–6 months; ambassador programs pay back over 6–12 months. Program
costs for a serious test run $5,000–$20,000/month (mostly creator fees plus product);
always-on DTC programs commonly run $25,000–$100,000+/month across 20–100 active creators.

## Agent Hierarchy

```text
influencer-marketing-agent (command hub)
└── sub-agents/
    ├── influencer-research/       → find creators in the niche, tiered longlists
    ├── vetting/                   → engagement authenticity, fake followers, brand fit
    ├── campaign-briefing/         → deliverables, creative guidelines, disclosure rules
    ├── negotiation/               → rates, contracts, usage rights, whitelisting terms
    ├── content-collaboration/     → co-creation, draft approvals, revision control
    ├── campaign-management/       → master calendar, go-live checks, quality oversight
    ├── tracking-measurement/      → reach, engagement, CPE, EMV, sales attribution
    └── relationship-building/     → long-term ambassador and repeat-partner programs
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| influencer-research | Starting a program, entering a new niche/platform, or refreshing the creator pipeline | ICP/persona, platform mix, tier strategy, budget | None (entry point) |
| vetting | Any creator is shortlisted before outreach; quarterly roster re-checks | Creator handles, platform URLs, prior content | influencer-research |
| campaign-briefing | Creators are signed (or shortlist is approved) and need deliverable specs | Campaign goal, product info, brand guidelines, messaging | vetting |
| negotiation | A vetted creator replies to outreach or rates are requested | Rate benchmarks, deliverables list, usage-rights needs | campaign-briefing |
| content-collaboration | Contracts are signed and drafts start arriving (or co-creation is planned) | Signed brief, contract terms, approval SLA | negotiation, campaign-briefing |
| campaign-management | Multiple creators are live or going live inside a flight window | Master calendar, signed deliverables, tracking checklist | content-collaboration |
| tracking-measurement | Campaign flight starts (live tracking) and within 7 days of flight end (report) | UTM/code/affiliate setup, spend log, platform analytics | campaign-management |
| relationship-building | A flight closes with performance data, or top performers repeat-buy attention | Post-flight report, creator performance tiers | tracking-measurement |

## End-to-End Workflows

### Workflow A — First Influencer Campaign Launch (weeks 1–8)

1. Run **influencer-research** to build a tiered longlist (30–60 creators) matched to the
   ICP, platform mix, and budget. Output: longlist + 10–20 shortlist with estimated rates.
2. Run **vetting** on every shortlisted creator: audience authenticity, engagement
   quality, brand safety. Output: Pass/Watch/Reject scorecard (expect to cut 20–40%).
3. Run **campaign-briefing** for the confirmed roster: deliverables table, mandatory
   messages (max 2–3), disclosure requirements, approval SLA. Output: one brief per creator.
4. Run **negotiation** creator by creator: rate benchmarks, bundled deliverables, usage
   rights and whitelisting terms, payment schedule. Output: signed contracts.
5. Run **content-collaboration**: receive drafts within 5 days of contract, approve in
   2–3 business days, cap revisions at 2 rounds. Output: approved, scheduled content.
6. Run **campaign-management** through the flight: master calendar, go-live checklist per
   post (link, code, disclosure, tracking), escalations. Output: 95%+ on-time delivery.
7. Run **tracking-measurement** from day one: capture story metrics within 48 hours, log
   spend, reconcile codes/links, deliver the post-flight report within 7 days. Output:
   CPE, EMV, attributed revenue by creator.

### Workflow B — Always-On Ambassador Engine (quarterly cycle, recurring)

1. Pull the **tracking-measurement** performance archive and feed the top 10–20% of
   creators into **relationship-building** as ambassador candidates.
2. Run **relationship-building** to structure tiers (product-only, paid retainer,
   revenue-share) and negotiate multi-month terms via **negotiation** with exclusivity.
3. Refresh the pipeline: **influencer-research** + **vetting** to replace churned creators
   and expand into adjacent niches (target: 30–50% of roster as repeat partners).
4. **campaign-briefing** issues lighter "evergreen" briefs; **content-collaboration**
   approves monthly content batches in bulk.
5. **campaign-management** runs the always-on calendar; **tracking-measurement** reports
   monthly by creator and by ambassador tier.
6. Quarterly **negotiation** refreshes ambassador rate cards against market benchmarks,
   promoting or sunsetting tier placements on the tracking archive's evidence.

### Workflow C — Product Launch Amplification Sprint (2–4 weeks)

1. **campaign-briefing** drafts a launch-specific brief (single hero message, launch-date
   embargo, unboxing-first formats).
2. **negotiation** fast-tracks existing vetted creators from the roster using pre-agreed
   rate cards; new creators only via express vetting.
3. **content-collaboration** runs a compressed 48-hour approval loop with one revision
   round max.
4. **campaign-management** orchestrates a staggered posting wave (nano/micro first for
   social proof, mid/macro for reach on launch day) and boosts top organic performers as
   Spark Ads / whitelisted paid social within 48 hours.
5. **tracking-measurement** reports daily during the flight and closes with a launch
   wrap-up: CPE by tier, code redemptions, earned media value, whitelisted-ad results
   handed to paid social.
6. Close with **relationship-building**: convert launch standouts into ambassador
   conversations while goodwill and performance evidence are fresh.

## KPI Dashboard

North-star metric: **campaign-attributed revenue via creator codes/links at target cost
per engagement (CPE)** — engagement proves the audience cared; attributed revenue proves
the trust converted.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Cost per engagement (CPE) | Spend log ÷ platform analytics | Per flight | $0.10–$0.50 social (micro-led); $0.05–$0.20 nano-heavy |
| Engagement rate by tier | Modash / platform analytics | Per flight | Micro 1–5%, mid/macro 1–3%, nano 4–8% |
| Coded/linked attributed sales | Affiliate platform + GA4 | Weekly in flight | ROAS 2–4x on coded campaigns |
| Earned media value (EMV) | Impressions × $5–$10 CPM benchmark | Per flight | EMV ≥ 2x creator fees |
| Deliverable on-time rate | Campaign calendar (GRIN/Aspire) | Weekly | ≥95% |
| Content approval cycle | Approval log | Per draft | ≤2 rounds, ≤3 business days |
| Whitelisted/Spark Ads CTR | TikTok Ads / Meta Ads Manager | Per flight | 0.8–1.5% |
| Repeat-partner share of roster | Creator CRM | Quarterly | 30–50% |
| Follower growth during active flights | Platform analytics | Monthly | +1–3% MoM attributable lift |
| Creator asset reuse across channels | UGC library log | Monthly | ≥30% of assets reused |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $1,000–$5,000 | 70% nano/micro fees (8–15 creators), 20% product/sampling/shipping, 10% tooling; affiliate incentives instead of big fees |
| $5,000–$20,000 | 60% micro/mid fees, 15% paid amplification (Spark Ads/whitelisting), 15% product/seeding, 10% tooling (Modash/GRIN tier) |
| $20,000–$50,000 | 55% mixed-tier fees, 20% paid amplification + usage rights, 15% ambassador retainers, 10% tooling/measurement |
| $50,000+ | 50% creator fees incl. macro moments, 20% always-on ambassador program, 15% amplification/usage, 15% platform (CreatorIQ/GRIN), team or agency |

Allocation principles:

- Creator fees are the media budget — keep 60–70% in fees, cap tooling at 10–15%.
- Buy usage rights (organic + paid, 6–12 months) at contract time; retrofitting later
  costs 30–100% premiums and delays whitelisting wins.
- Never commit more than 30% of a flight budget to one creator, however impressive.
- Weight the roster nano/micro-heavy (better CPE, more authentic voice); reserve macro
  for launch reach moments only.
- Fund product and seeding honestly: free product, shipping, and customs are real media
  costs — nano/gifting programs live or die on this line.
- Hold 5–10% as an in-flight amplification reserve to boost overperformers within 48
  hours instead of waiting for next quarter's budget.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy, tier mix, budget | In-house (channel owner) | Tied to business goals and margin math |
| Creator research & vetting | In-house with tooling (Modash/HypeAuditor), or agency at scale | Database skills are trainable; volume justifies agency only above ~50 creators/quarter |
| Contracts & usage rights | In-house + legal review of templates | Negotiation is relationship work; legal signs off on template clauses |
| Content approvals | In-house (brand + product owners) | Authenticity dies in agency telephone; keep feedback direct |
| Always-on ambassador ops | Fractional creator manager or agency (GRIN/Aspire admins) | High-touch routine work; scales externally |
| Measurement & reporting | In-house (analytics owner) | Attribution logic must match finance and other channels |
| Contract legal review | In-house counsel (as needed) | Usage rights, exclusivity, and FTC clauses carry legal exposure |

## Reporting Cadence

- **Weekly (in-flight, 30 min):** posts live vs calendar, early engagement, issues/escalations,
  boost candidates. Decision: reallocate boosts, chase late deliverables.
- **Monthly (stakeholders, 1 hr):** CPE and ER by tier, coded sales/ROAS, EMV, roster
  health (on-time rate, approvals), next-month creator slate. Decision: renew/replace creators.
- **Quarterly (leadership):** program ROI vs other channels, ambassador tier performance,
  rate-card benchmarks, whitelisting learnings for paid social. Decision: tier strategy,
  budget shift, exclusivity/ambassador upgrades.
- **Ad hoc (within 48 hours):** brand-safety events or viral posts — decision: boost,
  pause, respond, or pull, with a written call from the channel owner.

## Cross-Channel Integrations

- **→ social-media-marketing-agent:** deliver whitelisted/Spark Ads variants of winning
  creator posts and rights-cleared UGC for the organic calendar; receive platform trend
  and hashtag intel that feeds creator briefs.
- **→ affiliate-marketing-agent:** issue unique codes and tracking links per creator; run
  hybrid affiliate-influencer deals (commission + fee); reconcile attributed sales monthly.
- **→ content-marketing-agent:** hand over long-form creator content (YouTube integrations,
  blog-style collabs) and testimonial assets for the editorial calendar and email newsletter.
- **→ web-analytics-agent:** enforce UTM conventions and GA4 landing-page goals for every
  creator link; web-analytics reconciles traffic/revenue vs code redemptions.
- **← email-marketing-agent:** creator content and quotes embed in lifecycle campaigns;
  email announces ambassador programs to the customer base.
- **← cro:** creator-style UGC and hook formats feed landing-page video/social-proof tests.
- **→ video-marketing-agent:** long-form YouTube creator integrations and raw creator
  footage feed the video content library; production specs stay consistent across both.
