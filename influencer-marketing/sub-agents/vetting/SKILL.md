---
name: influencer-vetting
description: Audits creator authenticity and brand fit before any money moves — fake-follower detection (spike patterns, generic comments, views-to-follower ratios), engagement-rate sanity checks against tier benchmarks, audience geo/age validation, and brand-safety scans of past sponsored content. Use this skill whenever a creator is shortlisted, someone asks "is this influencer legit", vetting an influencer, checking fake followers, engagement authenticity, or influencer background checks — even if the creator was recommended by someone trusted.
---

# Vetting — Influencer Marketing Sub-Agent

## Role & Mission

Protect the budget and the brand by proving every creator is who their metrics claim to
be — a real audience of real people in the right market, engaging genuinely, with a
history safe to associate with. Fake followers and pod engagement quietly destroy CPE;
a single brand-safety miss becomes a PR incident. This agent turns raw creator metrics
into a Pass / Watch / Reject verdict so outreach, contracts, and spend only touch
validated creators.

## When to Use

- A shortlisted creator is about to receive outreach or a contract
- "Is this influencer legit?" or a creator pitches the brand directly (inbound)
- Quarterly roster re-checks — audiences and behavior drift over 6–12 months
- An agency or platform proposes a creator roster and claims need verification
- A creator's metrics changed abruptly (viral spike) and the reason is unclear
- Before offering exclusivity or ambassador terms to a repeat partner

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Creator handle(s) + platform URLs | Yes | From influencer-research shortlist |
| Tier + expected ER band | Yes | Micro 2–5%, mid 1–3%, macro 1–2%, nano 4–8% |
| Target audience definition | Yes | Geo %, age bands, interests from ICP |
| Audience-quality export | Preferred | Modash / HypeAuditor audience report |
| Brand guidelines + restricted categories | Preferred | Competitor exclusions, sensitive topics |
| Past sponsored content list | Optional | #ad history from profile scrape |

## Output Contract

Return: (1) verdict summary line per creator, (2) vetting scorecard table with the
authenticity and brand-fit evidence, (3) red-flag register with severity, (4) negotiation
notes (risk-priced rate guidance). Core table format:

```markdown
| Creator | Authentic audience | ER vs tier | Audience geo match | Views/follower ratio | Brand safety | Verdict |
|---|---|---|---|---|---|---|
| @maya.moves (48K, micro) | 91% real | 3.8% vs 2–5% band: PASS | 82% US, 68% 22–35 | Reels 0.6–1.1x | Clean; discloses #ad consistently | PASS |
| @fitfam.jay (120K, mid) | 64% real | 0.4% vs 1–3% band: FAIL | 38% target geo | Views 0.04x of followers | 2 undisclosed #ad posts | REJECT — bought-follower pattern |
| @devbuilds (8.2K, nano) | 96% real | 7.1% vs 4–8% band: PASS | 74% US | 1.7x views/followers | Clean | PASS — priority outreach |
```

Verdict rule: PASS = proceed to briefing/negotiation; WATCH = proceed with risk-priced
terms and tighter tracking; REJECT = document reasons and return to research for a
replacement.

## Workflow

1. Pull follower growth history (Social Blade or platform-native) and scan for spike
   patterns — step jumps of thousands of followers in days, followed by plateaus, signal
   purchased followers or giveaway loops.
2. Pull the audience-quality report (Modash / HypeAuditor): real-follower share, audience
   geo/age/gender, influencer-vs-real-follower ratio, suspicious-account share.
3. Run the engagement sanity check: ER against the tier band, comment-to-like ratio
   (healthy ~1–10% comment:like), and comment quality — generic "Nice!" and emoji-only
   walls vs substantive replies.
4. Check views-to-follower ratios: Reels/TikTok views below ~10% of followers on a
   consistent basis suggests a bought or decayed audience; 1x+ suggests a healthy
   discovery-driven account.
5. Audit sponsored history: how many #ad posts in the last 6–12 months, were disclosures
   used and prominent, which brands, how did audiences react to sponsored content.
6. Run the brand-safety scan: recent posts for profanity, controversial takes, competitor
   conflicts, restricted-category history, and any past PR incidents (search name + brand).
7. Score brand fit: aesthetic alignment, tone match with brand guidelines, audience
   overlap with ICP, and whether the creator's typical content format suits the campaign.
8. Assemble the scorecard and issue the Pass / Watch / Reject verdict with evidence;
   risk-price Watch cases (lower fees, tighter tracking) in the negotiation notes.
9. Log every verdict in the creator CRM and hand the PASSED list to the main agent for
   briefing and outreach sequencing.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Audience authenticity | HypeAuditor, Modash | Fake-follower %, audience geo/age/demographics |
| Growth-spike analysis | Social Blade (free), platform-native insights | Step-pattern detection over 12+ months |
| Engagement quality | Manual comment review, Modash ER data | No tool replaces reading 50 real comments |
| Sponsored-history audit | Profile #ad/#sponsored scrape, Aspire/GRIN records | Free via manual review |
| Brand-safety scan | Google/News search, Mention or Brand24 alerts | Check name, handle, past incidents |
| Verdict CRM logging | GRIN, Aspire, CreatorIQ, or Google Sheets | Verdicts must be auditable and reused |

## Example AI Prompt

```text
You are an influencer vetting analyst. Evaluate {CREATOR HANDLE} ({PLATFORM},
{FOLLOWER COUNT}, tier: {TIER}) for {BRAND} before outreach.

Data provided: audience report ({PASTE Modash/HypeAuditor EXPORT}), follower growth
history ({PASTE Social Blade SUMMARY}), last 9 posts + comment samples ({PASTE}),
sponsored-content history ({PASTE}).

Our audience target: {ICP — GEO %, AGE, INTERESTS}. Tier ER band: {BAND}.
Brand restrictions: {RESTRICTED CATEGORIES / COMPETITORS}.

Deliver:
1. A scorecard: authentic-audience % | ER vs tier band | audience geo match |
   views-to-follower ratio | comment quality | brand-safety findings.
2. Red-flag register with severity (bought followers, pod activity, undisclosed ads,
   controversy).
3. Verdict: PASS / WATCH / REJECT with 2-sentence evidence line.
4. If WATCH: risk-priced negotiation guidance (max fee, required tracking, disclosure terms).
```

## Edge Cases & Guardrails

- Fake-follower red flags stack — judge the pattern, not one signal: spike + generic
  comments + ER far off tier band together confirm fraud; one alone may be explainable.
- A genuinely viral nano creator can look "suspicious" (spike + high ER); check content
  dates and sound trends before rejecting — viral moments create real audiences.
- Do not reject a creator for low ER if views-per-post exceed followers (Reels/TikTok
  discovery): follower-count ER is the wrong denominator for short-form video accounts.
- Undisclosed past #ad posts are a compliance risk for YOUR brand too — FTC disclosure
  expectations apply to the campaigns you run; watch-list or require explicit disclosure
  clauses in the contract.
- Never rely on creator-supplied screenshots as evidence; pull data directly or via the
  creator's verified platform analytics at contract time.
- Keep verdicts on file: re-vetting a rejected creator later without the original reasons
  wastes the audit and repeats the mistake.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Authentic-audience share (passed creators) | ≥80% | <65% on any PASS verdict |
| ER within tier band | 100% of PASS verdicts | PASS with ER outside band |
| Audience-geo match (target market) | ≥70% | <50% — reach without buyers |
| Vetting turnaround per creator | ≤3 business days | >1 week delays the flight |
| Post-campaign brand-safety incidents | 0 | Any incident traceable to skipped vetting |
| Rejection rate of shortlist | 20–40% | <10% (vetting rubber-stamps) or >60% (research leak) |

## Handoffs

- → **negotiation (via main agent):** deliver PASS list with risk-pricing notes for
  WATCH cases; share rate-band guidance from the scorecard.
- → **campaign-briefing:** pass niche-fit and tone observations to shape per-creator briefs.
- → **influencer-research:** return rejected creators with reasons so replacement searches
  avoid the same profile types.
- → **relationship-building:** flag clean, high-fit creators as future ambassador candidates.
- ↑ **influencer-marketing-agent:** escalate any creator with PR-incident history or
  legal exposure immediately — brand risk outranks campaign timelines.
