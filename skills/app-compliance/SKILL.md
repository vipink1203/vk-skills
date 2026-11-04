---
name: app-compliance
description: Legal and trust gates every app must pass before real users - privacy, consent and trackers, terms, payments and subscriptions, marketing claims and email, accessibility, licenses, user uploads, AI labelling. Use before any app launches, and whenever a change touches personal data, cookies or SDKs, signup, payments, emails, marketing copy, dependencies or assets, or AI features.
---

# App compliance

Every app passes these **gates** before it reaches real users, and keeps passing them as it changes.
A gate is one obligation with a rule, what to build, and a **done when** check.
Each gate's status lands in the project's compliance record, so nothing passes on memory or good intentions.

This is engineering against researched law, not legal advice.
The rules come from the sourced notes in [`research/`](research/), dated 2026-10-31: [01 privacy and consent](research/01-app-privacy-and-consent.md), [02 commerce and claims](research/02-app-commerce-and-claims.md), and [03 accessibility, IP and AI](research/03-app-accessibility-ip-and-ai.md).
When a note is more than 6 months old at run time, re-check the primary sources cited in the sections you are relying on (with a research skill, if you have one) before treating its dates and thresholds as current.

## Principles

- **One build for everyone.** Build to the strictest common standard (GDPR for privacy, California for subscriptions and pricing, WCAG 2.2 AA for accessibility) for every user, instead of branching by country.
- **The data map is the truth.** Legal pages, consent prompts and the vendor list describe what the code and the live app actually do, found by reading code and capturing traffic, never what a template assumes.
  When the app changes, the pages change in the same commit.
- **Evidence or nothing.** Every claim, badge, logo, review and number in the app points to an evidence entry in the record.
- **Owner decides, agent drafts.** The agent writes pages, code and tests; signatures, registrations, permissions and legal judgment are owner actions, and the agent never marks one done on the owner's behalf.

## Steps

1. **Map the data.** Build the data map in the compliance record from the code and a live run: every form field and API input with personal data, every database column or store holding it, every cookie and `localStorage`/`sessionStorage`/IndexedDB key, every domain the app calls (capture a Playwright HAR of every route, and a proxy capture such as mitmproxy of a fresh mobile install), every SDK in the dependency tree, and every email the app sends.
   For each item: purpose, lawful basis, where it is stored, retention period, and which vendor receives it.
   Done when the code search and the HAR show nothing absent from the map.
2. **Set scope.** Answer in the record: Who are the users (consumers, businesses, children possible)? Where (US, EU/UK, elsewhere)? How big is the business (staff, turnover)? Does it take payments or subscriptions? Send marketing email? Store content users provide (posts, comments, files, profiles, avatars)? Show AI output or an AI chat? Handle health, financial, biometric or precise location data?
   A sensitive-data or children "yes" adds a lawyer review to the owner actions.
3. **Walk every gate.** Read each gate file below and give every gate one status: `pass`, `fail`, `n/a` (with the scope answer that rules it out), or `owner` (waiting on an owner action).
   - [`gates/privacy.md`](gates/privacy.md): privacy notice, minimisation, retention, access and deletion requests, children, AI training on user data, vendors, DPAs and subprocessors (PRIV).
   - [`gates/consent-and-tracking.md`](gates/consent-and-tracking.md): cookie banner, blocking trackers before consent, opt-out signals, separate marketing consent (CONSENT).
   - [`gates/terms-and-payments.md`](gates/terms-and-payments.md): terms acceptance and its record, full prices, refunds, auto-renewal, cancellation, EU withdrawal (TERMS, PAY).
   - [`gates/marketing-and-claims.md`](gates/marketing-and-claims.md): claims, security badges, reviews, logos, uptime, urgency, dark patterns, business details, marketing email (CLAIM, UX, BIZ, EMAIL).
   - [`gates/accessibility.md`](gates/accessibility.md): WCAG 2.2 AA scan, contrast, alt text, keyboard, focus, timing and targets, EU accessibility statement (A11Y).
   - [`gates/licenses-and-content.md`](gates/licenses-and-content.md): code, font, image and icon licenses, reporting and taking down user content (LIC, UGC).
   - [`gates/ai.md`](gates/ai.md): AI chat disclosure, labelling and marking generated content (AI).
4. **Fix and prove.** Build what each `fail` needs, then run its done-when check: automated checks as tests in the project's suite so they keep running, manual checks recorded with date and result.
   Done when every gate is `pass`, `n/a` or `owner`, with no `fail` left.
5. **Hand over.** Write the owner actions list at the top of the record and tell the owner in the session, one line each: what to do, why, and where.

On a later change, repeat steps 1 and 3 to 5 for the gate files the change touches, and update the record in the same commit.

## The compliance record

Each app keeps one record at `docs/compliance.md` in its repository, updated in place, built from [`record-template.md`](record-template.md).
It holds the scope answers, the data map, every gate's status and proof, the evidence entries, the asset register, and the owner actions.
An app launches only when its record shows no `fail` and the owner has cleared or explicitly accepted each open owner action.
