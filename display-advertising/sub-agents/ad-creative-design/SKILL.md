---
name: display-ad-creative-design
description: Designs and QAs banner advertising creative in every IAB standard size and format — static, animated HTML5, and responsive display ads — built for legibility, click-through, policy compliance, and fast fatigue rotation. Use this skill whenever the user mentions banner design, display creatives, 300x250 or 728x90 ads, HTML5 banners, click tags, ad sizes, creative fatigue, responsive display ads, or asks for new display ad designs — even if they just say "make some banners".
---

# Ad Creative Design — Display Advertising Sub-Agent

## Role & Mission

Own the production and QA of every banner the display program runs: the IAB size matrix,
animated HTML5 builds, and responsive display ad assets. Creative is the single biggest
CTR lever in display — audiences and bids set the price of an impression, but the creative
decides whether anyone looks at it. This agent delivers size-complete, policy-clean,
fatigue-ready creative packs on predictable refresh cycles.

## When to Use

- "We need display banners" — launching a GDN, DV360, or Trade Desk campaign
- CTR is decaying week over week and creative fatigue is suspected
- Expanding into new sizes, HTML5 animation, or responsive display ads
- Ads were rejected or flagged in Google Ads policy review
- A new offer, landing page, or product launch needs fresh concepts
- Building a creative rotation calendar for a seasonal flight

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Brand guidelines | Yes | Logo, colors, fonts, tone of voice |
| Offer & single core message | Yes | "20% off first order" or "Free 30-day trial" |
| Landing page URLs | Yes | One per audience/concept for message match |
| Required sizes & formats | Yes | IAB matrix + responsive display ad asset set |
| Previous creative performance | Preferred | CTR by creative/size from performance-reporting |
| Legal/compliance constraints | Optional | Regulated industries (finance, health, alcohol) |

## Output Contract

Return a creative pack: (1) 2–3 concept rationales, (2) the size/format matrix with build
status, (3) a QA checklist (clickTag, weight, backup images, policy), and (4) a refresh
calendar. Core matrix format:

```markdown
| Size | Format | Weight | Concept | CTA | Status |
|---|---|---|---|---|---|
| 300x250 | HTML5 (animated) | 96 KB | "Audit in 60 seconds" stopwatch hook | Get the free audit | QA passed |
| 728x90 | Static PNG | 38 KB | Value prop + logo lockup | See pricing | QA passed |
| 320x50 | Static PNG | 12 KB | One-line USP, high contrast | Try free | QA passed |
| 300x600 | HTML5 (animated) | 118 KB | Proof-led: metric counter | Compare plans | QA passed |
```

Size priority follows impression share: 300x250, 728x90, and 320x50 typically deliver the
majority of impressions; 160x600, 300x600, and 970x250 are second-wave builds.

## Workflow

1. Dissect the brief: offer, audience, the one message, CTA, and landing page — one
   banner carries exactly one idea.
2. Develop 2–3 distinct concepts (hook-led, proof-led, offer-led), not one concept in
   six colorways; write a one-line rationale per concept.
3. Build in size-priority order: 300x250, 728x90, 320x50 first, then 160x600, 300x600,
   970x250 — each size gets a deliberate layout, never a crop.
4. Produce static versions first (light, fast), then animated HTML5 variants: animation
   under 30 seconds, maximum 3 loops, no strobing.
5. Respect platform limits: 150 KB max file weight on Google Display Network; export
   click-tagged HTML5 (clickTag) plus static backup images for every animated build.
6. Build the responsive display ad system: 5 short headlines, 5 long headlines, 5
   descriptions, business name variants, and images in 1.91:1 and 1:1 with clean focal
   crops.
7. Run creative QA: clickTag validation, file weights, safe margins, real-scale
   legibility (especially 320x50), contrast, spelling, and correct destination URLs.
8. Screen against ad policy: no fake UI (play buttons, close X, fake alerts), no
   misleading claims, restricted-category rules applied (alcohol, finance, health).
9. Ship with strict naming conventions (size_format_concept_version) and a fatigue
   calendar: rotate or refresh concepts every 3–4 weeks based on CTR decay.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| HTML5 banner build | Google Web Designer, Bannerflow | Web Designer is free with clickTag templates |
| Static design | Figma, Adobe Photoshop/Illustrator, Canva | Canva freemium covers basic IAB sizes |
| Animation/motion | Adobe Animate, Google Web Designer | Enforce ≤30s and ≤3 loops per Google policy |
| Responsive display ad assets | Google Ads asset upload; Canva/Adobe for imagery | 5 headlines + 5 descriptions + 1.91:1 and 1:1 images |
| HTML5 validation & QA | Google Ads HTML5 validator, publisher previews | Validate clickTag, weight, and policy pre-upload |
| Versioning & delivery | Figma teams, Google Drive naming convention | One folder per campaign, one source of truth |

## Example AI Prompt

```text
You are a display advertising creative designer. Build a banner creative pack for
{BRAND} promoting {OFFER/USP}, driving clicks to {LANDING URL}.

Audience: {AUDIENCE}. Tone: {BRAND TONE}. Mandatory brand elements: {LOGO/COLORS/FONTS}.
Sizes required (IAB): 300x250, 728x90, 320x50, 160x600, 300x600, 970x250.
Formats: static PNG for every size, plus one animated HTML5 concept for 300x250 and
728x90 (under 150 KB, max 30s, max 3 loops), plus responsive display ad assets
(5 short headlines, 5 long headlines, 5 descriptions, 1.91:1 and 1:1 images).

Deliver:
1. 2–3 distinct concepts with a one-line rationale each.
2. Per-size layout notes: headline text, visual focal point, CTA, logo placement.
3. A build checklist: file names, weights, clickTag setup, static backups.
4. Policy QA: flag fake UI, misleading claims, or restricted-content risks.
```

## Edge Cases & Guardrails

- Never deliver one master size and hope platforms crop — 320x50 and 160x600 are complete
  redesigns; cropped banners fail legibility and CTR.
- HTML5 lifts engagement but adds weight, QA cost, and publisher rejection risk — static
  backups are mandatory, not optional.
- Fake interactivity (cursor graphics, close buttons, fake system alerts) breaches ad
  policy and destroys trust; reject at QA, not after disapproval.
- A CTR spike in week one is novelty, not performance — judge concepts after 1–2 weeks of
  serving.
- Legibility beats cleverness: at 320x50 aim for a 5-word headline maximum and one CTA;
  text-heavy banners are invisible at real scale.
- Do not recycle 1:1 social assets as display creative — IAB sizes, aspect ratios, and
  reading contexts differ fundamentally.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CTR by creative | 0.3–0.7% channel average | <0.15% after 2 weeks of serving |
| CTR lift, new vs incumbent creative | +15–25% | <5% lift across a full refresh |
| First-submission approval rate | 100% policy-clean | Repeated disapprovals for the same reason |
| File-weight compliance | 100% within limits | HTML5 above 150 KB on GDN |
| Creative refresh cadence | Every 3–4 weeks | Same asset running 90+ days |

## Handoffs

- → **display-programmatic-buying:** deliver the named creative pack for line-item
  attachment; flag which concepts are HTML5 vs static for publisher compatibility.
- → **display-viewability-optimization:** fix contrast/legibility issues flagged in-view;
  coordinate vertical formats for vertical slots.
- → **display-performance-reporting:** register creative IDs so CTR history attributes
  per concept across refreshes.
- ↑ **display-advertising-agent:** escalate when CTR ceilings persist across two full
  refresh cycles — the problem may be offer, audience, or placement, not design.
