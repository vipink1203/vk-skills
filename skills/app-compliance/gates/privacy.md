# Privacy gates

What we collect, why, for how long, who else gets it, and how people see, correct or delete it.
Every gate here reads from the data map built in step 1 of the skill.
Evidence: [`research/01-app-privacy-and-consent.md`](../research/01-app-privacy-and-consent.md) sections 1, 2 and 5 to 10.

GDPR reaches any app offering services to people in the EU, CalOPPA requires a posted policy from any operator collecting data from Californians regardless of size, and CCPA covers even small apps that share data of 100,000+ Californians through ad pixels.
So every app gets every gate here.

## PRIV-1 Privacy policy matches the data map

- **Rule:** GDPR Art 13 lists the notice contents: controller identity and contact, purposes and legal basis for each, legitimate interests relied on, recipients, international transfers and their safeguard, retention per category, the user's rights (access, rectification, erasure, restriction, objection, portability, withdrawing consent, complaining to a regulator), whether data is required and why, and any automated decision-making.
  The UK adds, from 19 June 2026, the right to complain to the controller, which must accept complaints (for example through a form) and acknowledge them within 30 days.
  CCPA (11 CCR 7011) adds the statutory category names, sources, whether each category is sold or shared, whether we knowingly sell or share data of under-16s, the request and verification process, authorised agents, how opt-out preference signals are handled, a "last updated" date, and an update at least every 12 months.
  CalOPPA adds how the app responds to Do Not Track and whether other parties collect cross-site data.
  A privacy policy is a notice: users are informed, never asked to accept it.
- **Build:** A `/legal/privacy` page, printable, versioned with a "Last updated" date, generated from the data map and vendor register so policy and code cannot drift.
  Linked from the footer of every page with a link containing the word "privacy", from signup, from app settings, and from the app store listing.
  Just-in-time notices beside each collection point (signup, forms, permission prompts) that deep-link to the matching policy section, not the top of the page.
  Signup copy: "See how we use your data in our [Privacy Policy]", never a checkbox to accept it.
  A privacy contact address and a complaint form whose submissions get an automatic acknowledgment (the UK requires acknowledgment within 30 days).
- **Done when:** every data map row and every vendor appears in the policy with purpose, basis, retention and recipients; the policy has a section for each item in the rule above; every collection point has a just-in-time notice; the policy date is less than 12 months old; a test complaint gets its acknowledgment; and whether the app needs an EU/UK Art 27 representative is recorded as an owner question.

## PRIV-2 Collect only what is needed

- **Rule:** Personal data must be limited to what each purpose needs (GDPR Art 5(1)(c), Art 25(2)); CCPA requires collection to be reasonably necessary and proportionate to the disclosed purpose.
- **Build:** Every form field, API input, database column, log field and analytics property with personal data maps to a feature that reads it.
  Remove fields no feature reads, make optional what the feature can do without, and keep personal data out of logs, URLs and analytics events.
  Session replay and analytics tools have automatic form and URL capture turned off.
- **Done when:** a schema and form review against the data map finds no personal data field without a purpose and a reading feature.

## PRIV-3 Retention limits are enforced in code

- **Rule:** Data is kept no longer than necessary (GDPR Art 5(1)(e)), and the retention period per category is disclosed (GDPR Art 13(2)(a), CCPA 1798.100(a)(3)).
  The FTC charged Blackbaud (2024) with keeping data far longer than necessary and ordered a retention schedule.
- **Build:** A retention table in code: per data category, the period, the deletion job, and any legal hold.
  Scheduled jobs purge expired rows, logs, analytics events and backups past their window.
  The same table renders into the privacy policy.
  Our house defaults, a choice rather than a legal number, unless a purpose needs longer: deleted accounts purged within 30 days, server logs kept 30 days, analytics events kept 25 months at most (CNIL's ceiling for exempt audience measurement).
  Consent and acceptance records follow TERMS-2.
- **Done when:** every data map row has a retention period, every period has a scheduled job, and a test with a fixed clock shows the job deleting an expired row.

## PRIV-4 People can see, export, correct and delete their data

- **Rule:** GDPR: answer access, rectification, erasure and portability requests free, within one month (extendable by two with notice), in electronic form for electronic requests, and tell recipients about erasures.
  CCPA: confirm receipt within 10 business days and answer within 45 calendar days, counting verification time; exclusively online businesses with a direct consumer relationship may offer just an email address; re-authenticate account holders before disclosing, correcting or deleting; for people without an account, match two data points (three plus a signed declaration for specific pieces); deletion reaches service providers and third parties, and backups may wait until restored or next accessed.
  Apple requires in-app account deletion; Google Play requires in-app deletion and a web deletion link.
- **Build:** In settings, each behind re-authentication: "Download my data" (JSON or CSV of everything we hold about the user), editable profile fields plus a "Request a correction" form for data the user cannot edit, and "Delete my account" (confirm, then hard delete or deidentify, and send deletion requests to every vendor in the register).
  A public web form for people without an account, also used as the app store deletion link, with the data-point verification above.
  A request ledger: received date, receipt confirmation date, verification state, deadline (the shorter of one month and 45 days), vendor deletion confirmations, outcome.
  Backups age out on their own retention window, and a restore re-applies pending deletions.
- **Done when:** end-to-end tests cover each path: export (after re-authentication) contains every data map field for a seeded user; a correction request lands in the ledger; deletion leaves no row for the user in any live store after the purge job, and every vendor deletion request is recorded as sent; and a request through the public form is confirmed and lands in the ledger.

## PRIV-5 Children

- **Rule:** COPPA (amended rule binding since 22 April 2026) covers apps directed to under-13s and general-audience apps with actual knowledge of an under-13 user; it requires verifiable parental consent before collection, separate consent for third-party disclosure, a written security program and a published retention policy.
  GDPR Art 8 requires parental consent for under-16s (member states may set 13 to 16; the UK sets 13) where consent is the basis.
  The UK Age Appropriate Design Code applies to services likely to be accessed by under-18s.
- **Build:** For a general-audience app: the terms say the service is not for children under 13 (under 16 where EU parental-consent flows are unwanted); a neutral date-of-birth screen at signup that does not default to an adult age, does not hint at the cutoff, and blocks under-age signups with a cookie to prevent immediate retry, storing no entered birthdate beyond the decision; any account found to belong to an under-13 is deleted promptly.
  An app directed at children, or likely to be used by them, stops here: it needs a parental-consent design and lawyer review before any build.
- **Done when:** the age screen passes those rules in a test and the deletion path for discovered under-13 accounts exists; or the scope marks the app directed at children and an owner action for legal review is open.

## PRIV-6 User data does not train AI without opt-in

- **Rule:** The FTC warns that quietly widening terms or the privacy policy to allow AI training can be unfair or deceptive, and that no-training promises must be kept wherever made (FTC, Jan and Feb 2024).
  The EDPB says a mention in the privacy policy does not make training reasonably expected (Opinion 28/2024); California requires separate consent for unexpected uses.
- **Build:** Default: user content is never used to train or fine-tune models, ours or a vendor's.
  Calling an LLM API to serve the user is processing for the service, under a vendor DPA or API terms that exclude training on our data; record that clause in the vendor register.
  Training, if ever wanted: a separate unticked opt-in in settings, explained in plain words, recorded, revocable, and applied only to data created after opt-in, plus an owner question on whether a CCPA risk assessment is needed (required when training automated decision-making technology for significant decisions, or facial recognition, emotion recognition or identity verification technology).
- **Done when:** the policy states the no-training default, every AI vendor's no-training term is in the vendor register, and no training pipeline reads user data without an opt-in check.

## PRIV-7 Vendors have contracts and are listed publicly

- **Rule:** GDPR Art 28 requires a processing agreement with every processor and lets processors add subprocessors only with authorisation and notice, which is why services publish subprocessor lists.
  CCPA 11 CCR 7051 requires service-provider contract terms; without them, a disclosure may count as a sale or share.
  The EU-US Data Privacy Framework was upheld in September 2025 but an appeal was pending in mid-2026, so check its status before relying on it instead of standard contractual clauses.
- **Build:** A vendor register in the compliance record with every vendor that receives personal data: role (processor or independent controller), purpose, data categories, region, transfer mechanism, DPA link and status, CCPA service-provider terms, no-training term, subprocessor list URL, and whether we subscribed to its change notices.
  The agent fills the register and finds each DPA; the owner accepts or signs each one.
  A public `/legal/subprocessors` page listing each vendor, purpose and region, with its update date and a way to subscribe to changes.
  If we act as a processor for business customers: a notice-and-object process before adding a subprocessor.
- **Done when:** every third-party domain in the HAR and every SDK in the dependency tree is in the register; every processor row has an owner-confirmed DPA and CCPA terms; every independent-controller row records why no DPA applies; and the public page matches the register.

## PRIV-8 Sensitive data gets extra protection

- **Rule:** GoodRx (2023) was the FTC's first Health Breach Notification Rule action, for sharing health data with ad platforms; BetterHelp paid $7.8M for sharing health questionnaire data for ads; the rule covers health apps outside HIPAA.
  Washington's My Health My Data Act has no size threshold, covers health data inferred from other data, needs a separate health data policy, consent to collect, separate consent to share, a signed authorisation to sell, deletion reaching backups within six months, and allows private lawsuits.
  CCPA requires a risk assessment before selling or sharing personal information or processing sensitive personal information.
  Hashing an email before sending it to an ad platform does not anonymise it.
- **Build:** No ad, social or session-replay scripts on any page or screen that shows or collects health, financial, children's, biometric or precise location data, including in URLs, page titles and form fields.
  Any app handling these categories opens an owner action for lawyer review before launch, covering the Washington and CCPA duties above.
- **Done when:** the HAR of every sensitive screen shows no third-party analytics, ad or replay request; or the scope records that the app handles no sensitive data.
