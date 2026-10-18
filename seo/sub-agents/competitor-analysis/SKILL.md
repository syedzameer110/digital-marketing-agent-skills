---
name: seo-competitor-analysis
description: Reverse-engineers the SEO strategies of true SERP competitors — their winning keywords, content playbook, backlink profile, and technical posture — and turns the gaps into a prioritized attack plan. Use this skill whenever the user asks why a competitor outranks them, wants a keyword or content gap analysis, share-of-voice tracking, competitor benchmarks, or market-entry SEO research — even if they just say "compare us to {competitor}".
---

# Competitor Analysis — SEO Sub-Agent

## Role & Mission

Reverse-engineer the SEO strategies of the domains actually winning your SERPs: their
keywords, content playbook, link profile, and technical posture. The output is not a
data dump — it is a gap analysis with an attack plan: what they win that you ignore,
what it is worth, and the fastest route to take it. Note that SERP competitors and
business competitors are different sets, and confusing them wastes quarters.

## When to Use

- "Why does {competitor} outrank us?" or losing share of voice on key terms
- Entering a new market, niche, or product category
- Quarterly strategy review and benchmarking refresh
- Sizing the authority gap before commissioning link campaigns
- New site planning — understanding who holds the SERP and why
- A rival launched an aggressive content or link push

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| 3–5 competitor domains (SERP-verified) | Yes | From SERP review or Ahrefs competing domains |
| Target keyword set | Preferred | Shared universe from keyword-research |
| Own-site baseline | Yes | DR, ranking keywords, content count, RD growth |
| Tool access (Ahrefs/Semrush) | Yes | Gap and backlink exports |
| Business context | Optional | Margins, differentiators, no-go topics |

## Output Contract

Return a competitor intelligence report: (1) a competitor scorecard table, (2) a
keyword gap table segmented by intent, (3) content gap themes with formats, (4) a
backlink gap summary with replicable sources, and (5) a prioritized attack plan.
Core scorecard format:

```markdown
| Competitor | DR | Organic traffic | Top-10 kw | Content velocity | Link velocity | Primary gap to exploit |
|---|---|---|---|---|---|---|
| rivalhr.com | 58 | 240K/mo | 3,100 | 12 posts/mo | +22 RD/mo | No tools/templates; weak mobile speed |
| payrolly.io | 44 | 96K/mo | 1,750 | 4 posts/mo | +8 RD/mo | Thin comparison content; no original data |
| hrweekly.com | 61 | 310K/mo | 4,200 | 8 posts/mo | +35 RD/mo | News-heavy; evergreen guides outdated |
```

## Workflow

1. Identify true SERP competitors, not assumed ones: pull domains sharing the most
   keywords (Ahrefs "Competing Domains", Semrush Organic Research) and verify by
   eyeballing live results for the money terms.
2. Build the scorecard: DR, organic traffic, keyword count, traffic value, top
   pages, publishing velocity, and referring-domain growth for each rival and you.
3. Run the keyword gap: terms they rank top-10 for where you rank absent or worse
   (Ahrefs Content Gap, Semrush Keyword Gap); segment by intent and cluster.
4. Decompose their content strategy: top pages, formats, depth, update cadence,
   and title angles; identify what actually earns their traffic — not just what
   they publish.
5. Decompose their backlink strategy: most-linked assets, source types, and
   velocity; list replicable link sources for backlink-building.
6. Sample their technical posture: PageSpeed and CWV on their money templates,
   schema usage, and mobile UX — technical edges explain rankings content cannot.
7. Quantify each gap: traffic value at stake, difficulty, effort to compete, and
   time-to-result; separate quick wins from strategic bets.
8. Produce the attack plan: 10–15 prioritized actions across content, links, and
   technical, each with an owner, effort (S/M/L), and expected impact — then hand
   workstreams to the owning sub-agents.
9. Schedule a quarterly refresh: competitor moves and SERPs shift; stale
   intelligence creates misplaced confidence and misallocated budget.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Keyword & traffic gaps | Ahrefs Content Gap, Semrush Keyword Gap | Paid; core gap-analysis engines |
| Backlink comparisons | Ahrefs Backlink Intersect, Majestic Clique Hunter | Find sources rivals share |
| Traffic estimates | Semrush Traffic Analytics, SimilarWeb (free tier) | Directional only — validate big claims |
| Content cadence tracking | Ahrefs Top Pages, Feedly, manual SERP reviews | Watch launches and refresh patterns |
| Scorecard assembly | Google Sheets, Looker Studio | One living benchmark file |
| Technical sampling | PageSpeed Insights, Screaming Frog (list mode) | Compare money templates, not homepages |

## Example AI Prompt

```text
Act as an SEO competitive intelligence analyst. Compare {SITE} against these
SERP competitors: {COMPETITOR DOMAINS}. Our profile: DR {DR}, {N} ranking
keywords, {M} content pages, ~{L} referring domains. Target keywords:
{KEYWORD SET OR ATTACHMENT}.

Deliver:
1. A competitor scorecard (DR, est. traffic, top-10 keywords, content velocity,
   link velocity) with our position in it.
2. Keyword gap: top 25 terms they win and we do not, grouped by intent, each
   with difficulty and an honest 6-month winnability verdict for our authority.
3. Content gap: 5 themes where their formats beat ours (tools, comparisons,
   original data, templates) with concrete counter-format proposals.
4. Backlink gap: 10 sources they hold that we do not, each with a pitch angle.
5. An attack plan: 10 prioritized actions with effort (S/M/L) and expected
   impact, split into quick wins vs strategic bets.
Flag any "competitor" that is really a marketplace or authority we should not
chase head-on, and say what to do instead.
```

## Edge Cases & Guardrails

- Business competitors are not SERP competitors: marketplaces (Amazon), media
  brands, and aggregators often own results — segment them and route around, not
  through, unless the site has comparable authority.
- Third-party traffic estimates are directional models, not facts: validate any
  claim that drives budget with Search Console data or live SERP sampling.
- Competitors make mistakes too: check whether their top pages convert, not just
  rank — replicating a traffic trap wastes a quarter.
- Filter every gap by business relevance and margin, not raw volume; a 50K/mo
  keyword that cannot monetize is a distraction dressed as opportunity.
- DR and authority scores are proprietary heuristics that differ across tools —
  use them as filters and trend lines, never as goals.
- Tool indexes lag reality by days to weeks: for fresh rival launches, monitor
  their new pages and sitemaps directly rather than trusting exports.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Share of tracked top-10 vs competitor set | Growing QoQ | Losing share 2+ quarters straight |
| Keyword gap closed | 10–20% of P1 gaps per quarter | Gap widening despite investment |
| Content velocity parity | Within ~1.5× of the category leader | Publishing 5× less than rivals |
| Referring-domain growth parity | ≥50% of the leader's velocity | Negative net growth |
| Analysis refresh cadence | Every quarter | Last analysis older than 12 months |
| Attack-plan execution rate | >60% of actions shipped per quarter | Reports that never become work |

## Handoffs

- ← **keyword-research:** shares the keyword universe and difficulty baselines.
- → **backlink-building:** deliver the link-gap list and replicable source types
  with pitch angles.
- → **content-ideation:** deliver content gaps as topic and format candidates.
- → **on-page-optimization:** flag pages where a rival's on-page execution beats
  ours on the same intent.
- → **reporting:** feed share-of-voice and benchmark trends into the monthly pack.
- ↑ **seo-agent:** escalate strategic threats — a funded rival's content blitz or
  an SERP structure change that undermines the channel strategy.
