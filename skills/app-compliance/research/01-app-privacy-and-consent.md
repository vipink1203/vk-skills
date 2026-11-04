# 01 - App Privacy and Consent

Research date: 2026-10-31.
Scope: baseline privacy and consent obligations an AI coding agent must apply to every small web or mobile app we build (US owner; users in the US, EU/UK, and elsewhere).
Every claim carries an inline link to the primary source it was checked against on the research date.
Where a primary page blocked automated fetches (ICO, HHS, leginfo.legislature.ca.gov, the Council press site), the note says so and names what was read instead.
This is engineering research, not legal advice; the last section lists what needs a lawyer.

## 0. Status snapshot as of 2026-10-31

- EU GDPR text is unchanged; the "Digital Omnibus" amendments are a proposal, not law ([Council press release, 21 Oct 2026](https://www.consilium.europa.eu/en/press/press-releases/2026/10/21/digital-rulebook-council-agrees-position-to-simplify-data-protection-privacy-and-cyber-reporting-rules/); page blocked automated fetch, content read from the search index).
- The Commission proposed the omnibus on 19 November 2025, and the Council agreed its negotiating mandate on 21 October 2026; trilogues with Parliament have not concluded ([Council press release](https://www.consilium.europa.eu/en/press/press-releases/2026/10/21/digital-rulebook-council-agrees-position-to-simplify-data-protection-privacy-and-cyber-reporting-rules/)).
- The Council mandate keeps cookie rules inside the ePrivacy framework (it rejected the Commission's move into GDPR Arts 88a/88b) and adds purposes, such as audience measurement and security, where consent would not be needed ([Council press release](https://www.consilium.europa.eu/en/press/press-releases/2026/10/21/digital-rulebook-council-agrees-position-to-simplify-data-protection-privacy-and-cyber-reporting-rules/), read via search index).
- UK: the Data (Use and Access) Act 2025 (DUAA) rewrote PECR regulation 6 (cookies) with new consent exceptions, in force 5 February 2026 ([PECR reg 6, legislation.gov.uk](https://www.legislation.gov.uk/uksi/2003/2426/regulation/6)).
- UK: a new duty to handle data protection complaints (DPA 2018 s.164A) and matching privacy-notice items apply from 19 June 2026 ([DPA 2018 s.164A](https://www.legislation.gov.uk/ukpga/2018/12/section/164A)).
- UK: the Information Commission replaces the Information Commissioner (ICO) from 30 September 2026 ([DUAA 2025 Part 5](https://www.legislation.gov.uk/ukpga/2025/18/contents); [SI 2026/386, transitional provision for the first chair](https://www.legislation.gov.uk/uksi/2026/386/contents/made)); the 30 September date comes from the commencement regulations as read on the research date.
- California: the current CCPA regulations took effect 1 January 2026 and add risk assessments, cybersecurity audits, and automated decisionmaking (ADMT) rules ([CPPA regulations page](https://cppa.ca.gov/regulations/); [CCPA Regulations eff. 1/1/2026](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- California: from 1 January 2027 every browser must offer a configurable opt-out preference signal (Civ. Code 1798.136) ([CCPA statute eff. 1/1/2026](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- California: the CPPA has preliminary (not proposed) rulemakings open on opt-out preference signals, notices and disclosures, and "reducing friction" in rights requests ([CPPA regulations page](https://cppa.ca.gov/regulations/)).
- COPPA: the amended Rule took effect 23 June 2025, and full compliance was required by 22 April 2026 ([Federal Register 2025-05904](https://www.federalregister.gov/documents/2025/04/22/2025-05904/childrens-online-privacy-protection-rule)).
- COPPA: on 25 February 2026 the FTC issued an enforcement policy statement that shields general-audience operators who collect data solely for age verification under six conditions ([FTC press release](https://www.ftc.gov/news-events/news/press-releases/2026/02/ftc-issues-coppa-policy-statement-incentivize-use-age-verification-technologies-protect-children)).

## 1. Privacy policy / privacy notice

### When each regime applies

- GDPR applies to a non-EU controller that offers goods or services (paid or free) to people in the EU, or monitors their behaviour in the EU ([GDPR Art 3(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- UK GDPR has the same test for people in the UK ([UK GDPR Art 3(2)](https://www.legislation.gov.uk/eur/2016/679/article/3)).
- A non-EU controller caught by Art 3(2) must appoint an EU representative in writing, unless processing is occasional, not large-scale special-category, and unlikely to result in risk ([GDPR Art 27](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)); the UK has the same rule ([UK GDPR Art 27](https://www.legislation.gov.uk/eur/2016/679/article/27)).
- CCPA applies to a for-profit entity doing business in California that meets one of: annual gross revenue over the adjusted threshold; buys, sells, or shares personal information of 100,000+ consumers or households; or derives 50%+ of revenue from selling or sharing personal information ([Civ. Code 1798.140(d)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- The revenue threshold is $26,625,000 from 1 January 2025 (CPI-adjusted every odd-numbered year, so the next change is expected 1 January 2027) ([CPPA CPI adjustment](https://www.cppa.ca.gov/regulations/cpi_adjustment.html)).
- "Sharing" means disclosing personal information to a third party for cross-context behavioural advertising, with or without payment, so ad pixels count toward the 100,000 threshold ([Civ. Code 1798.140, "share"](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- CalOPPA has no size threshold: any operator of a commercial website or online service that collects personally identifiable information from California residents must conspicuously post a privacy policy ([Bus. & Prof. Code 22575(a), reproduced in the CA AG guide appendix](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf); leginfo blocked automated fetch).

### GDPR / UK GDPR Art 13 contents (data collected from the user)

Provide at the time the data is obtained ([GDPR Art 13(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)):

- (a) controller identity and contact details, and the EU/UK representative if any.
- (b) DPO contact details, where applicable.
- (c) purposes and the legal basis for each.
- (d) the legitimate interests pursued, where relying on Art 6(1)(f).
- (e) recipients or categories of recipients.
- (f) any third-country transfer and the adequacy decision or safeguard relied on.
- (2)(a) retention period, or the criteria used to set it.
- (2)(b) rights of access, rectification, erasure, restriction, objection, and portability.
- (2)(c) right to withdraw consent, where consent is the basis.
- (2)(d) right to complain to a supervisory authority.
- (2)(e) whether providing data is a statutory or contractual requirement and the consequences of not providing it.
- (2)(f) automated decision-making, including profiling, with meaningful information about the logic.

UK-only additions from 19 June 2026: the notice must also state the right to complain to the controller under DPA 2018 s.164A (new Art 13(2)(ca)) ([UK GDPR Art 13](https://www.legislation.gov.uk/eur/2016/679/article/13)).
UK controllers must also accept complaints, facilitate them (for example an electronic complaint form), and acknowledge them within 30 days ([DPA 2018 s.164A](https://www.legislation.gov.uk/ukpga/2018/12/section/164A)).
For data obtained from someone other than the user, Art 14 information is due within a reasonable period and at the latest one month, or at first communication, or at first disclosure ([GDPR Art 14(3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
Information must be concise, transparent, intelligible, easily accessible, and in clear and plain language ([GDPR Art 12(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
EDPB-endorsed transparency guidance says privacy information should be clearly differentiated from contractual terms and recommends a layered notice online ([WP29 Guidelines on transparency WP260 rev.01, para 8](https://ec.europa.eu/newsroom/article29/redirection/document/51025)).
Material changes (for example new recipient categories or new transfers) should be notified well in advance, explicitly and effectively, so the user can object or withdraw consent ([WP260, para 30](https://ec.europa.eu/newsroom/article29/redirection/document/51025)).

### CCPA: notice at collection (11 CCR 7012)

- Give it at or before the point of collection; if not given, the business must not collect the personal information ([11 CCR 7012(c)-(d)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Contents: categories of personal information (including sensitive), purposes, whether each category is sold or shared, retention period per category (or criteria), the "Do Not Sell or Share" link if applicable, and a link to the privacy policy ([11 CCR 7012(e)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Online, it may be a link that lands directly on the relevant section of the privacy policy; linking to the top of the policy does not satisfy the rule ([11 CCR 7012(f)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Webform placement: a conspicuous link close to the input fields or the submit button; mobile: on the download page and inside the app, for example in settings ([11 CCR 7012(c)(2)-(3)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- If you let a third party (for example an ad network) collect via your site, both you and that third party must give notice at collection ([11 CCR 7012(g)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).

### CCPA: privacy policy (11 CCR 7011)

- Post it via a conspicuous link containing the word "privacy" on the homepage or the app's download/landing page; a mobile app must also link it from its settings menu ([11 CCR 7011(d)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- It must be printable ([11 CCR 7011(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Required practices disclosure, covering the preceding 12 months: categories collected (using the statutory category names), sources, purposes, categories sold/shared and to whom, categories disclosed to service providers, whether it has actual knowledge of selling/sharing data of under-16s, and whether sensitive personal information is used beyond the permitted purposes ([11 CCR 7011(e)(1)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Required rights description: know, delete, correct, opt out of sale/sharing (if applicable), limit sensitive PI (if applicable), ADMT opt-out and access (if applicable), and non-retaliation ([11 CCR 7011(e)(2)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Required process description: request methods, verification process, how opt-out preference signals are processed, authorized agent instructions, and a contact method ([11 CCR 7011(e)(3)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- It must show the date last updated and be updated at least once every 12 months ([11 CCR 7011(e)(4)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf); [Civ. Code 1798.130(a)(5)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).

### CalOPPA contents (Bus. & Prof. Code 22575(b))

- Categories of personally identifiable information collected and categories of third parties it may be shared with ([22575(b)(1)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- The process for reviewing and requesting changes, if one exists ([22575(b)(2)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- How users are notified of material changes, and the policy's effective date ([22575(b)(3)-(4)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- How the operator responds to browser "Do Not Track" signals or similar mechanisms, if it collects data about activity over time and across third-party sites ([22575(b)(5)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- Whether other parties may collect such cross-site data when the user uses the service ([22575(b)(6)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- Violation of the posting duty occurs only if not cured within 30 days of notice ([22575(a)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf)).
- Caveat: the statute text was read from the AG's 2014 guide appendix because leginfo blocked automated access; verify no later amendment before relying on exact wording.

### App store rules (contractual, not law, but enforced at review)

- Apple requires a privacy policy link in App Store Connect and inside the app, covering data collected, third-party SDK sharing, retention/deletion, and how to revoke consent or request deletion ([App Review Guideline 5.1.1(i), last updated 16 Oct 2026](https://developer.apple.com/app-store/review/guidelines/)).

### Implementation

- One canonical privacy policy page, versioned, with a "last updated" date, linked from footer, signup screen, app settings, and store listing.
- A layered notice: short just-in-time text next to each collection point (signup, forms, permissions) that deep-links to the matching policy section (satisfies CCPA 7012(f) and WP260 layering).
- A per-category data inventory (category, purpose, legal basis, recipients, retention, sold/shared yes/no) kept in the repo and rendered into the policy, so policy and code cannot drift.

## 2. "I accept the privacy policy" checkbox: notice vs consent vs clickwrap

- A privacy policy is a notice (GDPR Arts 12-14), not a contract and not a consent request; the controller must "provide" it, and nothing in Arts 12-14 requires the user to accept it ([GDPR Arts 12-14](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Where consent is the legal basis and is requested in a declaration that also covers other matters, the consent request must be clearly distinguishable from the other matters ([GDPR Art 7(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Consent bundled as a non-negotiable part of terms and conditions is presumed not freely given ([EDPB Guidelines 05/2020 on consent, para 13](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Consent requested electronically "cannot simply be a paragraph within terms and conditions" ([EDPB 05/2020, para 71](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Consent and contract are separate legal bases that "cannot be merged and blurred" ([EDPB 05/2020, para 26](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Tying a service to consent for processing not necessary for that service makes consent presumptively invalid ([GDPR Art 7(4)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng); [EDPB 05/2020, para 13](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Processing needed to run the account is normally on Art 6(1)(b) (contract), not consent ([GDPR Art 6(1)(b)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- The ICO's direct marketing guidance gives a worked example that a customer confirming they "have read" the privacy policy is not valid marketing consent ([ICO, Plan direct marketing](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/direct-marketing-guidance/plan-direct-marketing/); ico.org.uk timed out on direct fetch, content read from the search index).
- California: acceptance of general terms of use that contain data-processing descriptions alongside unrelated information is a choice architecture that prevents valid consent ([11 CCR 7004(a)(4)(C)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Washington MHMDA: consent "may not be obtained by" acceptance of a general or broad terms of use agreement ([RCW 19.373.010](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- Terms of service are different: in the US, a "clickwrap" (an "I agree" box or button next to the terms) is routinely enforced, and an inquiry-notice contract forms only with reasonably conspicuous notice of the terms plus an action that unambiguously manifests assent ([Berman v. Freedom Financial Network, 30 F.4th 849 (9th Cir. 2022)](https://cdn.ca9.uscourts.gov/datastore/opinions/2022/04/05/20-16900.pdf)).
- In Berman, a large "continue" button with small, unclear hyperlinked terms was not assent ([Berman, slip op.](https://cdn.ca9.uscourts.gov/datastore/opinions/2022/04/05/20-16900.pdf)).

### Implementation

- Signup: one required checkbox or explicit button text for the Terms ("I agree to the Terms"), with conspicuous links, and store terms version + timestamp per user.
- Privacy policy: a plain link and sentence ("See how we use your data in our Privacy Policy"), never a required "I accept the privacy policy" checkbox.
- Every consent-based purpose (marketing email, analytics where consent is required, AI training opt-in) gets its own unticked control, separate from the terms checkbox.

## 3. Cookie banners, trackers, and opt-out signals

### EU: ePrivacy Directive Art 5(3)

- Storing or reading information on a user's device is allowed only with consent after clear and comprehensive information, except storage/access for the sole purpose of transmitting a communication or "strictly necessary" for a service the user explicitly requested ([Directive 2002/58/EC Art 5(3), consolidated](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219)).
- It applies to any "information", not only personal data ([CJEU C-673/17 Planet49, ruling 2](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0673); [EDPB Guidelines 2/2023 v2.0, para 7](https://www.edpb.europa.eu/system/files/documents/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf)).
- Cookie information must include cookie duration and whether third parties can access them ([Planet49, ruling 3](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0673)).
- Scope is technology-neutral: the EDPB says Art 5(3) covers tracking pixels and URL tracking, JavaScript that instructs the browser to send stored data, SDKs, local-processing APIs, IP-based tracking where the IP originates from the device, and unique identifiers ([EDPB Guidelines 2/2023 v2.0, adopted 7 Oct 2024, sections 2-3](https://www.edpb.europa.eu/system/files/documents/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf)).
- Cookie consent must meet the GDPR consent standard; pre-ticked boxes are invalid ([Planet49, ruling 1](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0673); [GDPR Recital 32](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Scrolling or swiping is never consent ([EDPB 05/2020, para 86](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Cookie walls (no access without accepting) do not produce freely given consent ([EDPB 05/2020, paras 39-41](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Legitimate interest cannot be the basis for placing or reading cookies under Art 5(3) ([EDPB Cookie Banner Taskforce report, 17 Jan 2023, para 24](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).

### EDPB cookie banner taskforce positions

- By default, no consent-requiring cookie may be set before a positive action by the user ([Taskforce report, para 7](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).
- A vast majority of authorities treat a banner with an accept button but no reject option on the same layer as an infringement ([Taskforce report, para 8](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).
- A reject "link" buried in text or placed outside the banner without sufficient visual support does not yield valid consent ([Taskforce report, para 14](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).
- Button colour/contrast is assessed case by case, but an unreadable reject button is manifestly misleading ([Taskforce report, para 18](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).
- Mislabelling non-essential cookies as "essential" is a listed bad practice; site owners must be able to justify each "essential" classification ([Taskforce report, para 26](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).
- Withdrawal must be possible at any time and as easy as giving consent, for example a persistent icon or a link in a standard visible place ([Taskforce report, paras 32-35](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf); [GDPR Art 7(3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- These are a common minimum; national rules and national DPA guidance also apply ([Taskforce report, preamble](https://www.edpb.europa.eu/system/files/2023-01/edpb_20230118_report_cookie_banner_taskforce_en.pdf)).

### France (CNIL) audience-measurement exemption

- Analytics trackers can be exempt from consent if strictly limited to measuring the site's/app's audience for the publisher alone, used only to produce anonymous statistics, not used for cross-site tracking, and non-anonymous data is not passed to third parties ([CNIL, Cookies: solutions pour les outils de mesure d'audience](https://www.cnil.fr/fr/cookies-solutions-pour-les-outils-de-mesure-daudience)).
- CNIL recommends a tracker lifetime of about 13 months without automatic extension and a maximum data retention of 25 months ([CNIL, mesure d'audience](https://www.cnil.fr/fr/cookies-solutions-pour-les-outils-de-mesure-daudience)).
- CNIL's developer guide adds: inform users, let them object, truncate the last byte of the IP address, and limit scope to a single publisher ([CNIL Sheet 16](https://www.cnil.fr/en/sheet-ndeg16-use-analytics-your-websites-and-applications)).
- CNIL says most large audience-measurement offerings fall outside the exemption ([CNIL Sheet 16](https://www.cnil.fr/en/sheet-ndeg16-use-analytics-your-websites-and-applications)).
- The exemption is a French reading of Art 5(3); other member states may differ ([CNIL Sheet 16](https://www.cnil.fr/en/sheet-ndeg16-use-analytics-your-websites-and-applications)).

### UK: PECR regulation 6 and Schedule A1 (in force 5 Feb 2026)

- Default: no storage or access on a user's device; "access" includes collecting information automatically emitted by the device ([PECR reg 6](https://www.legislation.gov.uk/uksi/2003/2426/regulation/6)).
- Exceptions: consent with clear and comprehensive information; transmission of a communication; strictly necessary for a requested service (including security, fraud prevention, fault detection, authentication, remembering user input) ([PECR Sch A1 paras 2-4](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- New statistical exception: first-party analytics whose sole purpose is improving the service or website, data not shared except with someone helping make those improvements, clear information given, and a simple free means of objecting provided and not used ([PECR Sch A1 para 5](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- The statistical exception does not cover collecting information automatically emitted by the device (for example fingerprinting signals) ([PECR Sch A1 para 5(2)](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- New appearance exception: storage whose sole purpose is adapting the site to user preferences or enhancing appearance/functionality, with information and a simple free opt-out ([PECR Sch A1 para 6](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- "Website" includes a mobile app ([PECR Sch A1 para 1](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- Advertising is not among the exceptions, so ad and cross-site tracking still need consent ([PECR Sch A1](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).

### US: opt-out of sale/sharing and Global Privacy Control (CCPA)

- A business that sells or shares must post a "Do Not Sell or Share My Personal Information" link (or the alternative opt-out link) in the homepage header or footer ([Civ. Code 1798.135(a)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf); [11 CCR 7013(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- It must treat a qualifying opt-out preference signal (for example an HTTP header or JavaScript object) as a valid opt-out for that browser/device and any linked profile, including pseudonymous profiles ([11 CCR 7025(b)-(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- The California AG identifies the GPC as such a signal ([CA AG CCPA page, FAQ 8](https://oag.ca.gov/privacy/ccpa)).
- Posting the links does not excuse ignoring signals; signals must be processed either way ([11 CCR 7025(e)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- The business must display whether it processed the signal, for example "Opt-Out Request Honored" ([11 CCR 7025(c)(6)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- A cookie banner alone is not an acceptable opt-out method, because cookies concern collection, not sale/sharing ([11 CCR 7026(a)(4)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Opt-outs must not require an account or identity verification and must take effect as soon as feasible, no later than 15 business days ([11 CCR 7026(c)-(f)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf); [11 CCR 7060(b)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Wait at least 12 months before asking an opted-out user to opt back in ([11 CCR 7026(k)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Enforcement example: Tractor Supply paid $1.35M (Sept 2025) partly because its opt-out form did not stop cookie-based sharing and it did not process opt-out preference signals ([CPPA announcement](https://cppa.ca.gov/announcements/2025/20250930.html)).

### Implementation

- A consent manager that loads zero non-exempt scripts, pixels, or SDKs until the user acts; gate tags in code, not just by hiding them.
- First layer: "Accept all" and "Reject all" buttons of equal size, weight, and contrast, plus "Settings"; unticked category toggles; a persistent "Privacy choices" link to reopen.
- Store consent record: categories, banner version, timestamp, region.
- Read `Sec-GPC: 1` / `navigator.globalPrivacyControl` server- and client-side; when set, disable sale/sharing tags for that browser and the logged-in account, and show "Opt-out request honored".
- Region logic is optional; the simplest compliant default is EU-grade consent for everyone plus GPC handling for everyone.

## 4. Marketing consent separate from service consent

- EU: email/SMS direct marketing needs prior consent ([ePrivacy Directive Art 13(1)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219)).
- EU soft opt-in: a business that obtained an email address from a customer in the context of a sale may market its own similar products, if the customer was given a clear, free, easy chance to object at collection and in every message ([ePrivacy Directive Art 13(2)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219)).
- UK: the same soft opt-in is in PECR reg 22(3), and from 5 February 2026 charities have their own soft opt-in in reg 22(3A) ([PECR reg 22](https://www.legislation.gov.uk/uksi/2003/2426/regulation/22)).
- Marketing consent must be separate from service terms ([GDPR Art 7(2), 7(4)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)) and granular per purpose ([EDPB 05/2020, para 42](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- Pre-ticked opt-in boxes and opt-out boxes are invalid ([EDPB 05/2020, para 79](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf); [Planet49, ruling 1](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0673)).
- The user may object to direct marketing at any time, and the data must then no longer be used for it ([GDPR Art 21(2)-(3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- The controller must be able to demonstrate consent: who, when, what they were shown ([GDPR Art 7(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng); [EDPB 05/2020, paras 104-108](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).

### Implementation

- Signup has an unticked "Email me product news and offers" box, separate from the terms control; or, for soft opt-in, a visible opt-out box at checkout.
- Every marketing email has a one-click unsubscribe that takes effect immediately; transactional email stays on.
- Log consent source, text shown, and timestamp.

## 5. Access, deletion, and other data subject requests

### GDPR / UK GDPR

- Respond without undue delay and within one month; extendable by two further months for complexity or volume, with notice and reasons within the first month ([GDPR Art 12(3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Requests and responses are free unless manifestly unfounded or excessive ([GDPR Art 12(5)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- If the controller has reasonable doubts about identity it may ask for information necessary to confirm it ([GDPR Art 12(6)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Access: confirmation, a copy of the data, and the purposes, categories, recipients, retention, rights, source, and automated decision information ([GDPR Art 15](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Electronic requests get electronic answers ([GDPR Art 12(3), 15(3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Erasure without undue delay when, among other grounds, data is no longer needed, consent is withdrawn, or the user objects ([GDPR Art 17(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Tell each recipient about an erasure unless impossible or disproportionate ([GDPR Art 19](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Portability: data the user provided, processed by automated means on consent or contract, in a structured, commonly used, machine-readable format ([GDPR Art 20(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- UK changes: the one-month clock starts at the latest of receipt, receipt of ID information, or fee payment, and pauses while the controller waits for clarification it reasonably needs ([UK GDPR Art 12A, in force 5 Feb 2026](https://www.legislation.gov.uk/eur/2016/679/article/12A.)).
- UK access is limited to what a "reasonable and proportionate search" finds ([UK GDPR Art 15(1A)](https://www.legislation.gov.uk/eur/2016/679/article/15)).

### CCPA

- Exclusively online businesses with a direct consumer relationship need only provide an email address for requests to know, delete, and correct; others need two or more methods including a toll-free number, plus the website if they have one ([Civ. Code 1798.130(a)(1)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf); [11 CCR 7020(a)-(b)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Confirm receipt within 10 business days ([11 CCR 7021(a)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Respond within 45 calendar days from receipt regardless of verification time, extendable once by 45 days with notice ([11 CCR 7021(b)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf); [Civ. Code 1798.130(a)(2)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- Deletion means erase, deidentify, or aggregate in active systems; backups may wait until restored or next accessed ([11 CCR 7022(b), (d)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- On deletion, notify service providers/contractors and third parties the data was sold/shared to ([11 CCR 7022(b)(2)-(3)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- An optional second "confirm deletion" step is allowed online ([11 CCR 7020(d)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Verification: for password-protected accounts, use existing authentication and require re-authentication before deleting, correcting, or disclosing ([11 CCR 7061(a)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Non-account holders: two matching data points for categories, three plus a signed declaration for specific pieces ([11 CCR 7062(b)-(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Do not charge for verification; delete any new data collected for verification as soon as practical ([11 CCR 7060(d)-(e)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Enforcement example: Honda (March 2025) was fined in part for asking opt-out requesters for more information than needed and for requiring verification on opt-outs ([CPPA Honda order](https://cppa.ca.gov/regulations/pdf/20250307_hmc_order.pdf)).

### App stores

- Apple requires in-app account deletion for any app that supports account creation ([App Review Guideline 5.1.1(v)](https://developer.apple.com/app-store/review/guidelines/)).
- Google Play requires an in-app deletion path and a web link where users can request account and data deletion ([Play Console Help: account deletion](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en)).

### Implementation

- Settings page: "Download my data" (JSON/CSV export of user-provided data) and "Delete my account" (re-auth, optional confirm, hard delete or deidentify, queue processor/vendor deletions).
- A public web form or email address for people without accounts, and for app-store deletion links.
- A request ledger with received date, verification state, response deadline (shorter of GDPR one month and CCPA 45 days), and outcome; keep the ledger record per CCPA 7101.

## 6. Data minimisation and retention limits

- Personal data must be adequate, relevant, and limited to what is necessary ([GDPR Art 5(1)(c)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Data must be kept in identifiable form no longer than necessary ([GDPR Art 5(1)(e)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- The notice must state the retention period or the criteria for it ([GDPR Art 13(2)(a)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Data protection by default: only data necessary for each purpose, covering amount, extent, storage period, and accessibility ([UK GDPR Art 25(2)](https://www.legislation.gov.uk/eur/2016/679/article/25), same text as the EU GDPR).
- CCPA: notice at collection must state retention per category, and a business may not keep data longer than reasonably necessary for each disclosed purpose ([Civ. Code 1798.100(a)(3)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- CCPA: collection, use, retention, and sharing must be "reasonably necessary and proportionate" to the disclosed purpose or a compatible one ([Civ. Code 1798.100(c)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf); [11 CCR 7002](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- FTC: Blackbaud (Feb 2024) was charged with holding data "far longer than was necessary" and ordered to delete unneeded data and adopt a retention schedule ([FTC Blackbaud press release](https://www.ftc.gov/news-events/news/press-releases/2024/02/ftc-order-will-require-blackbaud-delete-unnecessary-data-boost-safeguards-settle-charges-its-lax)).
- FTC: GoodRx and BetterHelp orders both required data retention schedules ([FTC GoodRx](https://www.ftc.gov/news-events/news/press-releases/2023/02/ftc-enforcement-action-bar-goodrx-sharing-consumers-sensitive-health-info-advertising); [FTC BetterHelp](https://www.ftc.gov/news-events/news/press-releases/2023/03/ftc-ban-betterhelp-revealing-consumers-data-including-sensitive-mental-health-information-facebook)).
- COPPA now requires a written retention policy for children's data, published in the online notice, and bans indefinite retention ([16 CFR 312.10](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).

### Implementation

- Retention table in code (per data category: TTL, deletion job, legal hold exceptions) that also renders into the privacy policy.
- Scheduled jobs that purge expired rows, logs, analytics events, and backups past their window.
- Do not collect fields that no feature reads; review the schema against the inventory at each release.

## 7. Children

### COPPA (US, under 13)

- Covers operators of sites or services directed to children, and general-audience operators with actual knowledge they collect personal information from a child under 13 ([16 CFR 312.3](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- "Directed to children" weighs subject matter, visuals, characters, music, models, celebrities, ads, and now also audience-composition evidence, marketing plans, and reviews ([16 CFR 312.2](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- A "mixed audience" service (child-directed but children not the primary audience) must age-screen neutrally before collecting personal information, without defaulting to an age or encouraging falsification ([16 CFR 312.2](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Personal information includes persistent identifiers (cookie IDs, IP address, device IDs) and, since the 2025 amendments, biometric identifiers ([16 CFR 312.2](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Verifiable parental consent is required before collection, use, or disclosure, and a separate consent is required for disclosure to third parties unless integral to the service ([16 CFR 312.5(a)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Approved consent methods: signed form; card or payment transaction with notice; staffed toll-free call or video call; government ID check against databases (then delete); knowledge-based questions; government photo ID matched to a live face image (then delete); "email plus" or text plus extra steps if the operator does not disclose children's data ([16 CFR 312.5(b)](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Written information security program with an annual risk assessment ([16 CFR 312.8](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Written retention policy, no indefinite retention ([16 CFR 312.10](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- Dates: amended Rule effective 23 June 2025; compliance required by 22 April 2026, except listed safe-harbor provisions ([Federal Register 2025-05904](https://www.federalregister.gov/documents/2025/04/22/2025-05904/childrens-online-privacy-protection-rule)).
- FTC staff FAQ on age screens: ask date of birth freely, do not default to 13+, do not say under-13s cannot join (encourages lying), do not use "I am over 12" checkboxes, and use a cookie to stop back-button retries ([FTC COPPA FAQ](https://www.ftc.gov/business-guidance/resources/complying-coppa-frequently-asked-questions)).
- The FAQ body predates the 2025 amendments and carries a banner pointing to the amended Rule ([FTC COPPA FAQ](https://www.ftc.gov/business-guidance/resources/complying-coppa-frequently-asked-questions)).
- Since 25 February 2026, the FTC will not bring COPPA actions against general- or mixed-audience operators that collect data solely to determine age, if they limit use, delete promptly, vet vendors, give notice, secure it, and use reasonably accurate methods ([FTC policy statement press release](https://www.ftc.gov/news-events/news/press-releases/2026/02/ftc-issues-coppa-policy-statement-incentivize-use-age-verification-technologies-protect-children)).

### GDPR Art 8 and UK

- When consent is the basis for an information society service offered directly to a child, under-16s need parental consent; member states may lower the age to no less than 13 ([GDPR Art 8(1)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- The controller must make reasonable efforts to verify parental consent ([GDPR Art 8(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Member-state ages vary between 13 and 16; this note does not tabulate them because no primary consolidated table was found (see open questions).
- UK age is 13 directly in the UK GDPR ([UK GDPR Art 8](https://www.legislation.gov.uk/eur/2016/679/article/8)).
- UK: since 5 February 2026, services likely to be accessed by children must weigh "children's higher protection matters" when designing data protection measures ([UK GDPR Art 25(1A)-(1B)](https://www.legislation.gov.uk/eur/2016/679/article/25)).
- The ICO Age Appropriate Design Code (15 standards) applies to services likely to be accessed by under-18s, and requires high-privacy defaults, geolocation off by default, profiling off by default, and no nudges toward weaker privacy ([ICO, Age appropriate design code](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/age-appropriate-design-a-code-of-practice-for-online-services/); ico.org.uk timed out, content read from the search index).
- California: actual knowledge of selling/sharing data of under-16s requires opt-in (parent for under 13) and a policy statement either way ([11 CCR 7011(e)(1)(G), 7070-7071](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).

### Practical default for a general-audience app

- Write terms that the service is not for under-13s (or under-16s where we want to avoid Art 8 parental-consent flows in the EU), and do not design child-appealing content.
- Use a neutral date-of-birth screen at signup that follows the FTC FAQ rules; on an under-age result, block signup, set a cookie to prevent immediate retry, and do not store the entered birthdate beyond the decision.
- If we learn a user is under 13 (support ticket, parent contact), delete the account data promptly, since that is actual knowledge.
- No behavioural ads, no third-party trackers, and high-privacy defaults on any product that children are likely to use (UK code).

## 8. Data processing agreements and subprocessors

### GDPR Art 28

- Use only processors providing sufficient guarantees, under a binding contract stating subject matter, duration, nature, purpose, data types, data-subject categories, and the controller's rights ([GDPR Art 28(1), (3)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- The contract must require the processor to: act only on documented instructions; bind staff to confidentiality; apply Art 32 security; follow the subprocessor rules; help with data-subject requests; help with Arts 32-36 (security, breach, DPIA); delete or return data at the end; and provide information and allow audits ([GDPR Art 28(3)(a)-(h)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- A processor may not engage a subprocessor without the controller's prior specific or general written authorisation ([GDPR Art 28(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- Under general authorisation, the processor must inform the controller of intended additions or replacements so the controller can object ([GDPR Art 28(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- That notice-and-object duty is why SaaS vendors publish subprocessor lists with change notifications.
- The same obligations must flow down to subprocessors, and the initial processor stays liable for them ([GDPR Art 28(4)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- EDPB: controllers should have the identity (name, address, contact) of all processors and subprocessors in the chain readily available ([EDPB Opinion 22/2024](https://www.edpb.europa.eu/system/files/2024-10/edpb_opinion_202422_relianceonprocessors-sub-processors_en.pdf); conclusions read from the EDPB search index).

### CCPA service providers (11 CCR 7051)

- The contract must: prohibit selling/sharing; name specific business purposes (not "the entire contract"); bar use outside those purposes and outside the direct relationship, including combining with other data; require CCPA compliance and equal protection; give audit and remediation rights; require notice if the provider can no longer comply; and require help with consumer requests ([11 CCR 7051(a)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Service providers must have conforming contracts with their own subcontractors ([11 CCR 7051(b)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Without a compliant contract, a disclosure may be a "sale" or "share" rather than a service-provider disclosure ([Civ. Code 1798.100(d)](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- Never auditing a vendor weakens the defence that you had no reason to believe it misused data ([11 CCR 7051(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).

### Implementation

- For every vendor that touches user data (hosting, DB, email, analytics, error tracking, LLM API, payments): accept its DPA, record its subprocessor list URL, and subscribe to change notices.
- Keep a vendor register (vendor, data categories, purpose, region, transfer mechanism, DPA link, CCPA service-provider terms yes/no) in the repo.
- If we are the processor for business customers, publish our own subprocessor list and a notice-and-object process.

## 9. Using user data to train AI

- FTC (13 Feb 2024): adopting more permissive data practices, such as AI training, through a "surreptitious, retroactive amendment" to terms or privacy policy may be unfair or deceptive ([FTC Office of Technology blog](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/02/ai-other-companies-quietly-changing-your-terms-service-could-be-unfair-or-deceptive)).
- The post cites Gateway Learning (2004) and a 2023 genetic-testing case, both of which retroactively expanded data sharing without notice or consent ([FTC blog](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/02/ai-other-companies-quietly-changing-your-terms-service-could-be-unfair-or-deceptive)).
- FTC (9 Jan 2024): model-as-a-service companies must honour commitments not to use customer data to train models, wherever the commitment was made, and the FTC has required deletion of models and algorithms built on unlawfully obtained data ([FTC Office of Technology blog](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/01/ai-companies-uphold-your-privacy-confidentiality-commitments)).
- Both posts were still live on ftc.gov on the research date.
- EU: there is no hierarchy of legal bases; legitimate interest needs a three-step test (legitimate interest, necessity, balancing) ([EDPB Opinion 28/2024, executive summary](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
- Reasonable expectations matter, and a mention in the privacy policy "does not necessarily mean" users can reasonably expect the training ([EDPB Opinion 28/2024, para 92](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
- Mitigating measures the EDPB lists include an unconditional opt-out before processing, honouring erasure beyond Art 17 grounds, a gap between collection and training so users can act, and channels for memorisation/regurgitation claims ([EDPB Opinion 28/2024, para 102](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
- A model trained on personal data is anonymous only if extraction of personal data, directly or via queries, is insignificant, assessed case by case ([EDPB Opinion 28/2024, executive summary](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
- California: using personal information for a purpose the consumer would not reasonably expect needs a separate consent and cannot be bundled with the core service ([11 CCR 7002](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf); [11 CCR 7004(a)(4)(B)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- California: processing personal information to train ADMT for significant decisions, or facial/emotion recognition or identity verification technology, requires a risk assessment ([11 CCR 7150(b)(6)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- EU omnibus: the Council mandate adds a clarified lawful ground for AI training with safeguards, but it is not law ([Council press release](https://www.consilium.europa.eu/en/press/press-releases/2026/10/21/digital-rulebook-council-agrees-position-to-simplify-data-protection-privacy-and-cyber-reporting-rules/), search index).

### What a compliant setup looks like

- Default: user content is not used to train or fine-tune models; calling a third-party LLM API to serve the user is processing for the service (contract), not training, and is covered by the vendor DPA with a no-training clause.
- If we want training: a separate, unticked opt-in toggle in settings, explained in plain words, recorded with timestamp, revocable, with revocation excluding the user's data from future training runs.
- Never apply new training uses to data collected under older promises; change the policy prospectively, notify users in advance, and require opt-in for existing data.

## 10. Auditing third-party SDKs, analytics, and pixels

- FTC v. GoodRx (Feb 2023): first Health Breach Notification Rule action, $1.5M civil penalty, for sharing prescription and health data with Facebook, Google, Criteo, and others for advertising, contrary to its promises ([FTC GoodRx](https://www.ftc.gov/news-events/news/press-releases/2023/02/ftc-enforcement-action-bar-goodrx-sharing-consumers-sensitive-health-info-advertising)).
- The GoodRx order bans sharing health data for advertising, requires affirmative express consent for other sharing, deletion requests to third parties, and a retention schedule ([FTC GoodRx](https://www.ftc.gov/news-events/news/press-releases/2023/02/ftc-enforcement-action-bar-goodrx-sharing-consumers-sensitive-health-info-advertising)).
- FTC v. BetterHelp (Mar 2023): $7.8M for sharing email addresses, IP addresses, and health questionnaire answers with Facebook, Snapchat, Criteo, and Pinterest for ads after promising privacy ([FTC BetterHelp](https://www.ftc.gov/news-events/news/press-releases/2023/03/ftc-ban-betterhelp-revealing-consumers-data-including-sensitive-mental-health-information-facebook)).
- FTC technologists warn that pixels can send purchases and form inputs, that hashing is not anonymisation, and that blocking third-party cookies may not stop pixels ([FTC, Lurking Beneath the Surface, 16 Mar 2023](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2023/03/lurking-beneath-surface-hidden-impacts-pixel-tracking)).
- The amended Health Breach Notification Rule (finalized April 2024) covers health apps outside HIPAA and treats an unauthorized disclosure, not only a hack, as a breach ([FTC press release](https://www.ftc.gov/news-events/news/press-releases/2024/04/ftc-finalizes-changes-health-breach-notification-rule)).
- HIPAA itself reaches only covered entities and business associates ([45 CFR 160.103](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-160/subpart-A/section-160.103)).
- HHS's tracking-technology bulletin was reported partly vacated in AHA v. Becerra (N.D. Tex., 20 June 2024) as to IP addresses on unauthenticated pages, and HHS reportedly dropped its appeal in August 2024.
- That point rests on secondary reports only, because hhs.gov blocked automated fetches; verify against the court order before relying on it.
- Washington My Health My Data Act applies to any entity doing business in Washington or targeting Washington consumers that handles consumer health data, with no revenue threshold ([RCW 19.373.010](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- "Consumer health data" includes inferences derived from non-health data, such as by algorithms ([RCW 19.373.010, "consumer health data" (b)(xiii)](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- It requires a separate consumer health data privacy policy linked from the homepage ([RCW 19.373.020](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- It requires consent to collect (unless necessary for the requested service) and a separate, distinct consent to share ([RCW 19.373.030](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- It requires a signed authorization to sell ([RCW 19.373.070](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- It grants deletion rights that reach backups within six months ([RCW 19.373.040](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- Violations are enforceable through the Washington Consumer Protection Act, which includes private actions ([RCW 19.373.090](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- Effective 31 March 2024 (30 June 2024 for small businesses) ([RCW 19.373.020-.050](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- A business subject to CCPA must conduct a risk assessment before selling or sharing personal information or processing sensitive personal information, with pre-2026 ongoing processing assessed by 31 December 2027 ([11 CCR 7150(b), 7155](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).

### Practical audit expectations

- Before adding any SDK, pixel, or script: record what it collects, where it sends it, whether the vendor uses it for its own purposes, and whether it needs consent (EU/UK) or counts as "sharing" (CA).
- Run a network capture (browser devtools / proxy for mobile) on each release in a fresh profile, with and without consent and with GPC on, and diff against the vendor register; nothing non-exempt should fire before consent.
- Never place ad or social pixels on pages or screens that reveal health, finance, children's, or other sensitive data, including URLs, page titles, and form fields; disable automatic form and URL capture in session-replay and analytics tools.
- Prefer server-side, first-party, self-hosted analytics configured to the CNIL / PECR statistical-exception conditions.

## 11. Dark patterns in consent and privacy UI

- California: choices must be easy to understand, symmetric, not confusing, and not designed to impair choice, and requests must be easy to execute ([11 CCR 7004(a)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- The privacy-protective path may not be longer or harder than the other path ([11 CCR 7004(a)(2)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- "Accept All" paired only with "More information" or "Preferences" is not symmetric; "Accept All" / "Decline All" is ([11 CCR 7004(a)(2)(C)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- "Yes" / "Ask me later" is not symmetric ([11 CCR 7004(a)(2)(B)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- A more prominent "yes" button is not symmetric ([11 CCR 7004(a)(2)(D)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Prohibited: double negatives, unlabeled on/off toggles, inconsistent button order, treating closing a pop-up as consent, and fake urgency ([11 CCR 7004(a)(3)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- After clicking "Do Not Sell or Share", the user must not have to scroll through a policy to find the mechanism ([11 CCR 7004(a)(5)(A)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Agreement obtained through a dark pattern is not consent, and intent does not matter if the business knows of and does not fix the effect ([11 CCR 7004(b)-(c)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- Enforcement: Honda and Tractor Supply orders both cite asymmetric cookie or opt-out choices under 7004(a)(2) ([CPPA Honda order](https://cppa.ca.gov/regulations/pdf/20250307_hmc_order.pdf); [CPPA Tractor Supply](https://cppa.ca.gov/announcements/2025/20250930.html)).
- EU: the EDPB's deceptive design guidelines (v2.0, 14 Feb 2023) group patterns into six categories: overloading (continuous prompting, privacy maze, too many options), skipping (deceptive snugness, look over there), stirring (emotional steering, hidden in plain sight), obstructing (dead end, longer than necessary, misleading action), fickle (lacking hierarchy, decontextualising, inconsistent interface, language discontinuity), and left in the dark ([EDPB Guidelines 03/2022 v2.0](https://www.edpb.europa.eu/system/files/documents/2023-02/edpb_03-2022_guidelines_on_deceptive_design_patterns_in_social_media_platform_interfaces_v2_en_0.pdf)).
- The EDPB guidelines are addressed to social media platforms, but they interpret general GDPR principles (fairness, transparency, consent, data protection by design) and are the best available EU reference for any consent UI ([EDPB Guidelines 03/2022 v2.0](https://www.edpb.europa.eu/system/files/documents/2023-02/edpb_03-2022_guidelines_on_deceptive_design_patterns_in_social_media_platform_interfaces_v2_en_0.pdf)).

### Implementation checklist

- Equal-weight accept/reject buttons with identical styling; same number of clicks to refuse as to accept.
- Toggle labels state the effect ("Share my data for ads: Off"); no double negatives.
- No re-prompting after refusal within the same session; CCPA requires 12 months before re-asking after an opt-out.
- Account deletion and opt-out reachable from settings in two or three taps, with no retention offers blocking the path.

## Common misconceptions

- "We only need a privacy policy if we are big." False: CalOPPA has no size threshold, and GDPR applies to any non-EU app offering services to people in the EU ([CalOPPA 22575(a)](https://oag.ca.gov/sites/all/files/agweb/pdfs/cybersecurity/making_your_privacy_practices_public.pdf); [GDPR Art 3(2)](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng)).
- "CCPA only applies above $25M revenue." Incomplete: the threshold is now $26,625,000, and any business that buys, sells, or shares data of 100,000+ Californians (ad pixels count as sharing) is covered regardless of revenue ([CPPA CPI adjustment](https://www.cppa.ca.gov/regulations/cpi_adjustment.html); [Civ. Code 1798.140](https://cppa.ca.gov/pdf/20260101_ccpa_statute.pdf)).
- "Users must tick 'I accept the privacy policy'." Wrong under GDPR: the policy is a notice, and bundling consent into it or the terms invalidates the consent ([EDPB 05/2020, paras 13, 71](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
- "Strictly necessary covers analytics." Not under the ePrivacy Directive text; only France's CNIL exemption, the UK's new 2026 statistical exception, and similar national rules carve out narrow analytics, each with conditions ([ePrivacy Art 5(3)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219); [CNIL](https://www.cnil.fr/fr/cookies-solutions-pour-les-outils-de-mesure-daudience); [PECR Sch A1 para 5](https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1)).
- "Cookie rules only apply to cookies or to personal data." False: Art 5(3) covers pixels, SDKs, local storage, fingerprinting, and any "information" ([EDPB Guidelines 2/2023](https://www.edpb.europa.eu/system/files/documents/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf); [Planet49](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0673)).
- "The Digital Omnibus already relaxed EU cookie rules." False as of 2026-10-31: only a Council mandate exists, and current law applies ([Council press release](https://www.consilium.europa.eu/en/press/press-releases/2026/10/21/digital-rulebook-council-agrees-position-to-simplify-data-protection-privacy-and-cyber-reporting-rules/)).
- "A cookie banner satisfies CCPA opt-out." False: a cookie tool alone is not an acceptable opt-out method, and GPC must be honored even if you post the link ([11 CCR 7026(a)(4), 7025(e)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- "We can require ID to opt out." False under CCPA; verification is only for know/delete/correct ([11 CCR 7060(b)](https://cppa.ca.gov/regulations/pdf/ccpa_statute_eff_20260101.pdf)).
- "UK and EU DSAR rules are identical." No longer: the UK added a reasonable-and-proportionate search limit, a stop-the-clock rule, and a controller complaints duty ([UK GDPR Art 12A](https://www.legislation.gov.uk/eur/2016/679/article/12A.); [Art 15(1A)](https://www.legislation.gov.uk/eur/2016/679/article/15); [DPA 2018 s.164A](https://www.legislation.gov.uk/ukpga/2018/12/section/164A)).
- "COPPA only matters for kids' apps." Partly false: general-audience apps are covered once they have actual knowledge of an under-13 user, and persistent identifiers count as personal information ([16 CFR 312.2-312.3](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312)).
- "The 2025 COPPA amendments are not in force yet." False: compliance was due 22 April 2026 ([Federal Register 2025-05904](https://www.federalregister.gov/documents/2025/04/22/2025-05904/childrens-online-privacy-protection-rule)).
- "HIPAA does not apply, so health data is unregulated." False: the FTC Act, the Health Breach Notification Rule, and Washington's MHMDA apply to non-HIPAA health apps ([FTC GoodRx](https://www.ftc.gov/news-events/news/press-releases/2023/02/ftc-enforcement-action-bar-goodrx-sharing-consumers-sensitive-health-info-advertising); [RCW 19.373](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)).
- "Updating the privacy policy is enough to start AI training on existing data." The FTC says quiet retroactive changes may be unfair or deceptive, and the EDPB says a policy mention does not establish reasonable expectations ([FTC Feb 2024](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/02/ai-other-companies-quietly-changing-your-terms-service-could-be-unfair-or-deceptive); [EDPB Opinion 28/2024, para 92](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
- "Hashing emails before sending them to ad platforms makes it anonymous." The FTC says hashes can be reversed or used to link data ([FTC pixel blog](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2023/03/lurking-beneath-surface-hidden-impacts-pixel-tracking)).

## Open questions / needs a lawyer

- EU member-state Art 8 ages: confirm each target country's digital age of consent from national law before relying on any age below 16.
- Digital Omnibus: track trilogue outcome and effective dates; cookie exemptions (audience measurement, security) and AI-training legal ground may change the default design.
- CalOPPA text: confirm no amendments after the 2014 version reproduced by the AG (leginfo blocked automated access).
- California AB 1043 (Digital Age Assurance Act) is reported by secondary sources as operative 1 January 2027, requiring developers to request OS/app-store age-bracket signals; the bill text was not reachable (leginfo blocked), so verify before designing age screening for California.
- Texas SB 2420 (app-store age verification): secondary sources report it was enjoined in December 2025, the Fifth Circuit stayed the injunction on 4 June 2026, and the Supreme Court declined to vacate the stay on 6 July 2026; not verified against primary dockets.
- Other US state privacy laws (Colorado, Connecticut, Texas, Oregon, and others) have their own thresholds, universal opt-out mechanism rules, and sensitive-data opt-in rules; this note covers only California and Washington.
- EU-US Data Privacy Framework: the General Court upheld it on 3 September 2025 and an appeal (C-703/25 P) was reported pending in mid-2026; confirm status before relying on DPF for US vendors instead of SCCs.
- Whether we need an EU and UK Art 27 representative for each app (the "occasional processing" exemption is narrow and fact-specific).
- Whether a given app is "likely to be accessed by children" under the UK code, which pulls in the 15 standards.
- Whether a feature's data (fitness, mood, period tracking, inferred wellness) is "consumer health data" under MHMDA or "health information" under the FTC HBNR.
- CPPA's open preliminary rulemakings on opt-out preference signals and notices may change 7011, 7012, and 7025 requirements in 2027.
- Exact UK ICO cookie, direct-marketing, and children's code guidance wording should be re-checked once ico.org.uk is reachable; this note relied on statute plus search-index excerpts for ICO guidance.
