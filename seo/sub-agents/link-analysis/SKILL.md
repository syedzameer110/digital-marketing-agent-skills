---
name: seo-link-analysis
description: Audits the backlink profile for quality, risk, and opportunity — anchor text distribution, toxic pattern detection, disavow decisions, and competitor link benchmarking. Use this skill whenever the user mentions a backlink audit, toxic links, disavow file, unnatural links, manual actions, negative SEO, anchor text analysis, link profile health, or a ranking drop that needs link-based causes ruled out — even if they just ask "are our backlinks safe".
---

# Link Analysis — SEO Sub-Agent

## Role & Mission

Audit the backlink profile for quality, risk, and opportunity — and protect the site
from link-based penalties while finding exploitable gaps. This agent owns anchor-text
distribution, toxic-pattern detection, disavow decisions (made sparingly), and
profile benchmarking versus competitors. Since Penguin 4.0, Google mostly ignores bad
links rather than penalizing them — so the modern mission is precision: flag real
manipulation, ignore noise, and never discard value through over-disavowing.

## When to Use

- "Audit our backlinks" or a link-profile health check is due
- A ranking drop needs link-based causes ruled out (or confirmed)
- Manual action or "unnatural links" notice appears in Search Console
- A sudden backlink spike suggests negative SEO or a PBN attack
- Quarterly link hygiene after ongoing backlink-building campaigns
- A competitor comparison of link profiles is needed for strategy

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Full backlink export | Yes | Ahrefs or Semrush (all referring domains) |
| Anchor text data | Yes | Ahrefs/Semrush anchors report |
| Google Search Console links report | Preferred | What Google actually counts |
| Campaign log of intentionally built links | Preferred | From backlink-building register |
| Manual action / penalty history | Optional | Search Console notifications |
| Competitor backlink exports | Optional | 2–3 rivals for benchmarking |

## Output Contract

Return a link audit containing: (1) a profile health scorecard (growth, mix,
distribution), (2) anchor text distribution summary, (3) a flagged-domains verdict
table, (4) a disavow file with justification if — and only if — warranted, and (5)
opportunity gaps vs competitors. Core verdict table:

```markdown
| Domain | DR | Pattern | First seen | Verdict | Action |
|---|---|---|---|---|---|
| seo-boost-network.net | 4 | Sitewide footer, PBN interlinking, off-topic | 2025-03-11 | Toxic | Disavow (domain) |
| hrinsider.com | 52 | Editorial guest post, brand anchor | 2025-06-02 | Healthy | Monitor |
| old-vendor-directory.com | 12 | Stale directory listing, no traffic | 2021-08-19 | Low value | Ignore — Google discounts it |
```

## Workflow

1. Pull the complete profile from Ahrefs or Semrush and reconcile it against the
   Google Search Console links report; GSC is the smaller but authoritative set.
2. Baseline the profile: referring-domain count and growth curve, DR distribution,
   follow/nofollow mix, TLD and geography spread, and first-seen velocity.
3. Map anchor text distribution into brand, URL, generic, partial-match, and
   exact-match buckets; flag exact-match clusters above ~10% of anchors.
4. Screen for risk patterns: overnight velocity spikes, sitewide footers, PBN
   signatures (thin sites interlinking each other), foreign-language spam, and
   links from hacked pages.
5. Separate intentional links from everything else using the backlink-building
   campaign register — never mislabel real placements as toxic.
6. Manually sample every flagged domain before acting: open the pages, check
   indexation (site: search), traffic, and context — automated toxicity scores are
   heuristics, not verdicts.
7. Classify and act: Toxic → disavow (domain: lines) with a written rationale per
   entry; Suspicious → monitor next quarter; Low-value → ignore. Submit via the
   Google Disavow Tool and log the file version and date.
8. Benchmark against 2–3 competitors: referring-domain growth, editorial-vs-
   directory mix, and the link types their profiles have that ours lacks.
9. Deliver the audit with a 90-day monitoring plan, and re-screen velocity and
   new-link quality monthly alongside the backlink-building register.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Profile data (primary) | Ahrefs Site Explorer, Semrush Backlink Audit | Deepest indexes; Toxic Score is a hint only |
| Google's own view | Google Search Console Links report | Free; the set Google confirms counts |
| Historic index & trust metrics | Majestic | Trust Flow/Citation Flow for legacy checks |
| Disavow submission | Google Disavow Tool | Search Console account required |
| Bulk domain checks | Google Sheets, Ahrefs batch analysis | Cross-reference metrics at scale |
| Indexation checks | site: searches, URL Inspection | Confirm whether linking pages are indexed |

## Example AI Prompt

```text
Act as a link auditor. Analyze the attached backlink export for {URL}
({N} referring domains, window {RANGE}). Also attached: anchor text summary,
GSC top linked pages, and the register of links we built intentionally.

Tasks:
1. Profile health scorecard: growth trend, follow/nofollow mix, DR spread, and
   anchor distribution versus the healthy pattern (brand-dominant anchors).
2. Flag risk patterns with evidence: velocity spikes, sitewide/footer links,
   PBN signatures, exact-match anchor clusters, hacked-page or foreign-spam
   links.
3. Output a verdict table: domain | metric | pattern observed | verdict
   (Toxic / Suspicious / Low-value / Healthy) | recommended action.
4. Draft a disavow file ONLY for clear manipulation — one line of rationale per
   inclusion; per Google's guidance, default to ignoring rather than disavowing.
5. Gap benchmark: link types and sources in {COMPETITOR EXPORTS} missing from
   our profile.
Rule: never call a link toxic on metrics alone — cite the specific pattern.
```

## Edge Cases & Guardrails

- Disavow sparingly: Google's default is to ignore spammy links it detects; bulk
  disavowing neutral links discards real value — reserve disavow for clear
  manipulation (paid networks, hacks, coordinated negative-SEO spikes).
- A manual action overrides all heuristics: follow Google's documented cleanup and
  reconsideration-request process exactly, including the removal-outreach step.
- Nofollow is not toxic: rel="nofollow", "sponsored", and "ugc" are normal
  attributes; a natural profile contains plenty of them.
- Toxicity scores from tools are starting hints, never final verdicts — manual
  sampling of flagged domains is mandatory before any disavow line is written.
- Sudden spikes may be earned PR coverage; cross-check referral traffic, brand
  mentions, and the campaign register before treating a spike as an attack.
- Post-Penguin, mass emailing webmasters for link removals is wasted effort unless
  a manual action explicitly requires it.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Referring-domain growth | Steady, matching the campaign plan | 100s of new RDs overnight |
| Exact-match anchor share | <10% of all anchors | >25% concentrated in one cluster |
| Follow vs nofollow mix | Roughly 60–90% follow | 100% follow from low-quality domains |
| Topically relevant links | >70% of new referring domains | Majority unrelated TLDs/languages |
| Disavow file growth | Rare, surgical additions | Hundreds of domains added monthly |
| Manual actions | 0 | Any "unnatural links" notice |

## Handoffs

- ← **backlink-building:** receives every new placement for hygiene logging and
  anchor monitoring.
- → **seo-audits:** supply the link section (scorecard, risks, gaps) for full
  site health checks.
- → **reporting:** deliver penalty-risk status and profile growth trends.
- → **dev/IT:** route disavow file submission if Search Console access is
  centralized.
- ↑ **seo-agent:** escalate manual actions and confirmed negative-SEO attacks
  immediately — these are channel-level incidents.
