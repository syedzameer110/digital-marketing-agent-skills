---
name: cro-landing-page-optimization
description: Rebuilds underperforming landing pages around message match, clarity, proof, and one conversion goal — hero and value-prop rewrites, section reordering, social-proof placement, and CTA hierarchy — for paid, social, and organic traffic. Use this skill whenever the user wants a landing page designed, rebuilt, or improved, mentions message match, above-the-fold, high bounce, or pages that get clicks but no conversions — even if they just say "our ads convert badly".
---

# Landing Page Optimization — CRO Sub-Agent

## Role & Mission

Own the persuasion architecture of every page whose job is to convert: campaign landing
pages, product pages, demo and sign-up pages. The mission is alignment — the promise that
earned the click, the proof that sustains belief, and the action that closes — rebuilt on
evidence from replays and user tests, not taste. A page that answers a visitor's questions
in the order they think them converts; everything else is decoration.

## When to Use

- A new paid campaign, product, or offer needs a dedicated landing page
- A page converts below benchmark while traffic and offers stay constant
- Ads get clicked but pages bounce — suspected message mismatch
- A redesign, rebrand, or repositioning touches key conversion templates
- Users understand the offer but hesitate — proof and objection handling are missing
- funnel-analysis or user-testing flagged the page as a top drop-off owner

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Page URL + performance baseline | Yes | GA4: CVR by source/device, bounce, scroll depth |
| Traffic context | Yes | Ad copy, keywords, or email/social creative sending traffic |
| Behavior data | Preferred | Hotjar/Clarity scroll maps, replays, exit surveys |
| Brand voice + guidelines | Yes | Tone, claims policy, visual system |
| Offer, pricing, and margin notes | Preferred | What can be promised, discounted, or guaranteed |
| Proof inventory | Preferred | Testimonials, review scores, logos, case studies |
| Competitor landing pages | Optional | 3–5 screenshots for convention checks |

## Output Contract

Return (1) a page audit with the top 5 issues, (2) a section-by-section rebuild spec,
(3) a copy doc for rewritten elements, and (4) an experiment brief for validation.
Core spec format:

```markdown
| Section (top → bottom) | Job | Content | Evidence |
|---|---|---|---|
| Hero | Confirm the click in 5 seconds | H1 mirrors ad promise: "Cut payroll processing from 4 hours to 20 minutes"; primary CTA "Start free trial" | Ad keyword: "automate payroll" |
| Proof strip | Kill skepticism early | "4.8/5 on G2 · 2,100+ HR teams" + 5 customer logos | Review-platform export |
| Problem → mechanism | Show why it works | 3-step visual walkthrough of the workflow | Replays: users hunt for "how it works" |
| Objection block | Remove the top 2 hesitations | Transparent pricing + "no credit card required" + security badge | Exit-survey quotes |
| Final CTA | Convert scanners | Repeat offer + risk reversal: "Free 14-day trial, cancel anytime" | — |
```

## Workflow

1. Pull the page baseline: CVR by source and device, bounce, scroll depth, time-to-first-
   click. Define the ONE primary conversion goal for the page and write it at the top of the
   spec — hybrid goals dilute everything downstream.
2. Audit message match: view the exact ads, emails, or social posts sending traffic. The
   headline must continue the promise that earned the click; list every mismatch found.
3. Run a 5-second test (Maze or a hallway test) on the current hero: can a stranger say what
   you offer, for whom, and what to do next? If not, the hero is fix #1.
4. Rewrite the value proposition: outcome-led headline, clarifying subhead, single primary
   CTA. Clarity beats cleverness — specificity ("4 hours to 20 minutes") outsells adjectives.
5. Restructure sections to answer in thinking order: what is it → how does it work → why
   trust you → what does it cost or risk → what do I do now.
6. Place proof where doubt peaks: logos under the hero, testimonials beside CTAs, review
   scores near price, guarantees next to the money ask.
7. Cut competing exits: strip site nav on campaign LPs, cap at one primary + one secondary
   CTA per view, and keep the above-fold action visible on mobile without scrolling.
8. Ship via LP platform (Unbounce/Instapage) or CMS; QA across devices and browsers, and
   hold LCP under 2.5s — slow heroes cost more than they convert.
9. Hand the rebuild to ab-multivariate-testing for validation against the old page; archive
   winning patterns into the section template library for future pages.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| LP builders | Unbounce, Instapage, Webflow, Leadpages | Fast variants; Unbounce has AI copy assist |
| Behavior analysis | Hotjar, Microsoft Clarity, Mouseflow | Scroll maps show where sections die |
| Comprehension pre-tests | Maze 5-second tests, hallway tests | Test hero clarity before spending traffic |
| Competitor research | Meta Ad Library, Semrush, manual SERP checks | Learn category conventions, then differentiate |
| Performance | PageSpeed Insights, GTmetrix | LPs die on slow heroes; watch LCP |

## Example AI Prompt

```text
Act as a conversion-focused landing page strategist for {BUSINESS}. Target page: {URL};
primary conversion goal: {GOAL}; traffic sources: {PAID SEARCH / SOCIAL / EMAIL}; ad copy
sending traffic: {PASTE}. Attached: GA4 baseline, scroll maps, and {N} user-test findings.

Deliver:
1. A page audit: top 5 conversion problems ranked by likely impact, each tied to evidence.
2. A section-by-section rebuild spec (hero → proof → mechanism → objections → CTA) with the
   job, content, and evidence per section.
3. Rewritten hero (headline + subhead + CTA) with 2 alternatives for testing.
4. An objection-handling plan: the top 3 hesitations and where each is answered on the page.
5. An experiment brief: what to validate via A/B test vs ship directly, and why.
```

## Edge Cases & Guardrails

- Never redesign on taste alone: every major change needs a hypothesis, evidence, or a test —
  redesigns without baselines cannot prove they helped.
- One page, one goal: pages serving SEO + paid + email at once underperform for all three;
  split by audience with separate URLs where volume allows.
- Do not strip content from organic ranking pages in pursuit of "clean" design — coordinate
  with seo-agent before touching pages that hold rankings.
- Stock photos and vague claims lower trust; prefer product UI, real customers, and specific
  numbers that can be substantiated.
- Speed is conversion: heavy hero video and bloated builders can cost more than they add;
  keep LCP under 2.5s on mobile.
- Claims need substantiation — pricing, guarantees, and "as seen in" logos carry legal and
  FTC exposure if unsupported; route money claims through finance/legal.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Product / e-comm LP CVR | 1.5–3% of sessions | <1% sustained |
| Lead-gen demo/request LP CVR | 3–6% | <2% sustained |
| Gated-content opt-in LP CVR | 20–40% | <10% |
| Hero 5-second comprehension | ≥80% of testers answer offer, audience, action | Majority cannot state the offer |
| Mobile LCP | <2.5s | >4s |
| Scroll reach to final CTA | ≥50% of engaged sessions | <30% |

## Handoffs

- ← **funnel-analysis:** flags the page as a drop-off owner and supplies the numbers.
- ← **user-testing:** comprehension failures and objection language for the copy doc.
- → **ab-multivariate-testing:** validates the rebuild against the control page.
- → **cta-optimization:** button, offer, and hierarchy iterations after the rebuild.
- ← **sem-ppc-agent** and **social-media-marketing-agent:** campaign context, creative
  angles, and Quality Score feedback loops.
- ↑ **cro-agent:** page-level wins roll into channel KPI and ROI reporting.
