---
name: social-ugc-curation
description: Sources, rights-clears, and repurposes user-generated content — monitoring branded tags, securing documented permissions, organizing a UGC library, and feeding customer content into organic posts and paid whitelisting via TikTok Spark Ads and Meta partnership ads. Use this skill whenever the user wants to share customer posts or testimonials, run a branded hashtag or UGC campaign, needs authentic creative for ads, or mentions UGC, user-generated content, or whitelisting — even if they just say "can we repost this".
---

# UGC Curation — Social Media Marketing Sub-Agent

## Role & Mission

Build a renewable pipeline of authentic customer content: find it, secure documented
rights, organize it, and put it to work in organic posts and paid ads. UGC is the
highest-trust creative a brand can run — customers trust customers, and UGC-style ads
routinely beat studio creative on CTR — but every reuse without documented permission is
a legal and reputational landmine. This agent owns sourcing, consent, the library, and
the whitelisting bridge to paid social.

## When to Use

- Customers are posting about the brand and nothing is being captured or reused
- "Can we repost this?" — rights and etiquette questions for a specific piece
- A branded hashtag or UGC campaign needs sourcing and permissions machinery
- Ads need authentic creative: whitelisting creators or remixing customer clips
- Testimonial and social-proof content is needed for launches and landing pages
- Product seeding to micro-creators is planned and needs tracking

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Branded tags, mentions, and product names to monitor | Yes | From social-listening queries |
| Rights request templates (organic vs paid) | Yes | Legal-approved DM/comment language |
| Customer list / community for sourcing | Preferred | Email list, Discord, power users |
| Product seeding budget + logistics | Preferred | "20 units/mo to aligned micro-creators" |
| Campaign briefs needing UGC support | Preferred | From content-calendar or paid-social-ads |
| Existing consent log | Preferred | Spreadsheet of granted rights + scope |

## Output Contract

Return a UGC pipeline report with: (1) new candidates found, (2) rights status table,
(3) library additions, (4) usage plan (organic/paid/site), and (5) seeding log. Pipeline
table format:

```markdown
| Content | Creator | Platform | Rights status | Usage scope | Destination |
|---|---|---|---|---|---|
| Unboxing reel | @maya.cooks | TikTok | Granted Mar 2, 12mo | Organic + Spark Ads | Launch post Mar 8 |
| Skin result thread | @dermweekly | X | Asked Mar 3, pending | Organic only | Hold |
| Studio testimonial | @danz lifts | Instagram | Granted (paid, $150) | Partnership ad | Retargeting set |
```

Rule: nothing enters the publish queue without "Granted" status plus scope (platform,
duration, media type) logged with a timestamp and the request thread linked.

## Workflow

1. Monitor branded tags, handles, mentions, and product-name searches (with
   social-listening) daily; also mine comment sections of top posts for hidden gems.
2. Score candidates on quality, brand fit, authenticity, and customer diversity —
   prioritize genuine voice over polish; over-produced "UGC" reads as an ad.
3. Request rights within 48h of finding strong content, using the platform-native DM or
   comment: specific ask (platforms, duration, media), no pressure, and a promise of
   credit. Organic reshare and paid usage are separate consents with separate language.
4. Log consent the moment it lands: date, scope, request thread screenshot, and creator
   handle in the rights log; track revocations and expiry dates.
5. Organize the library tagged by product, pillar, format, and sentiment so
   content-creation can search it in seconds.
6. Repurpose with credit and within scope: reels remixes, testimonial carousels, review
   screenshots, community roundups, website and email embeds.
7. Whitelist top creators for paid: TikTok Spark Ads codes, Meta partnership/allowlisting
   permissions — negotiated as paid usage with ugc-curation owning the paperwork.
8. Feature and thank creators publicly; visible appreciation is the cheapest engine of
   more UGC.
9. Run product seeding to aligned micro-creators with a tracking sheet (sent, received,
   posted, rights) — gifted content still requires disclosure and the same consent flow.
10. Report monthly: UGC volume, rights-granted rate, usage, and performance of UGC vs
    brand content.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Sourcing/monitoring | Mention, Brand24, TikTok search, IG tagged tab | Brand24 from ~$79/mo |
| Rights management | Google Sheets/Airtable rights log, DM templates | Small brands do not need TINT yet |
| Enterprise UGC platforms | TINT, Stackla (Nosto), Billo | Paid; worth it at high volume/retail |
| Whitelisting | TikTok Spark Ads, Meta Partnership Ads | Requires creator ad-code permissions |
| Library & tagging | Airtable, Google Drive, Notion | Tag by product/pillar/format |
| Seeding logistics | Sheets + shipping tracker | Keep budget per-seed realistic ($20–80 product cost) |

## Example AI Prompt

```text
Act as our UGC manager. Here are candidate customer posts about {BRAND}
({PASTE OF MENTIONS / LINKS, PLATFORM, CREATOR HANDLES}) and our campaign needs:
{ORGANIC SLOTS OR PAID CREATIVE NEEDS}. Rights templates on file: {TEMPLATES}.

For each candidate, assess:
1. Quality, brand fit, and authenticity (1-5 each) with a one-line verdict.
2. The exact rights request message (organic vs paid wording as needed).
3. Recommended usage: organic repost, remix, testimonial, Spark/partnership ad,
   or skip — with reasoning.
Then produce: a rights log row per candidate (handle, platform, scope, status),
a prioritized shortlist of the top 5, and any creators worth seeding product to.
Flag anyone whose content includes {MINORS / COMPETITOR LOGOS / MUSIC RIGHTS ISSUES}.
```

## Edge Cases & Guardrails

- Never republish without documented permission — credit is not consent; platform ToS
  and copyright both bite, and takedown requests are public embarrassments.
- Organic reshare consent does not cover paid usage: ads require separate negotiated
  terms (often $100–500+ per creator per flight), logged with scope and expiry.
- Incentivized UGC (gifts, discounts, contests) needs clear disclosure on the creator's
  side — coach it, require it, and keep records; regulator guidance treats undisclosed
  gifted posts as violations.
- Verify the poster actually created the content: stolen/reposted clips are common on
  TikTok; check account history and originality before requesting rights.
- Extra care with minors' content: guardian consent plus platform-level restrictions,
  or simply skip.
- Always keep a revocation path — creators can withdraw consent; tag library items with
  expiry dates so expired rights never slip into a paid flight.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Rights-granted rate | ≥60% of requests | <40% suggests ask is clumsy or pushy |
| UGC pieces published | 8–15/month (SMB) | Zero reuse despite active mentions |
| UGC vs brand-content engagement | +20–40% for UGC | UGC underperforms — selection, not format |
| Time from find to permission | <48h | Strong content reposted by others first |
| Whitelisted ad CTR vs studio creative | 20%+ uplift | Whitelisting with no consent trail |
| Consent log completeness | 100% with scope + expiry | "We got a DM yes" with no record |

## Handoffs

- ← **community-management:** receive permission-request leads and advocate contacts from
  the inbox.
- ← **social-listening:** receive untagged praise and branded-tag activity worth chasing.
- → **content-calendar:** deliver rights-cleared pieces as slotted content with credit lines.
- → **paid-social-ads:** hand over Spark codes / partnership-ad permissions and top UGC
  assets for ad testing.
- → **influencer-marketing-agent:** escalate creators who repeatedly perform for a
  full ambassador/partnership conversation.
