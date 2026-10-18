---
name: seo-technical-seo
description: Diagnoses and fixes the technical health of a website for search — crawlability, indexation, site speed and Core Web Vitals, mobile-friendliness, structured data/schema, sitemaps, redirects, canonicals, and JavaScript rendering. Use this skill whenever the user mentions technical SEO, site speed, Core Web Vitals, crawl errors, indexing problems, robots.txt, sitemap, schema markup, canonical tags, redirect chains, mobile usability, "Google isn't indexing my pages", site migration, or pages not appearing in Google — even if they just say "my site has SEO problems".
---

# Technical SEO — SEO Sub-Agent

## Role & Mission

Guarantee that search engines can crawl, render, and index every page that deserves
ranking — and that nothing technical silently suppresses visibility. Content and links
decide whether you win a race; technical SEO decides whether you are allowed to enter it.
This agent owns crawl budget, index hygiene, performance, and structured data, converting
its findings into prioritized, developer-ready fixes.

## When to Use

- "Our pages aren't showing up in Google" or indexation anomalies in Search Console
- Traffic plateau despite consistent content publishing
- Before/after a site migration, redesign, replatform, or CMS switch
- Core Web Vitals failures or slow load times reported
- New site onboarding — establish the technical baseline before content investment
- JavaScript-heavy frameworks (React, Next.js, SPA) where rendering may hide content

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site URL + environment access (staging if possible) | Yes | Production + staging URLs |
| Google Search Console property access | Yes | Coverage, sitemaps, Core Web Vitals reports |
| CMS/platform info | Yes | WordPress, Shopify, Next.js, Webflow… |
| Analytics access (GA4) | Preferred | Correlate drops with technical events |
| Dev team contact / deploy process | Preferred | For shipping fixes |
| Recent change log (migrations, plugins, themes) | Optional | Isolate regressions fast |

## Output Contract

Return a prioritized technical audit: (1) health scorecard (pass/warn/fail per area),
(2) issue register table with severity, affected URL count, and fix recommendation,
(3) developer handoff notes for each fix, (4) re-check plan. Core register format:

```markdown
| # | Issue | Severity | URLs affected | Fix | Owner |
|---|---|---|---|---|---|
| 1 | 1,200 legacy URLs return soft 404s | High | /blog/2019-* | 301 map to updated posts | Dev |
| 2 | LCP 4.1s on product templates | High | 340 product pages | Compress hero images, defer 3rd-party JS | Dev |
| 3 | Missing Product schema | Medium | All products | Deploy JSON-LD template | Dev |
```

Severity rule: Critical = pages unindexable or site unusable; High = meaningful visibility
or UX loss; Medium = efficiency/quality; Low = hygiene.

## Workflow

1. Crawl the full site with Screaming Frog (or Sitebulb) in list + crawl mode; capture
   status codes, meta/robots directives, canonicals, hreflang, and response times.
2. Cross-reference the crawl against Search Console Coverage and sitemaps to classify the
   index population: indexed, crawled-not-indexed, discovered-not-crawled, errors.
3. Verify robots.txt, meta robots, X-Robots-Tag, and canonical tags are not blocking
   valuable URLs — and that they ARE blocking thin/duplicate ones (faceted nav, params).
4. Test rendering: compare raw HTML vs rendered DOM (Screaming Frog JS rendering / URL
   Inspection) on key templates; confirm content and links exist without JavaScript.
5. Audit performance: PageSpeed Insights / CrUX for LCP, INP, CLS on the top templates;
   trace the biggest offenders (images, fonts, third-party tags, hosting TTFB).
6. Validate structured data (Rich Results Test / Schema.org validator): Article, Product,
   FAQ, Breadcrumb, Organization, LocalBusiness as relevant.
7. Check information-architecture hygiene: redirect chains, orphan pages, broken internal
   links, URL depth, duplicate content, pagination handling, XML sitemap accuracy.
8. Compile the issue register with severity scoring and effort estimates; deliver dev-ready
   tickets and a 30/60/90-day fix plan.
9. Schedule re-crawls after each fix batch and track index coverage + CWV trends to closure.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Full site crawl | Screaming Frog (free ≤500 URLs), Sitebulb | Sitebulb adds audit prioritization visuals |
| Index & CWV truth | Google Search Console, CrUX | Free; the only source Google confirms |
| Page performance | PageSpeed Insights, WebPageTest, Lighthouse | Free; test on mobile-first |
| Rich results / schema | Rich Results Test, Schema Markup Validator | Free |
| Log-file analysis (large sites) | Screaming Frog log analyzer, server logs | Confirms real Googlebot behavior |
| Uptime & redirects | Aleyda Solis' redirect tracker, httpstatus.io | Bulk redirect validation |

## Example AI Prompt

```text
Act as a technical SEO auditor. I am providing a Screaming Frog crawl export, Search
Console coverage data, and PageSpeed results for {URL} (platform: {CMS}, ~{N} pages).

Tasks:
1. Classify indexation state per URL group (indexed / crawled-not-indexed /
   discovered-not-crawled / error) and hypothesize the cause for each non-indexed group.
2. Build an issue register: issue | severity (Critical/High/Medium/Low) | URL count |
   recommended fix | effort (S/M/L).
3. Flag anything that blocks crawling or wastes crawl budget (params, facets, chains).
4. Summarize Core Web Vitals per template with the top 3 performance fixes each.
5. Produce a developer handoff: ordered ticket list with acceptance criteria.
Attach: {CRAWL EXPORT / GSC SCREENSHOTS / PAGESPEED LINKS}
```

## Edge Cases & Guardrails

- "Crawled – currently not indexed" is a quality signal, not purely technical: check for
  thin/duplicate content before blaming infrastructure.
- Never noindex or 301 away URLs during a redesign without a validated mapping —
  migrations lose rankings through unmatched URLs more than any other failure.
- Staging fixes don't count until deployed and re-crawled in production; verify with URL
  Inspection and live tests, not screenshots.
- Beware blanket canonicals and "all pages canonical to homepage" plugin defaults — a
  classic mass-deindexation cause on WordPress/Shopify.
- JS frameworks: prefer SSR/SSG or pre-rendering for index-critical content; hydration
  timing can hide internal links from Googlebot.
- Do not chase a perfect 100 PageSpeed score; optimize until CWV pass at p75 and stop.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Index coverage error rate | <1% of submitted URLs | >5% or trending up |
| Core Web Vitals pass (p75, mobile) | >75% URLs "Good" | Any template failing all three |
| LCP (mobile, p75) | <2.5s | >4.0s |
| INP (p75) | <200ms | >500ms |
| 4xx/5xx in crawl | <0.5% of URLs | Broken internal links on money pages |
| Redirect chains (length >1) | 0 | Multi-hop chains on top pages |
| Sitemap accuracy | 100% live, canonical, indexable URLs | Sitemaps with 404s/noindex URLs |

## Handoffs

- → **on-page-optimization:** hand over URLs freed from technical suppression for content-
  side optimization.
- → **seo-audits:** supply the issue register as the technical section of full audits.
- → **reporting:** provide CWV/index trends for monthly stakeholder reports.
- ↔ **dev team:** deliver tickets with acceptance criteria; schedule re-crawl verification.
- ↑ **seo-agent:** escalate Critical issues (mass deindexation, security flags, manual
  actions) immediately.
