# Marketing and claims gates

Everything the app says to sell itself: claims, badges, reviews, logos, urgency, uptime, who we are, and marketing email.
Evidence: [`research/02-app-commerce-and-claims.md`](../research/02-app-commerce-and-claims.md) sections 5 to 12.

The leading word here is **evidence**: every claim the app makes points to a dated evidence entry in the compliance record that supports it at the level the claim states, or it is removed or rewritten as a qualitative statement that is true on its face.

## CLAIM-1 Every claim has evidence

- **Rule:** The FTC requires a reasonable basis before a claim runs, and at least the level of support the claim states ("tests prove").
  There is no AI exemption: unsupported accuracy or capability claims for AI features have drawn FTC orders (DoNotPay, Workado).
  Health claims need competent and reliable scientific evidence.
  From 27 September 2026 EU member states must ban generic environmental claims without recognised excellent environmental performance.
  "Made in USA" has its own rule for physical goods.
- **Build:** Search all user-facing copy (pages, app store listing, emails, metadata) for numbers, percentages, superlatives ("fastest", "#1", "best"), "AI-powered", accuracy, savings, health, environmental and origin claims, and review every image and video for claims in their text.
  Each one gets an evidence entry in the compliance record: the claim, the evidence file or measurement, what level of support it gives, the date, and a re-check date.
- **Done when:** every claim found has an evidence entry whose support matches the claim's wording (a "tested" claim has a test), and every claim without one is removed or rewritten.

## CLAIM-2 Security and compliance claims are exact

- **Rule:** SOC 2 is a CPA's attestation report, not a certification; "HIPAA certified" and "GDPR certified" do not exist; the FTC has acted against false HIPAA, Privacy Shield and encryption claims (Verkada, Monument, Zoom), including lapsed participation still advertised; displaying a trust mark without authorisation is always unfair in the EU.
- **Build:** Use only wording backed by a current document:
  completed SOC 2 Type II: "SOC 2 Type II report available on request under NDA";
  audit underway with a signed engagement letter: "SOC 2 Type II audit in progress";
  hosted on a certified cloud: "Hosted on {provider}, which holds {certification}";
  EU-US transfers: "Self-certified to the EU-U.S. Data Privacy Framework" only while listed and current;
  otherwise, describe actual controls ("Data encrypted at rest with AES-256 via {provider}").
  No SOC 2, ISO 27001, HIPAA or GDPR badges, and no "certified" or "compliant" for any of them.
- **Done when:** a case-insensitive search for `SOC ?2|ISO ?27001|HIPAA|GDPR|Privacy Shield|Data Privacy Framework|certified|compliant|bank-grade|military-grade|end-to-end` across marketing copy, app UI and store listings (legal pages that describe our obligations factually are reviewed separately, by hand) finds only wording from the list above, each with an evidence entry and re-check date; and no image contains a certification badge.

## CLAIM-3 Reviews and testimonials are real

- **Rule:** The FTC Consumer Reviews and Testimonials Rule (16 CFR 465, in force since 21 October 2024; up to $53,088 per violation) bans fake or AI-generated reviews, sentiment-conditioned incentives, undisclosed insider reviews, review suppression, and bought followers or views.
  Testimonials about key results imply typical results, and "results not typical" does not cure that: disclose what users can generally expect.
  The EU requires disclosing how reviews are verified; California needs prior consent to use a person's name or photo in ads.
- **Build:** Show only reviews tied to a verified account or order.
  Label incentivised and employee reviews.
  Moderate positive and negative reviews by the same neutral rules.
  Store written consent for every named or pictured testimonial, and pair results testimonials with the generally expected result.
  For EU users, a "How we verify reviews" note beside reviews.
  The agent writes no placeholder testimonials, star ratings or user counts into shipped UI.
- **Done when:** every review or testimonial on screen traces to a stored source record (and consent for named people), and placeholder social proof is absent from the production build.

## CLAIM-4 Customer logos have permission

- **Rule:** Showing a company's logo implies its endorsement; false association is actionable under the Lanham Act (15 USC 1125(a)).
  No statute demands written permission, but written permission is the practical defence and many customer contracts require it.
- **Build:** A logo appears only for a current customer who gave written permission (email is fine), stored with date and scope.
  Our house rule: remove a logo within 30 days of the customer leaving or revoking permission.
  "Trusted by" numbers are true and dated ("Used by 1,200 teams as of Oct 2026").
  No logos of trial users, investors, partners or press presented as customers.
- **Done when:** every logo on the site maps to a permission entry for a current customer in the compliance record, and every count is dated.

## CLAIM-5 Uptime promises are measured

- **Rule:** No statute requires an uptime promise, but a promise you miss or cannot back is deception.
- **Build:** No uptime number in marketing unless a public status page shows measured history covering the claimed period.
  Never promise more than the dependencies' own SLAs combined allow.
  A sold SLA lives in the contract with the definition of unavailable, the measurement source, exclusions, credit tiers and the claim deadline.
- **Done when:** every availability figure in copy links to a status page with matching history, or no figure appears.

## UX-1 Urgency and scarcity are true

- **Rule:** Falsely claiming an offer is available only for a very limited time is always unfair in the EU (UCPD Annex I item 7) and banned in the UK (DMCC Act Sch 20 para 7).
  The FTC's 2022 staff report lists baseless countdown timers and false low-stock or high-demand messages as dark patterns judged under FTC Act Section 5 deception (no FTC case built solely on a timer was found).
  A timer that ends a user's task must also meet WCAG 2.2.1 (see A11Y-4).
- **Build:** A countdown shows only a real deadline stored server-side; at zero the offer ends for everyone and never restarts per visit or session.
  Stock and demand messages come only from live data.
- **Done when:** a test that reloads the page and starts a fresh session sees the same deadline, the offer is unavailable after it passes, and every stock or demand message reads from a live source.

## UX-2 No dark patterns

- **Rule:** Deceptive interface design is policed under FTC Act Section 5, the EU UCPD and, for online platforms, DSA Article 25; privacy and consent choices also have their own symmetry rules (CONSENT-1).
- **Build:** No preselected paid add-ons or opt-ins, no confirmshaming copy ("No thanks, I like paying more"), no hidden costs, no extra steps to cancel or decline compared to accepting, no disguised ads, no nagging repeat prompts after a decline.
- **Done when:** a walkthrough of signup, checkout, upgrade, cancel and every consent prompt, recorded with date, finds each choice presented with equal prominence and the same number of steps for yes and no.

## BIZ-1 Business contact details are published

- **Rule:** The EU E-Commerce Directive (Art 5), UK reg 6 and Germany's Impressum (§ 5 DDG, fines up to EUR 50,000) require name, geographic address, email and other contact details, register number and VAT ID where they exist; EU consumer contracts also need a telephone number.
  CAN-SPAM needs a valid postal address in every commercial email.
  Cite § 5 DDG, not the replaced § 5 TMG; the EU ODR platform link requirement ended on 20 July 2025.
- **Build:** One `/legal/imprint` page linked from every page footer and the app's settings: legal entity name and form, registered address, email, phone, representative, register number, VAT ID.
  Email footers and receipts reuse the same data.
  Use a registered business address or virtual office unless the owner chooses a home address.
- **Done when:** the page is reachable in one click from every page and from settings, and its data matches the email footer template.

## EMAIL-1 Marketing email can be unsubscribed

- **Rule:** CAN-SPAM: accurate sender and subject, identified as an ad, postal address, an opt-out that works for at least 30 days after sending and is honoured within 10 business days, no fee or login to opt out, and opted-out addresses never sold or transferred.
  Yahoo requires bulk senders to honour unsubscribes within 2 days and Gmail recommends 48 hours; both require SPF, DKIM, DMARC, one-click unsubscribe (RFC 8058) and a spam rate below 0.3%, and Gmail has been rejecting non-compliant mail since November 2025.
  EU/UK marketing email needs prior consent (CONSENT-3) except the soft opt-in for existing customers.
- **Build:** Every marketing email carries `List-Unsubscribe: <https://...>` and `List-Unsubscribe-Post: List-Unsubscribe=One-Click`, a visible unsubscribe link that keeps working, and the postal address.
  Unsubscribes apply within 24 hours (our house rule, inside every deadline above) and go on a permanent suppression list that is never exported.
  Transactional email (receipts, password resets) stays separate from marketing and carries no marketing content.
  Sending domain has SPF, DKIM and DMARC (at least `p=none`) aligned with the From address; spam rate is watched in Google Postmaster Tools.
- **Done when:** a test marketing email has both headers, posting to the one-click URL suppresses the address, and a DNS check shows SPF, DKIM and DMARC on the sending domain.
