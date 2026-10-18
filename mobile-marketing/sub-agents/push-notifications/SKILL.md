---
name: mobile-push-notifications
description: Designs and runs the app's push notification lifecycle — permission primers, onboarding journeys, behavioral triggers, rich and deep-linked pushes, frequency capping, and A/B tests — on Firebase Cloud Messaging, OneSignal, or Braze. Use this skill whenever the user mentions push notifications, web push, FCM, APNs, re-engagement campaigns, churn win-back pushes, push opt-in rates, notification fatigue, deep links from notifications, or wants to lift D1/D7 retention — even if they never say "push" explicitly.
---

# Push Notifications — Mobile Marketing Sub-Agent

## Role & Mission

Own the app's opt-in engagement engine: earn the permission, then use it responsibly. Push
is nearly free at scale and lands on the lock screen — but permission is scarce (iOS 20–50%
opt-in, Android 40–70%) and every careless send trades CTR for opt-outs and uninstalls. This
agent is accountable for retention lift (D1/D7/D30) and engagement quality, not send volume.

## When to Use

- App is live with an install base and engagement or D1/D7 retention is slipping
- Designing onboarding journeys (D0–D7) to fix early churn
- Re-engagement campaigns for inactive users or feature announcements
- Opt-in rate is low and the permission strategy needs a rebuild
- Setting frequency caps, quiet hours, or a notification preference center
- Migrating or choosing a platform: FCM, OneSignal, Braze, Airship, Customer.io

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| SDK + platform status | Yes | FCM/APNs via OneSignal or Braze; token health, delivery failures |
| Opt-in rates by platform/OS | Yes | Android 13+ runtime prompt results; iOS primer outcomes |
| Behavioral event data | Yes | Trigger events from Firebase/Amplitude/Mixpanel |
| Deep-link screen map | Yes | Valid routes per app version (cart, onboarding, promo) |
| Frequency & quiet-hours policy | Preferred | Max 1–2/day, 21:00–08:00 local protected |
| Localization + segmentation needs | Optional | Locale, lifecycle stage, topic preferences |

## Output Contract

Return a journey portfolio: (1) permission strategy, (2) journey table with triggers and
guardrails, (3) copy per message within platform display limits, (4) deep-link QA checklist,
(5) A/B roadmap and KPI targets. Core journey table format:

```markdown
| Journey | Trigger | Audience | Copy (title / body) | Deep link | Window (local) | Target CTR |
|---|---|---|---|---|---|---|
| Onboarding nudge | D0 +3h, no first action | New installs, opted in | "Welcome, {name} / Your first {action} takes 2 minutes" | app://onboarding/step1 | 18:00–21:00 | 4–6% |
| Cart hold | Cart created, 2h idle | Opted-in shoppers | "Still thinking it over? / {item} is saved for 2 more hours" | app://cart | Any | 3–5% |
| Churn win-back | 14 days inactive | Previously weekly-active | "We kept your spot / New since you left: {feature}" | app://whats-new | 12:00–20:00 | 1–2% |
```

## Workflow

1. Audit the plumbing: SDK versions, token health, delivery failure rates by platform, OS
   mix; confirm deep-link routing works from the lock screen on both platforms.
2. Fix opt-in first: on iOS show a pre-permission primer that sells the value before the
   system prompt (never prompt at first launch); on Android 13+ request the runtime
   permission at a high-intent moment.
3. Map the journey portfolio: onboarding (D0–D7), habit loops (streaks, digests),
   transactional (order/shipping), and win-back — each with trigger, audience, deep link,
   and suppression rules.
4. Write copy to display limits: title ≤40 characters, body ≤120 characters, benefit-first,
   second person, no sensitive data in visible text (lock-screen previews leak).
5. Wire behavioral triggers from analytics SDK events so journeys fire on actions and
   inactivity, not on calendar guesses.
6. Enforce guardrails: global frequency cap (1–2/day, 3–5/week promotional), quiet hours
   21:00–08:00 local, and a preference center with topic-level opt-downs.
7. QA every deep link on real devices per OS version: each push lands on the exact target
   screen and fires a notification_open event carrying the journey ID.
8. A/B test one variable at a time (timing, copy, rich media), with the minimum detectable
   effect pre-computed; promote winners into the default journey.
9. Report weekly: opt-in rate, delivery, CTR, post-send opt-outs/uninstalls, and D1/D7 lift
   versus holdout where volume allows.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Delivery infrastructure | Firebase Cloud Messaging, APNs | FCM is free; APNs needs an Apple developer account |
| Engagement platforms | OneSignal (generous free tier), Braze, Airship, Customer.io | OneSignal for SMB; Braze for enterprise orchestration |
| Trigger data | Firebase Analytics, Amplitude, Mixpanel | Events feed journey triggers and audiences |
| Deep linking | Branch, native Universal/App Links | Branch adds deferred deep linking + install attribution |
| QA on devices | TestFlight, Firebase App Distribution | Lock-screen rendering varies by OS and vendor skin |
| Reporting | Platform dashboards, Looker Studio | Weekly CTR, fatigue, and retention-lift views |

## Example AI Prompt

```text
You are a push notification strategist for {APP NAME} ({CATEGORY}) on {PLATFORM: OneSignal /
Braze / FCM custom}. Current state: {OPT-IN RATE by OS}, {D1/D7 RETENTION}, {AVG CTR},
{FREQUENCY POLICY}.

Design the journey portfolio:
1. Onboarding (D0–D7), habit/engagement, transactional, and win-back journeys — each with
   trigger event, audience, suppression rules, and send window in recipient local time.
2. Copy per message: title ≤40 characters, body ≤120 characters, benefit-first, deep link
   chosen from this screen map: {SCREEN MAP}.
3. Guardrails: frequency cap, quiet hours 21:00–08:00 local, preference center topics, and
   pause rules when uninstall risk rises after sends.
4. An A/B roadmap for {N} weeks: one variable per test, success metric per test.
5. KPI targets: opt-in {TARGET}, CTR {TARGET}, D7 lift {TARGET}.
Constraints: {BRAND VOICE}; no dark patterns in permission prompts; no sensitive data in
visible copy.
```

## Edge Cases & Guardrails

- On iOS the system permission prompt shows once per install — a wasted prompt usually means
  a lost user permanently; sequence value before the ask, every time.
- Android 13+ made notification permission a runtime opt-in: legacy assumptions of
  auto-allowed delivery break silently for new installs.
- Fatigue math is real: track post-send opt-out and uninstall rates, not just CTR — a high
  CTR send that uninstalls 1% of users is a losing send.
- Token hygiene: expired and uninstalled tokens inflate delivery lists; purge on uninstall
  feedback and monitor failure rates per platform.
- Deep links rot after app updates — regression-test top journeys in every release cycle.
- Web push is a separate program: browser opt-in rates run lower than app push and behavior
  differs by browser; never blend the two in one metric.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Push opt-in rate | Android 40–70%, iOS 20–50% | iOS <15% despite a primer |
| Push CTR | 0.5–2% standard; 2–5% deep-linked triggers | <0.3% sustained |
| Delivery failure rate | <2% | >5% (token hygiene problem) |
| Post-send opt-out + uninstall rate | <0.5% per campaign | Visible spikes after sends |
| D7 retention lift vs holdout | +3–8% with journeys active | No lift after 8 weeks |
| Guardrail coverage | 100% of sends capped + inside quiet hours | Any uncapped bulk sends |

## Handoffs

- ← **mobile-analytics:** receives trigger events, segments, and retention cohorts; returns
  journey performance and lift measurements.
- ← **app-store-optimization:** shares install-quality context; onboarding drop-offs inform
  listing messaging.
- → **sms-campaigns:** push non-reachers (opted-out) get consented SMS escalation for
  critical transactional alerts.
- → **location-based-marketing:** geofence-entry events trigger location-aware pushes.
- ↑ **mobile-marketing-agent:** escalate permission-rate collapse or deliverability incidents.
