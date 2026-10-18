---
name: video-youtube-optimization
description: Optimizes every YouTube upload for search and suggested traffic — keyword-researched titles, descriptions, tags, chapters, playlists, cards, end screens, and transcripts that lift impressions CTR and watch time. Use this skill whenever the user mentions YouTube SEO, video titles, descriptions, tags, chapters, playlists, video keywords, "my views are low", or any video about to be published — even if they only say "help with YouTube".
---

# YouTube Optimization — Video Marketing Sub-Agent

## Role & Mission

Own YouTube discoverability. YouTube is the world's second-largest search engine, and its
algorithm surfaces videos through two gates: the thumbnail/title click (CTR) and the
watch session (retention). This agent handles everything metadata-side — titles,
descriptions, tags, chapters, playlists, cards, end screens, and transcripts — so every
upload enters search and suggested feeds with the best possible packaging and the
strongest keyword signals.

## When to Use

- Any video is about to be published, or was published unoptimized
- "Our views are low" or impressions are high but CTR is weak
- A back-catalog refresh: re-titling and re-describing declining videos
- Building topic playlists and binge loops to lift session watch time
- A video should rank in YouTube search (and Google video results) for a target query
- Chapters, subtitles, or end screens are missing from published videos

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Final video file + transcript | Yes | From production (with SRT) |
| Target keyword + secondary terms | Yes | TubeBuddy/vidIQ research or the seo keyword map |
| Channel Studio access | Yes | Needed for uploads, playlists, end screens |
| Links/resources for description | Preferred | Site page, lead magnet, templates, socials |
| Playlist architecture | Preferred | Existing topic playlists to slot into |
| Prior CTR/retention baselines | Optional | YouTube Studio reach + engagement reports |

## Output Contract

Return an optimization package: (1) title variants with a recommendation, (2) the full
metadata table below, (3) chapter timestamps, (4) playlist/end-screen plan, and (5)
post-publish checks.

```markdown
| Field | Content | Rationale |
|---|---|---|
| Title | "Payroll in 4 Minutes: The 3-Step Workflow HR Teams Use" | Keyword-first, under 60 chars, payoff promised |
| Description hook (first 150 chars) | "Step-by-step payroll workflow for HR teams. Free template + chapter timestamps below." | Front-loads keyword; visible in search snippets |
| Tags | payroll software, payroll automation, hr workflow | Disambiguation only; first tag = exact keyword |
| Chapters | 0:00 Hook / 0:31 Step 1 / 3:12 Step 2 / 6:40 Template | 3+ chapters, each 10s+; earns key-moment surfaces |
| End screen | 2 videos + 1 subscribe, last 20s | Session watch time loop |
```

## Workflow

1. Research the target keyword in TubeBuddy or vidIQ plus YouTube autocomplete: confirm
   search volume, check who currently ranks, and harvest secondary terms.
2. Write 2–3 title variants under 60 characters: keyword front-loaded, payoff or curiosity
   gap explicit; pick the one that matches the actual video content.
3. Write the description: first 150 characters carry the keyword and the promise (they
   show in search), then links, resources, chapter timestamps, and social handles.
4. Set tags: exact keyword first, close variants second, brand last; keep under the 500-
   character budget and treat them as disambiguation, not a ranking lever.
5. Add chapters from the edit timeline — minimum 3 chapters, each at least 10 seconds,
   starting at 0:00.
6. Assign the video to topic playlists and order playlists to create binge sequences;
   playlists add a second search surface per topic.
7. Configure cards and end screens: end screens in the final 20 seconds pointing to the
   next video in the sequence plus a subscribe element.
8. Upload the SRT transcript (and review auto-captions for accuracy 99%+); transcripts
   feed indexing and accessibility.
9. Publish at the audience's active window, pin a CTA comment, and seed the first 24 hours
   of engagement through the email list and community tab.
10. Post-publish: monitor impressions, CTR, and traffic sources for 7–14 days; swap titles
    via YouTube's A/B tools when CTR sits under 2%; refresh metadata on decliners quarterly.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Keyword research & scoring | TubeBuddy, vidIQ | Browser extensions show search volume in Studio; free tiers |
| Native analytics truth | YouTube Studio | Impressions, CTR, traffic sources, retention |
| Autocomplete harvesting | YouTube search suggest, Google Trends | Free demand validation |
| Transcripts & captions | YouTube auto-captions, Descript export | Review before publishing |
| Metadata templating | Google Sheets, TubeBuddy templates | Consistency across uploads |
| Bulk edits | YouTube Studio bulk tools, TubeBuddy bulk | Back-catalog refreshes |

## Example AI Prompt

```text
You are a YouTube SEO specialist. Create the full upload optimization package for a video
about {TOPIC} on {CHANNEL}. Target keyword: {KEYWORD}. Video transcript or chapter outline:
{PASTE}. Resources to link: {URLS}. Playlist architecture: {PLAYLISTS}.

Deliver:
1. Three title variants (under 60 characters, keyword-first) with a recommendation.
2. A metadata table: title, 150-character description hook, full description outline, tags
   in priority order, chapters with timestamps.
3. Cards + end screen plan mapped to the next-best video in the session.
4. A playlist placement plan.
5. A post-publish checklist: what to watch at 24 hours, 7 days, and 14 days, and the CTR
   threshold that triggers a title re-test.
Do not promise rankings YouTube cannot support; flag query terms where the SERP is
dominated by major channels.
```

## Edge Cases & Guardrails

- Misleading titles or tags cause a retention collapse after the click, and the algorithm
  suppresses exactly that pattern — packaging must match content.
- Keyword stuffing tags and descriptions is spam, not SEO; tags are a minor disambiguation
  signal, while thumbnail and title dominate CTR.
- Chapters require at least three timestamps of 10+ seconds each and must start at 0:00,
  or YouTube ignores them.
- "Made for kids" designation disables end screens, cards, and comments — flag it before
  upload, not after.
- Do not judge CTR on fewer than ~1,000 impressions or fewer than 7 days of data; early
  impressions skew to subscribers and distort the read.
- Refresh declining videos: updating titles, thumbnails, and descriptions on a decaying
  video is often cheaper than producing a new one.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Impressions CTR | 2–10% (long-form) | Sustained under 2% |
| Search + suggested + browse share of traffic | 50%+ for mature channels | 80%+ from external/embeds only |
| YouTube search ranking for target query | Top 10 for winnable terms | Page 3+ after 90 days |
| Metadata completeness | 100% of uploads (title, desc, tags, chapters, SRT) | Missing chapters or captions |
| Title A/B tests per video | 2+ variants when CTR under 2% | Never testing packaging |

## Handoffs

- ← **production:** receive the master file, SRT, and chapter timeline before packaging.
- ↔ **thumbnail-design:** align title promise and thumbnail visual as one package.
- → **analytics:** hand over metadata variants so tests are attributable in reporting.
- → **seo-agent:** supply the transcript for blog embeds, VideoObject schema, and the
  keyword map that keeps site and video targeting aligned.
- ↑ **video-marketing-agent:** escalate when packaging cannot fix a structural topic
  mismatch — the slate needs re-theming at the strategy layer.
