# Consent and tracking gates

Cookies, pixels, SDKs, browser storage, opt-out signals, and every consent we ask for.
Evidence: [`research/01-app-privacy-and-consent.md`](../research/01-app-privacy-and-consent.md) sections 2 to 4 and 11.

EU consent rules cover any storing or reading on a device, not only cookies: pixels, SDKs, `localStorage`, IP-based tracking and fingerprinting (EDPB Guidelines 2/2023).
Legitimate interest is never a basis for them.
One build for everyone: EU-grade consent plus Global Privacy Control handling for every visitor.

## CONSENT-1 The consent banner offers a real choice

- **Rule:** No consent-requiring storage before a positive action; "Reject all" on the same layer as "Accept all"; withdrawing as easy as giving; scrolling, closing the banner or continuing to browse is never consent; cookie walls do not produce valid consent (EDPB taskforce report and Guidelines 05/2020).
  California requires symmetry: "Accept all" with only "Preferences" beside it, or a more prominent "Yes", is a dark pattern, and agreement obtained through one is not consent (11 CCR 7004).
  The information must include each cookie's purpose, duration and whether third parties can read it (Planet49).
- **Build:** Shown only when the app uses anything beyond strictly necessary storage.
  First layer: "Accept all" and "Reject all" buttons identical in size, weight, color and contrast, plus "Settings" with unticked, clearly labelled category toggles ("Analytics: Off").
  A persistent "Privacy choices" link in the footer and settings reopens it.
  A cookie table on the privacy policy listing each cookie and storage key: name, purpose, category, duration, third-party access.
  Consent record per choice: categories, banner version, region, timestamp.
  Withdrawing a category unloads its scripts and deletes its cookies and storage keys, without waiting for a reload.
  No re-prompt in the session after a refusal.
  The banner does not cover focused elements (A11Y-4) and is fully keyboard operable.
- **Done when:** a test asserts the two buttons have equal computed font size, weight, padding, and color contrast; "Reject all" takes as many clicks as "Accept all"; the stored choice survives reload; and withdrawing analytics through the reopen link removes its cookies and stops its requests.

## CONSENT-2 Nothing tracks before consent

- **Rule:** Only storage strictly necessary for a service the user asked for (session, security, load balancing, the consent choice itself, cart) is exempt.
  Mislabelling analytics or marketing as "essential" is a listed bad practice.
  The rule covers first-party and proxied tracking and fingerprinting too, not only third-party cookies.
  Analytics exemptions exist only nationally and under conditions (France's CNIL audience-measurement exemption; the UK's first-party statistics exception since 5 February 2026): single publisher, anonymous statistics only, no cross-site use, clear information, and a simple free way to object.
- **Build:** Every non-exempt script, pixel, SDK, server-side tracking call and storage write is gated in code on the stored consent category, not hidden with CSS and not loaded then paused.
  Analytics goes behind consent by default; relying on a national analytics exemption is an owner decision recorded with how each condition is met, including the objection control.
  Mobile SDKs initialise only after consent.
- **Done when:** in a fresh profile, without touching the banner, a Playwright HAR of every route in the data map shows every request going only to our own non-tracking endpoints or to a vendor whose register row says no consent is needed (our own analytics or tracking endpoints count as needing consent), and no cookie or storage key outside the strictly necessary rows of the cookie table; the same run after "Accept all" shows the expected extras, and after "Reject all" in a new profile shows none.
  Mobile builds pass the same check through a proxy capture (for example mitmproxy) of a fresh install.

## CONSENT-3 Each consent is separate and recorded

- **Rule:** Marketing email needs prior opt-in consent in the EU/UK, except the soft opt-in for existing customers' similar products with an opt-out at collection and in every message (ePrivacy Art 13, PECR reg 22).
  Consent must be separate from the terms, granular per purpose, never pre-ticked, provable, and as easy to withdraw as to give (GDPR Art 7, Planet49).
- **Build:** Signup shows each consent-based purpose as its own unticked checkbox, apart from the TERMS-1 control: "Email me product news and offers" and any other (for example an AI training opt-in, PRIV-6).
  For soft opt-in at checkout, a visible "Don't send me offers" box instead.
  Each grant and withdrawal is a `consent_events` row with the purpose, the exact text shown, timestamp and source.
  Settings show every consent with a toggle to withdraw.
- **Done when:** a test signs up without ticking the marketing box and the user is excluded from marketing sends; a test ticks it and a consent row with the shown text exists; withdrawing in settings takes effect on the next send.

## CONSENT-4 Opt-out signals are honoured

- **Rule:** CCPA: a business that sells or shares personal information (ad pixels for cross-context advertising count as sharing) must post a "Do Not Sell or Share My Personal Information" link and must honour opt-out preference signals such as Global Privacy Control, showing whether it did ("Opt-Out Request Honored").
  A cookie banner alone is not a valid CCPA opt-out; opt-outs cannot require an account or ID; an opted-out user may not be asked to opt back in for 12 months.
- **Build:** Preferred: no selling or sharing at all, so no ad pixels, and the policy says so.
  Either way, read `Sec-GPC: 1` on the server and `navigator.globalPrivacyControl` in the client; when set, treat the browser and any signed-in account as opted out of sale, sharing and targeted advertising, and show "Opt-out request honored" in the privacy choices panel.
  If anything is sold or shared: the "Do Not Sell or Share" link in the footer, leading straight to the control, effective without sign-in, with the opt-out date stored so no opt-in prompt appears for 12 months; and an owner action for the CCPA risk assessment required before selling or sharing, when CCPA applies.
- **Done when:** a test with GPC enabled loads the app and sees no sale or sharing requests and the "honored" message; and either the policy states no selling or sharing (matching the HAR) or the footer link works signed out.
