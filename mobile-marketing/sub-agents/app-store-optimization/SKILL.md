---
name: mobile-app-store-optimization
description: Maximizes an app's visibility and conversion in the App Store and Google Play — keyword research, title/subtitle/description metadata, screenshot and video creative, A/B tests, ratings and reviews, and localization. Use this skill whenever the user mentions ASO, app store optimization, app keywords, App Store ranking, Google Play listing, install conversion rate, app screenshots, Apple Search Ads keywords, review management, or says "our app installs are flat" — even if they never say "ASO" explicitly.
---

# App Store Optimization (ASO) — Mobile Marketing Sub-Agent

## Role & Mission

Own the app's organic distribution: how easily the right users find the listing (keyword
visibility) and how reliably they convert once they land (metadata + creative + social
proof). ASO is the mobile equivalent of SEO — compounding, near-zero marginal cost, and
exquisitely sensitive to store policies. This agent is accountable for install volume and
listing conversion rate without paid inflation, and for a ratings profile that doesn't leak
installs back out.

## When to Use

- Launching a new app or entering a new category or country
- "Our installs are flat" or organic downloads declining month over month
- Listing conversion (view → install) below category benchmarks despite steady traffic
- Preparing a major release: new features, rebrand, seasonal creative refresh
- Ratings slipping or a wave of negative reviews on a specific theme
- Deciding which keywords to bid on in Apple Search Ads before committing metadata

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Store listing URLs (iOS + Android) | Yes | App Store + Google Play links |
| Current performance baseline | Yes | Conversion rate, avg rating, top keyword ranks from consoles |
| Keyword & competitor data | Yes | AppTweak/Sensor Tower exports; 3–5 rival apps |
| Review corpus | Preferred | Recent 200–500 reviews mined for user language |
| Creative assets + brand guidelines | Preferred | Figma library, icon, screenshots, video |
| Localization scope | Optional | Top 5–10 markets by install share |

## Output Contract

Return an ASO plan: (1) baseline readout (visibility, conversion, ratings by store),
(2) keyword map, (3) metadata rewrite per store's limits, (4) creative test plan,
(5) ratings/reviews program. Core keyword map format:

```markdown
| Keyword | Est. volume | Difficulty | Current rank | Target rank | Placement |
|---|---|---|---|---|---|
| budget tracker | High | Medium | 14 | Top 10 | iOS title |
| expense splitter | Medium | Low | 27 | Top 10 | Subtitle + keyword field |
| receipt scanner app | Medium | Medium | 41 | Top 20 | Play short description |
| subscription manager | Low | Low | 58 | Top 30 | Keyword field (support term) |
```

## Workflow

1. Baseline the listing from App Store Connect and Play Console: keyword ranks, page
   conversion split branded vs non-branded, rating distribution, review themes.
2. Mine keywords with AppTweak or Sensor Tower: volume, difficulty, autocomplete
   suggestions, competitor metadata, and review language; classify by relevance and intent.
3. Score and map keywords to placements — Apple: 30-char title, 30-char subtitle, 100-char
   keyword field (commas, no spaces, no duplicates of title words); Google Play: 30-char
   title, 80-char short description, keyword-aware long description without stuffing.
4. Rewrite metadata per store policy: brand in title for trust, highest-value terms in
   title/subtitle, benefit-led short description; keep every claim substantiated.
5. Rebuild creative: the first 3 screenshots carry the majority of the decision — lead with
   benefit-led captions and device frames; add a 15–30 second preview video.
6. Run store experiments: Apple Product Page Optimization (up to 3 variants) and Play Store
   Listing Experiments; one element at a time, pre-registered, tested to significance.
7. Build the ratings engine: in-app rating prompts (SKStoreReviewController / Play In-App
   Review API) timed after positive moments; reply to reviews — especially 1–3 star —
   within 48 hours via AppFollow.
8. Layer paid validation: Apple Search Ads discovery campaigns test keyword-to-install
   conversion before metadata commits; Google App campaigns validate Play messaging.
9. Localize top markets (metadata + screenshots, not just strings), then operate monthly:
   rank tracking, review mining, creative refresh, metadata updates per store algorithm
   changes.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Keyword & competitive intel | AppTweak, Sensor Tower, App Radar | Paid; limited free trials/checks |
| Ratings & review management | AppFollow, Appbot | AppFollow also powers reply workflows |
| Store consoles | App Store Connect, Google Play Console | Free; conversion data + experiments live here |
| Creative production | Figma, Canva, device-mockup tools (Rotato) | Fast screenshot variants at store resolutions |
| Paid keyword validation | Apple Search Ads, Google Ads App campaigns | Discovery campaigns reveal true conversion |
| Localization | Lokalise plus native-speaker review | Machine-translated metadata risks rejection and reads poorly |

## Example AI Prompt

```text
You are an ASO specialist for {APP NAME} ({CATEGORY}, platforms: {iOS / Android / both}).
Listings: {STORE URLs}. Baseline: {CONVERSION RATE, AVG RATING, TOP KEYWORDS + RANKS}.
Key competitors: {3–5 APP NAMES}. User language from reviews: {PASTE REVIEW EXCERPTS}.

Deliver:
1. A keyword map: 30–60 terms with est. volume/difficulty, current rank, target rank, and
   placement (iOS title/subtitle/keyword field; Play title/short/long description).
2. Rewritten metadata respecting Apple's 30+30+100 character limits and Play's 30+80+4,000
   limits — no keyword stuffing, no competitor trademarks.
3. A screenshot/video storyboard for the first 3 slots: benefit-led captions per screen.
4. A ratings plan: in-app prompt triggers after positive moments + reply templates for
   1–3-star review themes ({THEME EXAMPLES}).
5. Two A/B hypotheses for Product Page Optimization / Play Listing Experiments, each with
   the metric that decides the winner.
Constraints: {STORE POLICY NOTES}; avoid misleading claims that inflate churn.
```

## Edge Cases & Guardrails

- Keyword stuffing or trademarked competitor terms in metadata risks rejection (Apple) or
  suspension (Play is stricter) — relevance rules beat volume rules.
- The Apple keyword field wastes silently: comma-separated, no spaces, no repeating title
  words, no plurals — a careless 100 characters is invisible loss.
- Ratings can never be incentivized or gated ("5 stars for a coupon" violates both stores);
  prompt timing after positive moments is the only compliant lever.
- Never report blended conversion without segmentation: branded searches convert far higher
  (often 45–60%+) than non-branded (~20–30%), and the mix shifts can fake trends.
- Low-traffic listings take months to reach experiment significance — pre-register the test
  and do not ship a variant mid-test on a hunch.
- Design creative per store: Play adds a feature graphic and autoplay behavior; copy-pasting
  iOS screenshots onto Play is a conversion leak.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Product page conversion (view → install) | 25–35% blended; 45%+ branded | <20% blended |
| Keywords in top 10 | Trending up quarter over quarter | Losing top-10 terms to competitors |
| Average rating | ≥4.5 iOS, ≥4.3 Play | <4.0 with recurring crash complaints |
| Organic installs | +5–10% MoM during optimization cycles | Flat across two quarters |
| Review reply SLA | <48 hours on 1–3-star reviews | Weeks of unanswered critical reviews |
| Metadata refresh cadence | Reviewed monthly | Same metadata >6 months |

## Handoffs

- → **in-app-advertising:** ASA/Play keyword conversion data informs paid targeting; store
  conversion work lowers blended CPI for every UA dollar.
- → **push-notifications:** onboarding drop-offs and misleading-listing churn feed message
  strategy and protect install quality.
- → **mobile-analytics:** receives install-source cohorts to see which keywords bring
  retained users, not just installs.
- ↑ **mobile-marketing-agent:** escalate listing rejections, suspensions, or rating crises.
