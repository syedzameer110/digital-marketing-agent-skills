---
name: seo-backlink-building
description: Plans and executes link acquisition — prospecting, personalized outreach, guest posting, digital PR, and linkable-asset promotion — to grow domain authority with quality links that survive algorithm updates. Use this skill whenever the user mentions backlinks, link building, guest posts, outreach, digital PR, "we need more referring domains", DR/authority gaps vs competitors, or promoting a new study or tool — even if they just ask "how do we get links".
---

# Backlink Building — SEO Sub-Agent

## Role & Mission

Grow the site's authority through earned links: prospecting, personalized outreach,
guest posting, and digital PR. This agent owns link velocity and quality — a steady
stream of relevant referring domains that moves rankings without ever tripping spam
filters. It consumes linkable assets from content-creation and link gaps from
competitor-analysis, and turns them into placements tracked end-to-end.

## When to Use

- "We need backlinks" or Domain Rating lags the competitors winning the SERP
- A strong content asset is live and needs promotion while it is fresh
- Competitor backlink gaps are identified and ready to exploit
- A link campaign month or quarter needs planning and targets
- Recovery from a thin or low-quality link profile is underway
- Stakeholders ask why rankings plateau despite good content

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Linkable assets to promote | Yes | Studies, tools, guides from content-creation |
| Prospect criteria | Yes | DR floor ≥30, real traffic, topical relevance |
| Competitor backlink gap export | Preferred | Ahrefs/Semrush link intersect from competitor-analysis |
| Outreach infrastructure | Yes | Dedicated domain/inbox, SPF/DKIM/DMARC set |
| Positioning & PR angles | Preferred | Unique data, contrarian POV, expert quotes |
| Monthly target (net-new RDs) | Preferred | Agreed with seo-agent and reporting |

## Output Contract

Return a campaign tracker: (1) strategy summary with monthly link targets, (2) a
qualified prospect table, (3) an outreach pipeline with status per prospect, (4) a
placed-links register with metrics and live URLs, (5) follow-up cadence and rejection
taxonomy. Core format:

```markdown
| Prospect | DR | Traffic | Link type | Asset pitched | Status | Placed URL |
|---|---|---|---|---|---|---|
| hrweekly.com | 54 | 82K/mo | Guest post | Payroll automation guide | Replied — negotiating angle | — |
| hrtechdaily.io | 61 | 45K/mo | Resource link | 2025 Salary Benchmarks report | Placed (followed) | /resources/benchmarks |
| peopleopsforum.com | 38 | 210K/mo | Broken link | Onboarding checklist template | Sent — follow-up day 4 | — |
```

## Workflow

1. Set the target with seo-agent: net-new referring domains per month, sized from
   the authority gap versus the competitors that currently win the SERP.
2. Audit the asset shelf and pick 1–3 hero assets (original data, free tools,
   definitive guides, templates); if none qualify, commission one before outreach
   starts — weak assets waste every email that follows.
3. Prospect at 3–10× the target volume: competitor link intersect, resource pages,
   broken-link mining, unlinked brand mentions, and journalist request platforms.
4. Qualify every prospect manually: topical relevance first, then DR/traffic floors,
   real organic traffic (not PBN zeros), and outbound-link hygiene on the target page.
5. Personalize each email: reference their specific recent content, state the exact
   value for their readers, and make one clear ask — under 120 words, subject line
   under 6 words, no flattery templates.
6. Run follow-ups on a fixed cadence (day 0 / 4 / 9), then close the thread; log
   replies, rejections, and rejection reasons for pattern learning.
7. Execute parallel plays: guest posts only on genuinely edited, relevant
   publications; digital-PR pitches (new data, seasonal studies) to journalists on
   request platforms and direct.
8. Verify every placement: link live and followed (or intentionally nofollowed),
   anchor appropriate, page indexed — then add it to the placements register with
   date and DR.
9. Report monthly to reporting: links placed vs target, velocity, DR trend, and
   ranking movement of linked pages; hand the new-link list to link-analysis for
   hygiene logging.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Prospecting & authority metrics | Ahrefs, Semrush, Majestic | Link intersect + referring-domain data |
| Outreach at scale | Pitchbox, BuzzStream, Respona | CRM-style pipeline, follow-up automation |
| Journalist requests | Connectively (ex-HARO), Qwoted, Featured | Free/cheap; fast editorial wins |
| Email deliverability | Google Workspace, NeverBounce, warmup tools | Verify every address; warm new inboxes |
| Pipeline & tracking | Google Sheets, Airtable, Notion | Sheets suffices under ~100 prospects/mo |
| Placement verification | Ahrefs backlinks report, manual SERP checks | Confirm live, followed, indexed |

## Example AI Prompt

```text
You are a link-building strategist for {BUSINESS} ({URL}), niche {NICHE},
current DR {DR}. The competitors outranking us: {COMPETITOR DOMAINS + THEIR DR}.

Assets available to promote: {LINKABLE ASSETS + URLS}
Prospect criteria: DR ≥{FLOOR}, organic traffic ≥{MIN}, relevance rule {RULES}
Outreach email that underperformed last quarter: {PASTE EMAIL}

Deliver:
1. A 3-pronged campaign plan (guest posts, digital PR/data story, resource and
   broken links) with expected placements per prong per month.
2. 25 qualified prospects in a table: site | DR | traffic | link type | a
   personalized angle referencing their actual content (no generic flattery).
3. Two outreach email variants (≤120 words, subject ≤6 words) tuned to the
   strongest asset.
4. A follow-up cadence (day 0/4/9) and a rejection-reason taxonomy for tracking.
Never propose paid links, link farms, PBNs, link exchanges, or comment spam.
```

## Edge Cases & Guardrails

- Never buy links from networks or spam schemes: Google's link-spam policies can
  nullify or penalize paid signals, and recovery costs far exceed any shortcut.
- Relevance beats authority: a DR 35 niche publication moves rankings more than a
  DR 80 irrelevant one; filter on topic first, metrics second.
- Keep anchor distribution natural: brand and URL anchors dominant (≥60%), partial
  matches sparingly, exact-match anchors under ~10% of the profile.
- Protect deliverability: warm up new sending domains, authenticate SPF/DKIM/DMARC,
  cap cold volume around 50/day per inbox, and verify addresses before sending.
- Avoid "write for us" farms: if a site publishes anything for anyone and its guest
  posts sit unindexed, the link is near-worthless.
- Reclaim passively: unlinked mentions and dead placements erode gains monthly —
  monitor and convert or restore them.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Net-new referring domains / month | +5–15 (SMB), +15–40 (mid-market) | Zero for 2+ consecutive months |
| Outreach reply rate | 5–15% | <2% — deliverability or targeting failure |
| Reply-to-placement conversion | 15–30% | <5% — wrong ask or weak asset |
| Topical relevance of placements | >80% niche-relevant sites | Mostly unrelated directories |
| Effective cost per placed link | $100–$500 (outreach); ~$0 earned/PR | >$1,000 with no ranking movement |
| Exact-match anchor share of new links | <10% | Exact-match clusters forming |

## Handoffs

- ← **content-creation:** receives live linkable assets — promote within days of
  publish while the content is fresh.
- ← **competitor-analysis:** receives the link-gap list and replicable source types.
- → **link-analysis:** hand over every placed link for hygiene logging and anchor
  distribution monitoring.
- → **reporting:** monthly velocity, placements, and DR/ranking movement.
- ↑ **seo-agent:** escalate when the authority gap requires a digital-PR investment
  decision or when prospect supply runs dry in the niche.
