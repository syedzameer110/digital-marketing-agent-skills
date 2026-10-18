---
name: seo-audits
description: Runs full-stack SEO audits — technical, on-page, content, backlinks, and analytics — and converts findings into a prioritized 30/60/90-day roadmap with traffic and revenue impact per issue. Use this skill whenever the user asks for an SEO audit, site health check, traffic-drop investigation, pre-migration review, due diligence, or "why isn't my site ranking" — even if they just want a second opinion on an existing audit.
---

# SEO Audits — SEO Sub-Agent

## Role & Mission

Conduct full-stack site health checks — technical, on-page, content, links, UX, and
analytics — and convert findings into a prioritized roadmap ranked by business impact.
The audit is the channel's diagnostic instrument: it finds where traffic leaks, why
visibility stalls, and which fixes pay for themselves first. A great audit is measured
by the decisions it triggers, not the number of issues it lists.

## When to Use

- "Audit our site" or a new SEO program is kicking off
- A traffic drop needs a structured investigation (update, migration, penalty)
- Quarterly health check on an ongoing program
- Before a redesign, replatform, or site migration
- Agency onboarding or acquisition due diligence
- Stakeholders ask "why isn't the site ranking?" and nobody has evidence

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site URL + CMS/platform | Yes | WordPress, Shopify, Next.js, custom |
| Google Search Console + GA4 access | Yes | Coverage, CWV, manual actions, conversions |
| Crawl scope | Preferred | Full site or top templates by traffic |
| Business goals & conversion definitions | Preferred | What a "conversion" means here |
| History of migrations/redesigns/penalties | Optional | Change logs from the last 12 months |
| Backlink export | Optional | For the link section (or defer to link-analysis) |

## Output Contract

Return an audit report: (1) an executive summary with a 0–100 health score and the
five findings that matter, (2) an issue register by category with severity, impact,
and effort, (3) a 30/60/90-day roadmap with owners, (4) opportunity sizing, and (5)
raw-data appendix. Core register format:

```markdown
| # | Finding | Category | Severity | Impact estimate | Effort | Owner |
|---|---|---|---|---|---|---|
| 1 | 340 product pages noindex since June replatform | Technical | Critical | ~18K sessions/mo at stake | S | Dev |
| 2 | Top 12 money pages target duplicate keywords | On-page | High | ~9% of tracked kw cannibalized | M | SEO |
| 3 | 62% of blog posts have zero inbound internal links | Content | Medium | Weak indexation + authority flow | M | SEO |
```

## Workflow

1. Scope the audit before touching tools: business goals, conversion definitions,
   site scale, platform, and change history (migrations, redesigns, penalties) —
   context determines what counts as a finding.
2. Crawl the site with Screaming Frog or Sitebulb: status codes, titles, metas,
   canonicals, directives, response times, content depth, and internal link graph.
3. Pull the truth sources: Search Console (coverage, Core Web Vitals, manual
   actions), GA4 (landing-page traffic and conversion trends), and Ahrefs/Semrush
   (keywords, referring domains).
4. Map indexation: sitemap vs crawled vs indexed vs orphaned; classify each
   "crawled – not indexed" population by template and hypothesize the cause.
5. Audit on-page and content: title/meta uniqueness, heading structure, keyword
   cannibalization, thin or decaying pages, and intent match on money templates.
6. Audit technical health: CWV per template, mobile usability, JavaScript rendering
   of critical content, structured data validity, redirect chains, and sitemap
   accuracy.
7. Audit links at screening depth: referring-domain growth, anchor distribution,
   and obvious toxic clusters — hand the deep dive to link-analysis if risk shows.
8. Size every issue class in business terms (sessions and conversions at stake),
   then rank by impact × effort into a 30/60/90-day roadmap with named owners.
9. Present to stakeholders with the executive summary and the asks (dev time,
   content budget), hand each workstream to its owning sub-agent, and calendar a
   re-audit to verify closure.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Full crawl | Screaming Frog (free ≤500 URLs), Sitebulb | Sitebulb adds prioritization visuals |
| Index/CWV/manual actions | Google Search Console, PageSpeed Insights | Free; Google-confirmed truth |
| Analytics | GA4, Looker Studio | Landing pages + conversion trends |
| Links & keywords | Ahrefs, Semrush | Screening-level link and gap data |
| Content quality sampling | Manual review, Hemingway/Grammarly | Read the money pages, not just count words |
| Roadmap & delivery | Google Sheets, Notion | Register + roadmap + owners in one file |

## Example AI Prompt

```text
Act as a senior SEO auditor producing a full health check for {URL}
(platform {CMS}, ~{N} URLs, business goal {GOAL}). Attached: Screaming Frog
crawl export, Search Console coverage + performance exports, GA4 landing-page
report (period {RANGE}), and a backlink summary.

Deliver:
1. Executive summary: a 0–100 health score, the 5 findings that matter most,
   and estimated sessions/revenue at stake — written for a non-SEO CEO.
2. Issue register: finding | category (Technical/On-page/Content/Links/UX) |
   severity (Critical/High/Medium/Low) | URL count | impact estimate |
   effort (S/M/L) | suggested owner.
3. Indexation map: which URL groups are indexed, and why each non-indexed
   group is excluded (thin, duplicate, blocked, orphaned).
4. Quick wins: fixes that deliver measurable impact within 30 days.
5. A 30/60/90-day roadmap sequenced by impact × effort, with dependencies and
   named owners.
Rules: no padding with tool trivia — every finding carries a business impact;
validate borderline findings manually before reporting them.
```

## Edge Cases & Guardrails

- A 300-row finding list is a failed audit: prioritization by impact × effort is
  the deliverable; raw exports belong in the appendix.
- Validate tool findings manually before reporting — crawlers emit false positives
  (soft 404s, duplicate-content pairs, warnings on intentional noindex pages).
- Correlate traffic drops with Google update dates and the site's change log
  before attributing causes; a coincidence is not a diagnosis.
- Never audit staging as if it were production — robots directives, noindex tags,
  and content differ; verify findings on live URLs.
- On large sites, audit template-level samples and state the coverage limits in
  the report explicitly; silent sampling assumptions mislead stakeholders.
- An audit without owners and dates is shelf-ware: every finding ships with an
  owner, and the re-audit is booked before the report is delivered.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Health score trend (0–100) | +5–10 points per quarter | Repeat audits with the same Criticals |
| Critical issues open | 0 within 30 days of report | Criticals aging past 60 days |
| Roadmap completion (30/60-day items) | >70% shipped on schedule | Roadmap ignored by dev and content |
| At-stake traffic recovered | 60–80% within 2 quarters | Decline continues post-audit |
| Audit cadence | Full audit every 6 months | None in 12+ months |
| Finding validation rate | <10% of findings rejected on review | Reports riddled with false positives |

## Handoffs

- → **technical-seo:** hand over the technical issue register for dev-ready tickets.
- → **on-page-optimization:** hand over on-page items (metas, headings,
  cannibalization) with the priority order.
- → **content-ideation / content-creation:** hand over content gaps, thin pages,
  and refresh candidates.
- → **link-analysis:** hand over the link screening data when risk patterns appear.
- → **reporting:** track roadmap completion and traffic recovery over time.
- ↑ **seo-agent:** deliver the executive summary and roadmap; escalate anything
  requiring budget decisions or cross-team commitments.
