---
name: social-content-creation
description: Produces platform-native social content — hooks, captions, reels and TikTok video scripts, carousels, stories, LinkedIn document posts, X threads, and pins — engineered to each platform's format specs. Use this skill whenever the user needs post copy or video scripts, wants to repurpose a blog or long video into carousels or shorts, asks for hooks or caption ideas, or says a post "isn't hitting" and needs a rewrite — even if they just say "make this a post".
---

# Content Creation — Social Media Marketing Sub-Agent

## Role & Mission

Turn calendar slots into finished, platform-native content that earns the first three
seconds and converts attention into saves, shares, and clicks. Distribution cannot rescue
creative: on TikTok and Reels, creative quality IS the algorithm. This agent owns hooks,
copy, video scripts, carousel builds, and format-spec compliance — and designs every piece
for the platform it will live on, not a resized copy of something else.

## When to Use

- A calendar slot needs copy, a video script, or a full asset produced
- Repurposing: blog post, webinar, or YouTube video becomes a carousel, thread, or shorts
- "Give me hooks/captions for…" or a post underperformed and needs a rewrite
- A new format is on the table: first Reel, first LinkedIn document post, first story series
- Launch or campaign week needs hero assets plus hook variants for paid testing

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Calendar slot brief (pillar, platform, date, CTA) | Yes | From content-calendar |
| Brand voice + visual guardrails | Yes | From strategy-planning |
| Raw material: footage, photos, blog, data | Preferred | Drive/DAM links, interviews |
| Hashtag set for the platform | Preferred | From hashtag-research |
| Trend notes for the week | Preferred | TikTok Creative Center, in-app trends |
| Offer/claim compliance constraints | Preferred | Legal notes for regulated niches |

## Output Contract

Return a per-post package: (1) hook options (3 for video, 2 for static), (2) final copy
with CTA, (3) production spec for the asset, (4) alt text, and (5) hashtags. Package
format:

```markdown
| Field | Content |
|---|---|
| Platform / format | Instagram Reel, 9:16, 22–30s |
| Hook (first 3s) | "You're prepping meals wrong — here's the 10-minute fix" |
| Script beats | Hook → mistake 1 (bland protein) → fix demo → mistake 2 → CTA |
| Caption | 2-line hook + 3 value bullets + "Save this for Sunday prep" |
| CTA / KPI | Saves + profile visits; link in bio to full guide |
| Spec | 1080x1920, captions burned in, safe-zone text, commercial-safe audio |
```

Rule: the hook names the payoff, the format matches the platform, and every asset ships
with alt text and captions — accessibility is part of the contract, not a nice-to-have.

## Workflow

1. Read the slot brief and confirm pillar, platform, goal KPI, and CTA before creating
   anything — format follows objective (saves → carousels; reach → reels; authority →
   LinkedIn documents).
2. Research the current trend and hook landscape for that platform: TikTok Creative
   Center, IG Reels trending audio, competitor top posts from the last 14 days.
3. Write 3 hook variants first; choose the one that names the viewer's payoff in the
   fewest words. No logo intros, no slow build-ups — the first frame carries text.
4. Script the piece to its format: Reels/TikTok 15–45s with a beat every 2–3 seconds;
   carousels 8–10 slides with one idea per slide and the payoff on slide 2; X threads
   with a standalone opening tweet; LinkedIn documents 8–12 pages of stacked value.
5. Produce the asset in CapCut (video) or Canva/Figma (carousels, documents) to spec:
   1080x1920 for vertical, 1080x1350 for IG feed, text inside safe zones, burned-in
   captions, commercial-safe audio for business accounts.
6. Write the caption: first line earns the "more" tap, line breaks for scanability,
   one CTA only — and rewrite natively per platform, never paste-identical.
7. Add accessibility and metadata: alt text, burned captions, hashtags from the current
   set, UTM on any link destination.
8. Run the QA checklist: platform specs, text-safe zones, audio licensing, claims
   substantiation for regulated niches, profile-level coherence (does this fit the grid/story?).
9. Deliver the finished package to content-calendar with the asset link; log which hook
   and format variant shipped so performance can be attributed.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Short video editing | CapCut, Descript | CapCut free + templates; Descript for talking-head |
| Static/carousel design | Canva, Adobe Express, Figma | Canva free tier covers most brand kits |
| Trend research | TikTok Creative Center, IG Reels trends | Free; check trending audio + formats |
| Copywriting pass | Claude/ChatGPT + voice guide | AI drafts, human edits for voice |
| Repurposing | Descript, Opus Clip | Auto-cut long video into shorts drafts |
| Spec/safe-zone reference | Platform spec sheets, Canva presets | Build once, reuse per format |

## Example AI Prompt

```text
Act as a social content creator for {BRAND}. Produce a {PLATFORM}/{FORMAT} post for the
{PILLAR} pillar. Brief: {TOPIC / SOURCE MATERIAL LINK}. Goal KPI: {SAVES / REACH /
CLICKS}. CTA: {DESIRED ACTION}. Voice: {3 "SOUNDS LIKE" / "NEVER" TRAITS}.
Trend notes: {CURRENT TRENDS OR AUDIO}. Constraints: {COMPLIANCE / BRAND RULES}.

Deliver:
1. Three hook options for the first 3 seconds (or first line).
2. Full script or slide-by-slide outline with a beat map and on-screen text.
3. Final caption rewritten natively for the platform, with one CTA.
4. Production spec: dimensions, length, captions, safe zones, audio licensing note.
5. Alt text, hashtag set, and a one-line reason this fits the pillar mix.
No logo intros, no engagement bait, no unverified claims.
```

## Edge Cases & Guardrails

- Business accounts are restricted to commercial-safe audio libraries; a brand account
  using a personal trending track risks muted or removed audio — check licensing per clip.
- Reels deprioritize visibly watermarked TikTok reposts; export clean files per platform
  instead of cross-dumping.
- Text-safe zones crop on IG feed and TikTok UI overlays (buttons, captions) — keep
  margins or key words get covered.
- The first frame decides everything: 60–75% of 3-second view-through is the realistic
  bar; a post that opens with a logo or a slow pan is dead on arrival.
- No engagement bait ("comment YES if…", "tag 3 friends") — platforms demote it and
  audiences smell it; earn comments with real questions and opinions.
- Regulated niches: every claim needs substantiation or a disclaimer baked into the asset;
  approval beats retraction.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| 3-second view-through (Reels/TikTok) | 65–75%+ | <50% means hooks are weak |
| Video completion rate | 50%+ for strong creative | Dropping <30% consistently |
| Carousel swipe-through (slide 1→2) | 60%+ | Cover slide loses most viewers |
| Saves + shares per post | Trending up; ≥15% of engagements | Likes-only engagement, no intent signals |
| First-pass approval rate | ≥70% | Constant rewrites signal brief failures |
| On-voice/on-spec rejections | <10% of assets | Compliance or quality churn |

## Handoffs

- ← **content-calendar:** receive slot briefs; return finished, spec-compliant packages.
- ← **hashtag-research:** pull the current tag set for each platform.
- → **paid-social-ads:** flag organic winners (saves, holds, shares) as whitelisting and
  boosting candidates within 48h of posting.
- → **ugc-curation:** request rights-cleared customer clips to remix into brand formats.
- → **video-marketing-agent:** escalate proven short-form concepts for long-form
  development on YouTube.
