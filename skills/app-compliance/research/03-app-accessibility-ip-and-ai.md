# 03 - App Accessibility, IP Licensing, and AI Labelling

Research date: 2026-10-31.
Scope: baseline legal and licensing obligations an AI coding agent must apply to every small web or mobile app we build (US owner; users in the US, EU/UK, and elsewhere).
Every claim carries an inline link to the primary source it was checked against on the research date.
Where a primary page blocked automated fetches, the note says so and names what was read instead.
This is engineering research, not legal advice; the last section lists what needs a lawyer.

## 1. Accessibility legal baseline

### Target: WCAG 2.2 level AA

WCAG 2.2 is a W3C Recommendation dated 12 December 2024 ([W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/)).
WCAG 2.2 marks 4.1.1 Parsing as "Obsolete and removed", so tools that still flag Parsing failures are out of date ([WCAG 2.2, 4.1.1](https://www.w3.org/TR/WCAG22/#parsing)).
We target 2.2 AA because it is a superset of the 2.1 AA that the US Title II rule requires (see below) and it is the version EN 301 549 V4.1.1 references ([NDA Ireland](https://nda.ie/news/en301549-published)).

### US: ADA Title III (private businesses, which is us)

DOJ guidance (dated 18 March 2022) says Title III prohibits discrimination by "businesses open to the public" and that this covers goods and services "including those offered on the web" ([ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/)).
The same guidance says DOJ has no regulation setting detailed web standards for businesses and that businesses "have flexibility in how they comply", while still having to make online offerings accessible; it points to WCAG and the Section 508 Standards as existing technical standards ([ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/)).
The page is still live on ADA.gov as of 2026-10-31, with a notice that it does not reflect the 2024 Title II rule ([ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/)).
ADA.gov's footer states guidance documents "have no legally binding effect" ([ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/)).
Practical reading: there is no fixed WCAG version in law for private apps, so WCAG 2.2 AA is our chosen, defensible bar rather than a statutory one.

### US: DOJ Title II rule (state and local governments, and their vendors)

The 2024 rule makes WCAG 2.1 Level AA the technical standard for state and local government web content and mobile apps, including content a contractor or vendor provides on the government's behalf ([ADA.gov fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/)).
It has five exceptions (archived web content, preexisting conventional electronic documents, third-party content posted by the public, password-protected individualized documents, preexisting social media posts), each with conditions that must all be met ([ADA.gov fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/)).
An Interim Final Rule published 20 April 2026 (FR doc 2026-07663) moved the compliance dates by one year ([Federal Register](https://www.federalregister.gov/documents/2026/04/20/2026-07663/extension-of-compliance-dates-for-nondiscrimination-on-the-basis-of-disability-accessibility-of-web); [ADA.gov](https://www.ada.gov/title-ii-web-rule/)).
Current dates: entities with population 50,000 or more must comply by **26 April 2027**; entities under 50,000 and special district governments by **26 April 2028** ([ADA.gov Title II web rule](https://www.ada.gov/title-ii-web-rule/); [ADA.gov fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/)).
The original dates were 24 April 2026 and 26 April 2027 ([ADA.gov fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/)).
The IFR changed only dates; the standard remains WCAG 2.1 AA (per the IFR summary on [ADA.gov](https://www.ada.gov/title-ii-web-rule/); federalregister.gov blocked automated fetch, so the IFR text itself was not read).
Applies to us only if an app is sold to or built for a US state or local government, in which case its content is "provided on behalf of" that government ([ADA.gov fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/)).

### EU: European Accessibility Act (Directive (EU) 2019/882)

Member States had to apply their national EAA measures from **28 June 2025** ([Directive 2019/882, Art. 31(2)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
Services covered (only when "provided to consumers"): electronic communications, access to audiovisual media, specified elements of passenger transport (websites, mobile apps, e-tickets, travel info), consumer banking, e-books and dedicated software, and **e-commerce services** ([Art. 2(2)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
"E-commerce services" means services provided at a distance through websites and mobile device-based services, by electronic means, at the individual request of a consumer "with a view to concluding a consumer contract" ([Art. 3(30)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
**Microenterprises providing services are exempt** from the accessibility requirements and related obligations ([Art. 4(5)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
A microenterprise employs fewer than 10 persons and has annual turnover not exceeding EUR 2 million or an annual balance sheet total not exceeding EUR 2 million ([Art. 3(23)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
Non-exempt service providers must publish, in their terms and conditions or equivalent, information describing how the service meets the accessibility requirements, in accessible formats ([Art. 13(2) and Annex V](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
An operator may claim "disproportionate burden" or "fundamental alteration" only after a documented assessment, kept for five years ([Art. 14](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
Transitional rule: service contracts agreed before 28 June 2025 may continue unaltered until expiry but no longer than five years from that date ([Art. 32(1)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
Conformity with harmonised standards cited in the Official Journal gives a presumption of conformity ([Art. 15(1)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
EN 301 549 V4.1.1 (references WCAG 2.2 AA, built for the EAA) was published 2 September 2026 but is not yet cited in the OJ; citation is expected 16 December 2026, and until then V3.2.1 (WCAG 2.1) remains the cited version ([NDA Ireland](https://nda.ie/news/en301549-published)).
Applies to us: a consumer-facing shop or checkout flow sold into the EU once we pass microenterprise size; a B2B-only SaaS or a non-listed consumer app is outside Art. 2(2).

### UK: Equality Act 2010

A service provider to the public "must not discriminate" against a person requiring the service ([Equality Act 2010 s.29(1)](https://www.legislation.gov.uk/ukpga/2010/15/section/29)), and the duty to make reasonable adjustments applies to service providers ([s.29(7)](https://www.legislation.gov.uk/ukpga/2010/15/section/29)).
For services, the duty is owed to "disabled persons generally", i.e. it is anticipatory ([Schedule 2 para 2](https://www.legislation.gov.uk/ukpga/2010/15/schedule/2)).
Where information is involved, reasonable steps include ensuring the information "is provided in an accessible format" ([s.20(6)](https://www.legislation.gov.uk/ukpga/2010/15/section/20)).
The Act names no WCAG version for private services, so WCAG 2.2 AA is again our chosen bar.

## 2. WCAG 2.2 success criteria the skill must enforce

Each item: requirement, then how to test it.

- **1.1.1 Non-text Content (A).** All non-text content has a text alternative serving the equivalent purpose; controls and inputs have a name describing their purpose ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#non-text-content)).
  Pure decoration must be implementable so assistive technology can ignore it ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#non-text-content)).
  Decorative `<img>`: `alt=""` present and empty, and `title` absent or empty; a missing `alt` is not the same as an empty one ([W3C technique H67](https://www.w3.org/WAI/WCAG22/Techniques/html/H67)).
  Test: automated tools catch a missing `alt`; only a human can judge whether alt text is equivalent.
- **1.4.3 Contrast (Minimum) (AA).** Text and images of text at least **4.5:1**; large-scale text at least **3:1**; incidental text (inactive components, pure decoration) and logotypes are exempt ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#contrast-minimum)).
  Large scale means at least 18 point, or 14 point bold ([WCAG 2.2 definition](https://www.w3.org/TR/WCAG22/#dfn-large-scale)).
  Ratio formula: (L1 + 0.05) / (L2 + 0.05) using relative luminance ([WCAG 2.2 definition](https://www.w3.org/TR/WCAG22/#dfn-contrast-ratio)).
  Specifying a text color without a background color (or vice versa) is a failure because the user default is unknown ([WCAG 2.2 definition notes](https://www.w3.org/TR/WCAG22/#dfn-contrast-ratio)).
- **1.4.11 Non-text Contrast (AA).** At least **3:1** against adjacent colors for visual information needed to identify UI components and their states, and for graphical objects needed to understand content; inactive components and unmodified user-agent styling are exempt ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#non-text-contrast)).
- **2.1.1 Keyboard (A).** All functionality operable through a keyboard interface without specific keystroke timings, except path-dependent input such as freehand drawing ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#keyboard)).
- **2.1.2 No Keyboard Trap (A).** If focus can move into a component by keyboard it can move out by keyboard; if non-standard keys are needed, the user is told how ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#no-keyboard-trap)).
  This criterion applies to all content on the page, even content not used to meet other criteria ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#no-keyboard-trap)).
  Test: modals, date pickers, embedded editors and iframes, by tabbing in and out.
- **2.4.1 Bypass Blocks (A).** A mechanism exists to bypass blocks repeated on multiple pages ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#bypass-blocks)).
  Typical implementation: a "Skip to main content" link plus landmarks.
- **2.4.3 Focus Order (A).** When sequential navigation affects meaning or operation, focus order preserves meaning and operability ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#focus-order)).
  Test: no positive `tabindex`; focus moves into opened dialogs and returns to the trigger on close.
- **2.4.7 Focus Visible (AA).** Any keyboard-operable UI has a mode where the focus indicator is visible ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#focus-visible)).
  Test: grep for `outline: none` / `outline: 0` without a `:focus-visible` replacement.
- **2.4.11 Focus Not Obscured (Minimum) (AA, new in 2.2).** A focused component is not *entirely* hidden by author-created content (sticky headers, cookie banners, chat widgets) ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum)).
  Content the user opened may obscure focus if the user can reveal the component without moving focus ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum)).
  Test: tab through the page and compare each focused element's bounding box with fixed/sticky overlays; `scroll-padding-top` equal to the sticky header height is the usual fix.
- **2.2.1 Timing Adjustable (A).** For each time limit set by content, the user can turn it off, adjust it to at least ten times the default, or is warned and given at least 20 seconds to extend with a simple action, at least ten times; exceptions are real-time events (e.g. auctions), essential limits, and limits longer than 20 hours ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#timing-adjustable)).
  A countdown timer that ends a session, a quiz, a reservation hold, or a checkout falls here.
  A purely informational countdown (e.g. a sale ending at a real-world time) is not a time limit on the user's task, but see 2.2.2.
- **2.2.2 Pause, Stop, Hide (A).** Auto-updating information that starts automatically and is shown in parallel with other content needs a way to pause, stop, hide, or control update frequency, unless essential; moving, blinking or scrolling content lasting more than five seconds needs pause, stop or hide ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#pause-stop-hide)).
  A ticking countdown and carousels fall here.
- **2.5.8 Target Size (Minimum) (AA, new in 2.2).** Pointer targets at least **24 by 24 CSS pixels**, except: spacing (a 24px-diameter circle centered on each undersized target intersects no other target or circle), an equivalent control elsewhere on the page, inline targets in sentences, user-agent-sized targets, or essential presentation ([WCAG 2.2](https://www.w3.org/TR/WCAG22/#target-size-minimum)).
  The Understanding document describes 2.5.5 Target Size (Enhanced) as stricter and recommends aiming for it on important controls ([Understanding 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)).
  Test: measure `getBoundingClientRect()` of every interactive element.

### Automated tooling

- **axe-core**: rules for WCAG 2.0, 2.1 and 2.2 at levels A, AA and AAA; the README says it finds "on average 57% of WCAG issues automatically", and it returns "incomplete" results that need manual review ([axe-core README](https://github.com/dequelabs/axe-core)).
  Latest is 4.14.0 (5 Oct 2026), licensed **MPL-2.0** ([npm registry](https://www.npmjs.com/package/axe-core)).
  Use via `@axe-core/playwright` or `@axe-core/cli` in CI with tags `wcag2a, wcag2aa, wcag21a, wcag21aa, wcag22aa`.
- **Lighthouse**: the accessibility score is a weighted average of pass/fail audits with no partial credit, weighted by axe user-impact assessments; manual audits do not affect the score, and the docs list manual checks such as focus order and focus traps ([Lighthouse scoring](https://developer.chrome.com/docs/lighthouse/accessibility/scoring)).
  A score of 100 therefore does not mean conformance.
  Latest is 13.6.0 ([npm registry](https://www.npmjs.com/package/lighthouse)).
- **pa11y**: runners `htmlcs` (default) and `axe`; `--standard WCAG2AA` is the default; `--threshold N` sets the error count that fails the run; current major version 10, license LGPL-3.0-only ([pa11y README](https://github.com/pa11y/pa11y)).
  Use `--runner axe --runner htmlcs` for wider coverage.
- **What tools cannot do**: W3C states that evaluation tools "can not determine accessibility, they can only assist", that "Human judgement is required", and that tools can produce false or misleading results ([W3C, Selecting evaluation tools](https://www.w3.org/WAI/test-evaluate/tools/selecting/)).
  Not reliably automatable: whether alt text is equivalent (1.1.1), logical focus order (2.4.3), keyboard traps inside custom widgets (2.1.2), focus hidden behind overlays during real navigation (2.4.11), time-limit handling (2.2.1), contrast of text over images or gradients (1.4.3), and state contrast on hover/focus (1.4.11).
  The skill must pair the automated scan with a scripted keyboard walk (Playwright: press Tab repeatedly, record `document.activeElement`, assert visibility, assert escape from dialogs) and a short manual checklist.

## 3. DMCA safe harbor and EU notice-and-action

### When the app needs it

Section 512(c) protects a service provider from monetary liability for infringement "by reason of the storage at the direction of a user" of material on its system ([17 U.S.C. 512(c)(1)](https://www.law.cornell.edu/uscode/text/17/512)).
So it matters only if users can upload or post content (images, text, files, profiles, comments) that we store and serve.
An app with no user-generated content does not need a designated agent.

### 512(c) conditions (all required)

- No actual knowledge or red-flag awareness of the infringement, or expeditious removal once known ([512(c)(1)(A)](https://www.law.cornell.edu/uscode/text/17/512)).
- No financial benefit directly attributable to the infringing activity where the provider has the right and ability to control it ([512(c)(1)(B)](https://www.law.cornell.edu/uscode/text/17/512)).
- Expeditious removal or disabling of access upon a compliant notice ([512(c)(1)(C)](https://www.law.cornell.edu/uscode/text/17/512)).
- A designated agent, with name, address, phone and email published on the service "in a location accessible to the public" and filed with the Copyright Office ([512(c)(2)](https://www.law.cornell.edu/uscode/text/17/512)).
- A repeat-infringer termination policy that is adopted, reasonably implemented, and communicated to users, plus accommodation of standard technical measures ([512(i)(1)](https://www.law.cornell.edu/uscode/text/17/512)).

### Designated agent registration

The Copyright Office no longer accepts paper designations; registration is through its online system ([Copyright Office DMCA directory](https://www.copyright.gov/dmca-directory/)).
The fee is **$6** per designation, amendment, or resubmission ([37 CFR 201.3, table item 25](https://www.law.cornell.edu/cfr/text/37/201.3); [DMCA FAQ](https://www.copyright.gov/dmca-directory/faq.html)).
A designation "will expire and become invalid three years after it is registered" unless renewed by amending or resubmitting it, which starts a new three-year period ([37 CFR 201.38(c)(4)](https://www.law.cornell.edu/cfr/text/37/201.38)).
The system emails reminders 90, 60, 30 and 7 days before expiry ([DMCA FAQ](https://www.copyright.gov/dmca-directory/faq.html)).
On lapse the provider risks losing section 512 safe harbor protection ([DMCA FAQ](https://www.copyright.gov/dmca-directory/faq.html)).
The filing must list the provider's full legal name and **physical street address** (a P.O. box for the provider needs a safety-based waiver), plus all alternate names the public would use, including website domains and app names ([37 CFR 201.38(b)](https://www.law.cornell.edu/cfr/text/37/201.38); [DMCA FAQ](https://www.copyright.gov/dmca-directory/faq.html)).
The agent's own address may be a P.O. box without a waiver ([DMCA FAQ](https://www.copyright.gov/dmca-directory/faq.html)).

### Takedown and counter-notice flow (implement as a state machine)

1. Notice must be written and substantially include: signature; identification of the work; identification and location of the infringing material; complainant contact info; a good-faith statement; and an accuracy statement plus a statement under penalty of perjury of authority to act ([512(c)(3)(A)](https://www.law.cornell.edu/uscode/text/17/512)).
2. Remove or disable access expeditiously ([512(c)(1)(C)](https://www.law.cornell.edu/uscode/text/17/512)).
3. Take reasonable steps promptly to notify the uploader ([512(g)(2)(A)](https://www.law.cornell.edu/uscode/text/17/512)).
4. A counter notice must include the subscriber's signature, identification of the removed material and its former location, a statement under penalty of perjury of good-faith belief of mistake or misidentification, and name, address, phone and consent to federal court jurisdiction ([512(g)(3)](https://www.law.cornell.edu/uscode/text/17/512)).
5. On a valid counter notice, promptly send a copy to the original complainant and say the material will be restored in 10 business days ([512(g)(2)(B)](https://www.law.cornell.edu/uscode/text/17/512)).
6. Restore the material **not less than 10 and not more than 14 business days** after receiving the counter notice, unless the complainant first notifies the agent that it has filed suit ([512(g)(2)(C)](https://www.law.cornell.edu/uscode/text/17/512)).
7. Record each strike against the account for the repeat-infringer policy ([512(i)(1)(A)](https://www.law.cornell.edu/uscode/text/17/512)).

Following this flow shields the provider from claims by the uploader over a good-faith takedown ([512(g)(1)-(2)](https://www.law.cornell.edu/uscode/text/17/512)).
Knowing material misrepresentation in a notice or counter notice creates liability for damages and fees ([512(f)](https://www.law.cornell.edu/uscode/text/17/512)).

### EU: Digital Services Act notice-and-action

The DSA applies from 17 February 2024 ([Regulation (EU) 2022/2065, Art. 93](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
Any hosting provider must offer an easy, electronic mechanism for anyone to report specific illegal content, facilitating notices with: a substantiated explanation, the exact URL(s), the notifier's name and email, and a good-faith statement ([Art. 16(1)-(2)](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
The provider must confirm receipt without undue delay, notify its decision with redress options, decide in a timely, diligent, non-arbitrary and objective way, and disclose any automated decision-making ([Art. 16(4)-(6)](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
Any removal, visibility restriction, monetisation restriction, or account suspension requires a clear and specific statement of reasons to the affected user when contact details are known ([Art. 17](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
Articles 16 and 17 have no micro-enterprise carve-out; the Art. 19 exemption for micro and small enterprises covers only the online-platform section (Arts. 20-28, except 24(3)) ([Art. 19](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)); transparency reporting under Art. 15 is waived for micro and small enterprises ([Art. 15(2)](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
All intermediary services must publish a single point of contact for authorities and for users ([Arts. 11-12](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
A provider without an EU establishment that offers services in the Union must designate in writing a legal representative in a Member State ([Art. 13(1)](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
"Offering services in the Union" requires a substantial connection, such as a significant number of users in a Member State or targeting activities toward Member States ([Art. 3(d)-(e)](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).

## 4. Open source license obligations

### Permissive

- **MIT**: "The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software" ([OSI, MIT](https://opensource.org/license/mit)).
  Minified bundles count as copies, so the notice must travel with the shipped bundle or a linked notices file.
- **BSD-2/3-Clause**: same pattern (retain the copyright notice, conditions, and disclaimer in source and in documentation for binaries); 3-Clause adds a no-endorsement clause.
  (License texts on the [SPDX License List](https://spdx.org/licenses/).)
- **ISC**: notice and permission notice must "appear in all copies" (as quoted on [Lucide's license page](https://lucide.dev/license)).
- **Apache-2.0** redistribution conditions: give recipients a copy of the License; mark modified files; retain copyright, patent, trademark and attribution notices; and **if the work includes a NOTICE file, include a readable copy of its attribution notices** in a NOTICE file, in the source or documentation, or in a display "if and wherever such third-party notices normally appear" ([Apache License 2.0, s.4(a)-(d)](https://www.apache.org/licenses/LICENSE-2.0)).

### Weak copyleft

- **MPL-2.0** is file-level: if you distribute covered files in executable form, their source must be available and recipients told how to get it; you may combine them into a "Larger Work" under terms of your choice ([MPL-2.0 s.3.2-3.3](https://www.mozilla.org/en-US/MPL/2.0/)).
  Practical rule: do not modify MPL files in place, or publish the modified files.
  The axe-core library itself is MPL-2.0 ([npm registry](https://www.npmjs.com/package/axe-core)).
- **LGPL-3.0**: a combined work may be under your terms if you give prominent notice that the library is used, include copies of the GPL and LGPL, include its notice among any runtime copyright notices, and either provide materials to relink against a modified library or "use a suitable shared library mechanism" ([LGPL-3.0 s.4](https://opensource.org/license/lgpl-3-0)).
  Static linking into a mobile binary makes the relink option hard; prefer dynamic linking or avoid.

### Strong copyleft

- **GPL**: you may run a modified GPL program privately or on your server without releasing source; the FSF says a company running a modified GPL program on a website "does not have to release the modified sources" ([GPL FAQ #UnreleasedMods](https://www.gnu.org/licenses/gpl-faq.html#UnreleasedMods)).
  But GPL code sent to the browser (e.g. JavaScript) is distributed, and its source "must be released to the user under the terms of the GPL" ([GPL FAQ #UnreleasedMods](https://www.gnu.org/licenses/gpl-faq.html#UnreleasedMods)).
  The same applies to any GPL code compiled into a shipped mobile app.

### Network copyleft

- **AGPL-3.0 s.13**: if you **modify** the program, your version must prominently offer all users interacting with it remotely over a network the Corresponding Source, from a network server at no charge ([AGPL-3.0 s.13](https://www.gnu.org/licenses/agpl-3.0.html#section13)).
  Mere network interaction without transferring a copy is not "conveying" ([AGPL text via OSI](https://opensource.org/license/agpl-v3)).
  Rule for the skill: AGPL in the request path of our SaaS is blocked by default; AGPL tools used unmodified as separate services need explicit owner sign-off.

### Source-available (not open source)

- **SSPL**: OSI states SSPL is not an open source license; its steward withdrew it from review ([OSI blog](https://opensource.org/blog/the-sspl-is-not-an-open-source-license)).
- **BSL 1.1**: allows copying, modification and non-production use; production use beyond the licensor's "Additional Use Grant" needs a commercial license; it converts to the Change License on the Change Date (no later than the fourth anniversary of first public distribution) and states it "is not an Open Source license" ([MariaDB BSL 1.1](https://mariadb.com/bsl11/)).
- **Elastic License 2.0**: may not provide the software to third parties as a hosted or managed service, may not circumvent license-key functionality, and may not remove licensor notices ([Elastic License 2.0](https://www.elastic.co/licensing/elastic-license)).
- On SPDX License List 3.29.0 (2026-09-16), SSPL-1.0, BUSL-1.1 and Elastic-2.0 are listed without an OSI-approved mark ([SPDX License List](https://spdx.org/licenses/)).
  The skill should gate on the OSI-approved flag, not on "source is on GitHub".

### Producing a third-party notices file

1. Generate an SBOM: `npm sbom --sbom-format spdx --omit dev` (or `cyclonedx`) ([npm sbom docs](https://docs.npmjs.com/cli/v11/commands/npm-sbom)).
   SPDX is the ISO/IEC 5962:2021 standard; the current spec line is 3.0 ([SPDX specifications](https://spdx.dev/use/specifications/)).
2. Collect license and NOTICE texts for production dependencies: Python `pip-licenses --format=json --with-license-file --with-notice-file` (5.5.5, March 2026) ([pip-licenses](https://pypi.org/project/pip-licenses/)); Node `license-checker-rseidelsohn` (5.0.1, May 2026), because the original `license-checker` was last published in January 2019 ([npm registry](https://www.npmjs.com/package/license-checker-rseidelsohn); [npm registry](https://www.npmjs.com/package/license-checker)).
3. Fail CI on disallowed licenses: `pip-licenses --allow-only=...` / `--fail-on=...` ([pip-licenses](https://pypi.org/project/pip-licenses/)); the npm equivalent is `license-checker-rseidelsohn --production --onlyAllow '...'` or `--failOn '...'` ([license-checker-rseidelsohn README](https://github.com/RSeidelsohn/license-checker-rseidelsohn#readme)).
4. Deep scan when manifests lie or code is vendored: ScanCode detects licenses, copyrights and package manifests and emits JSON, SPDX or CycloneDX ([ScanCode toolkit](https://github.com/aboutcode-org/scancode-toolkit)).
5. Detect a single repo's own license: `licensee` matches LICENSE files against known licenses with a similarity score ([licensee](https://github.com/licensee/licensee)).
6. Keep our own repo machine-readable with REUSE 3.3: `LICENSES/` folder named by SPDX ID, `SPDX-License-Identifier` and `SPDX-FileCopyrightText` headers, or `REUSE.toml` annotations ([REUSE spec 3.3](https://reuse.software/spec-3.3/)).
7. Ship `THIRD_PARTY_NOTICES.txt` (and an in-app "Open source licenses" screen on mobile) containing, per component: name, version, SPDX ID, copyright lines, full license text, and verbatim Apache NOTICE contents.

## 5. Font licenses

### SIL Open Font License 1.1

OFL permits use, study, copy, merge, embed, modify, redistribute, and sell copies, subject to five conditions ([OFL 1.1 text](https://openfontlicense.org/documents/OFL.txt)):

1. The font may not be sold by itself.
2. It may be bundled, redistributed or sold with any software if each copy contains the copyright notice and license (as a text file, header, or viewable metadata).
3. Modified versions may not use a Reserved Font Name without written permission.
4. Author names may not be used to promote modified versions.
5. The font stays under OFL, but documents created with it do not.

The OFL FAQ says serving fonts via CSS `@font-face` is distribution and is allowed ([OFL FAQ 2.1](https://openfontlicense.org/ofl-faq/)).
Subsetting is a modification, and a font with declared Reserved Font Names must then be renamed ([OFL FAQ 2.6](https://openfontlicense.org/ofl-faq/)).
Converting to WOFF2 keeps the name only if font data is unchanged except compression and metadata is kept intact or omitted ([OFL FAQ 2.2-2.2.1](https://openfontlicense.org/ofl-faq/)).
Commercial apps, including mobile apps, may ship OFL fonts, and the app itself need not be open source ([OFL FAQ 1.3-1.4](https://openfontlicense.org/ofl-faq/)).
The FAQ asks that the copyright statement, license notice and license text be included for fonts used ([OFL FAQ 1.20](https://openfontlicense.org/ofl-faq/)).
(scripts.sil.org/OFL now resolves to openfontlicense.org, which hosts the official text.)

### Google Fonts

Most families use OFL 1.1, some use Apache 2.0, and the Ubuntu fonts use the Ubuntu Font License 1.0; each family directory holds its license file, and the top-level `ofl/`, `apache/`, `ufl/` directory names the license ([google/fonts README](https://github.com/google/fonts)).
Self-hosting is therefore governed by the individual family's license, not by a Google-wide term.

### Commercial and Adobe Fonts

Desktop and webfont licenses from commercial foundries are separate products; read each EULA for pageview caps, app embedding and self-hosting.
Adobe Fonts (via Creative Cloud): Adobe does not offer self-hosting, and self-hosting needs a license bought from the foundry; fonts may not be embedded inside mobile or desktop applications (web views are fine); a client's site must load fonts through the client's own subscription ([Adobe Fonts licensing FAQ](https://helpx.adobe.com/fonts/web/font-licensing/font-licensing.html); [Adobe web fonts FAQ](https://helpx.adobe.com/fonts/using/webfont-licensing.html)).
Caveat: helpx.adobe.com returned 403 to automated fetches; these points come from Adobe's own text as quoted in the search index on 2026-10-31 and should be rechecked in a browser.
Skill rule: default to OFL/Apache fonts self-hosted; never copy a font file out of a Creative Cloud sync folder or a paid desktop license into an app bundle.

## 6. Image and icon licenses

### Unsplash

Unsplash grants an irrevocable, nonexclusive, worldwide license to download, copy, modify and distribute photos for commercial and non-commercial use without permission; attribution is not required ([Unsplash License](https://unsplash.com/license)).
Images may not be sold without significant modification, and Unsplash images may not be compiled to replicate a similar or competing service ([Unsplash License](https://unsplash.com/license)).
The license page does not address model or property releases, so photos with identifiable people or trademarks need separate judgment.

### Creative Commons 4.0

- **BY**: when sharing, keep creator identification, copyright notice, license notice, disclaimer notice, and a URI to the material where reasonably practicable, and indicate modifications ([CC BY 4.0 s.3(a)(1)](https://creativecommons.org/licenses/by/4.0/legalcode.en)); a link to a page with this information satisfies the condition in a reasonable manner for the medium ([s.3(a)(2)](https://creativecommons.org/licenses/by/4.0/legalcode.en)).
  Commercial use is allowed.
- **NC**: "not primarily intended for or directed towards commercial advantage or monetary compensation" ([CC BY-NC-ND 4.0 s.1](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode.en)).
  Treat any NC asset as unusable in a monetised app.
- **ND**: you may not share Adapted Material ([CC BY-NC-ND 4.0 s.3(a)(1)(A)](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode.en)).
  Cropping, recoloring or compositing an ND image and publishing it is out.

### Icon sets

- **Lucide**: ISC license, with icons derived from Feather under MIT (Cole Bemis) ([Lucide license](https://lucide.dev/license)); npm `lucide` 1.66.0 declares ISC ([npm registry](https://www.npmjs.com/package/lucide)).
- **Heroicons**: MIT, Copyright Tailwind Labs ([Heroicons LICENSE](https://github.com/tailwindlabs/heroicons/blob/master/LICENSE)).
- **Font Awesome Free**: icons as SVG/JS are CC BY 4.0; icons as web/desktop font files are SIL OFL 1.1 with Reserved Font Name "Font Awesome"; all other non-font, non-icon files are MIT ([Font Awesome LICENSE.txt](https://github.com/FortAwesome/Font-Awesome/blob/7.x/LICENSE.txt)).
  Attribution is required by all three, but the embedded comments in the downloaded files are sufficient for normal use; do not strip them ([Font Awesome LICENSE.txt](https://github.com/FortAwesome/Font-Awesome/blob/7.x/LICENSE.txt)).
  Brand icons are trademarks and may only represent the brand they depict ([Font Awesome LICENSE.txt](https://github.com/FortAwesome/Font-Awesome/blob/7.x/LICENSE.txt)). npm declares `(CC-BY-4.0 AND OFL-1.1 AND MIT)` ([npm registry](https://www.npmjs.com/package/@fortawesome/fontawesome-free)).
  Build tools that inline SVGs and drop comments break the CC BY attribution, so add Font Awesome to the notices file.

### AI-generated images and copyright (US)

The Copyright Office's Part 2 report (29 January 2025) concludes that copyright does not extend to purely AI-generated material or material without sufficient human control over expressive elements, and that "prompts do not alone provide sufficient control" ([Copyright Office, Part 2, p.iii](https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf); [copyright.gov/ai](https://www.copyright.gov/ai/)).
The report says human expression perceptible in the output, and creative selection, arrangement or modification of AI output, remain protectable ([Part 2, p.iii](https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf)).
Registration guidance asks applicants to disclose more than de minimis AI-generated material and describe the human contribution ([Part 2, citing 88 Fed. Reg. 16,190](https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf)).
In *Thaler v. Perlmutter* (D.C. Cir., decided 18 March 2025) the court held that the Copyright Act "requires all eligible work to be authored in the first instance by a human being" ([D.C. Cir. opinion No. 23-5233](https://media.cadc.uscourts.gov/opinions/docs/2025/03/23-5233.pdf)).
The opinion notes the rule still lets humans seek rights in works "they make with the assistance of artificial intelligence" ([opinion](https://media.cadc.uscourts.gov/opinions/docs/2025/03/23-5233.pdf)).
The Supreme Court **denied certiorari on 2 March 2026** (No. 25-449), so the D.C.
Circuit ruling stands ([Supreme Court docket 25-449](https://www.supremecourt.gov/docket/docketfiles/html/public/25-449.html)).
Practical rule: purely generated hero images, icons or illustrations give us no exclusive rights, so competitors may copy them; this is a business risk, not a compliance breach.

## 7. Labelling AI-generated content

### EU AI Act Article 50

Article 50 applies from **2 August 2026** ([Regulation (EU) 2024/1689, Art. 113](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
The AI Act applies to providers placing AI systems on the EU market regardless of where they are established, and to non-EU providers and deployers where the output is used in the Union ([Art. 2(1)(a),(c)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).

- **50(1) Chatbots and agents (provider duty)**: systems intended to interact directly with people must be designed so people are informed they are interacting with an AI system, unless obvious to a reasonably well-informed, observant and circumspect person ([Art. 50(1)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
- **50(2) Machine-readable marking (provider duty)**: providers of systems generating synthetic audio, image, video or text must ensure outputs are marked in a machine-readable format and detectable as AI-generated, as far as technically feasible; this does not apply to assistive standard editing or outputs that do not substantially alter the input ([Art. 50(2)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
- **50(4) Deepfakes and public-interest text (deployer duty)**: deployers must disclose deep fake image, audio or video, with a lighter regime for evidently artistic, satirical or fictional works; AI-generated text published to inform the public on matters of public interest must be disclosed unless it underwent human review or editorial control with editorial responsibility ([Art. 50(4)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
  A "deep fake" is AI-generated or manipulated image, audio or video resembling existing persons, objects, places, entities or events that would falsely appear authentic ([Art. 3(60)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
- **50(5) Timing and form**: information must be clear and distinguishable, given at the latest at first interaction or exposure, and must meet accessibility requirements ([Art. 50(5)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
- **Penalties**: Article 50 breaches carry fines up to EUR 15 million or 3% of worldwide turnover, whichever is higher; for SMEs and start-ups, whichever is lower ([Art. 99(4),(6)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).

**Digital Omnibus status (verified in the Official Journal text)**: Regulation (EU) 2026/1744 of 8 July 2026 was published on 24 July 2026 and entered into force on the third day after publication ([Regulation (EU) 2026/1744, Art. 4](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
It did **not** postpone Article 50 generally.
It adds Art. 111(4): providers of systems generating synthetic audio, image, video or text **placed on the market before 2 August 2026** must comply with Art. 50(2) by **2 December 2026** ([Reg. 2026/1744, point (39)(b)](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
Recital 38 describes this as a four-month transitional period for those already-marketed systems only ([Reg. 2026/1744, recital 38](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
It also amends Art. 50(7) so the Commission assesses codes of practice for adequacy instead of approving them by implementing act ([Reg. 2026/1744, point (20)](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
The delays it made are to high-risk rules: 2 December 2027 for Annex III systems and 2 August 2028 for Annex I systems ([Reg. 2026/1744, point (40)(b)](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
(EUR-Lex blocks automated fetches; the text was read from the EU Publications Office copy of CELEX 32026R1744.)

**Commission guidance**: the Commission adopted Article 50 guidelines on 20 July 2026 (C(2026) 5054) ([Commission guidelines page](https://digital-strategy.ec.europa.eu/en/library/guidelines-transparency-obligations-providers-and-deployers-ai-systems); [PDF](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
The guidelines say a company offering a chatbot, image generator or AI agent on the EU market under its own name is a provider, whether free or paid and wherever established ([Guidelines para. 11](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
They list as insufficient on their own: disclosure only in terms, URLs or docs; invisible metadata or watermarks; generic labels like "assistant"; human-like avatars that may mislead; and blanket statements like "Services on this website use AI" ([Guidelines para. 38](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
They recommend persistent icons or recognisable "AI" symbols alongside a first-turn textual disclosure ([Guidelines para. 37](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
They exclude from 50(2) short outputs such as single words, captions, alt text and UI labels, and source code ([Guidelines para. 68](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
Marking may use one technique or a combination (watermarks, metadata, cryptographic provenance, logging, fingerprints) ([Guidelines paras. 72-73](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)).
The final voluntary Code of Practice on marking and labelling AI-generated content was published 10 June 2026; signing is voluntary, the obligations are not, and the EU offers optional label icons for deployers ([Commission code of practice page](https://digital-strategy.ec.europa.eu/en/policies/code-practice-ai-generated-content)).

### California AI Transparency Act (SB 942, amended by AB 853, SB 1000, AB 2713)

The chapter is operative **2 August 2026** ([Bus. & Prof. Code 22757.6](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.&article=)).
**SB 1000 (Ch. 861, approved 30 September 2026, urgency statute, effective immediately) deleted the 1,000,000-monthly-user threshold** ([SB 1000 chaptered text](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
A "covered provider" is now "a person that creates, codes, or otherwise produces a generative artificial intelligence system that is publicly accessible within the geographic boundaries of the state" ([B&P 22757.1(e) as amended](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
Covered-provider duties now:

- Provide a free, publicly accessible **disclosure verification tool** (replacing the "AI detection tool") that lets users upload a file or URL, shows system provenance data, withholds personal information absent consent, and has an API; a compliant third-party tool linked clearly from the UI is acceptable ([B&P 22757.2](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- Embed a **latent disclosure** where technically feasible in image, video or audio content created or altered (beyond minor modification) by the system, conveying provider name, system name and version, creation time, a unique identifier, and whether the content was created or altered; it must be permanent or extraordinarily difficult to remove and interoperable with widely recognized standards ([B&P 22757.3(a)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- The former duty to offer users an optional **manifest** (visible) disclosure was deleted ([SB 1000 digest](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- Notify licensees of their obligations, and act within 72 hours if a licensee's modification breaks compliance ([B&P 22757.3(b)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- Civil penalty $5,000 per violation, each day a separate violation, enforced by the Attorney General, city attorneys or county counsel ([B&P 22757.4](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- Exempt: exclusively non-user-generated videogames; and until 1 January 2029, systems designed primarily as assistive technology ([B&P 22757.5](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).

Text-only output is not within the latent-disclosure duty, which covers image, video and audio ([B&P 22757.3(a)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
Large online platforms (over 2,000,000 monthly users) must detect and surface provenance data and not strip it, from 1 January 2027 ([B&P 22757.1(i), 22757.3.1](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.&article=)); AB 2713 (Ch. 856, approved 30 September 2026) revised those platform duties ([AB 2713](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB2713)).
GenAI hosting platforms may not knowingly offer non-compliant systems from 1 January 2027, and capture-device duties start 1 January 2028 ([B&P 22757.3.2-22757.3.3](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.&article=)).

### California BOT Act (B&P 17940-17943)

It is unlawful to use a bot to communicate with a person in California online "with the intent to mislead the other person about its artificial identity" to incentivize a purchase or sale or to influence a vote; a person who discloses the bot is not liable ([B&P 17941(a)](https://california.public.law/codes/ca_bus_and_prof_code_section_17941)).
The disclosure must be "clear, conspicuous, and reasonably designed to inform persons ... that it is a bot" ([B&P 17941(b)](https://california.public.law/codes/ca_bus_and_prof_code_section_17941)).
A bot is an automated online account where all or substantially all actions or posts are not the result of a person ([B&P 17940(a)](https://california.public.law/codes/ca_bus_and_prof_code_section_17940)); the chapter has been operative since 1 July 2019 ([B&P 17943](https://california.public.law/codes/ca_bus_and_prof_code_section_17943)).
The 10,000,000-monthly-user "online platform" definition in 17940(c) relates to platforms, not to the bot-user's disclosure duty ([B&P 17940(c)](https://california.public.law/codes/ca_bus_and_prof_code_section_17940)).
AB 410, which would have broadened the Act, has been held in Senate Appropriations since 29 August 2025 ([AB 410 status](https://leginfo.legislature.ca.gov/faces/billStatusClient.xhtml?bill_id=202520260AB410)).
(Section text read from california.public.law, which marked it up to date as of 26 October 2026; the official leginfo code pages block automated fetches.)

### California companion chatbots (SB 243, B&P 22601-22605)

An operator of a "companion chatbot" (human-like, able to meet social needs) must give a clear and conspicuous notice that it is AI and not human if a reasonable person could be misled ([B&P 22602(a)](https://california.public.law/codes/ca_bus_and_prof_code_section_22602)).
For users known to be minors: disclose AI, and by default show a notice at least every three hours to take a break and that the bot is not human, and block sexually explicit content ([B&P 22602(c)](https://california.public.law/codes/ca_bus_and_prof_code_section_22602)).
Operators need a published suicide and self-harm protocol that refers users to crisis services ([B&P 22602(b)](https://california.public.law/codes/ca_bus_and_prof_code_section_22602)).
Bots used only for customer service, business operations, productivity and analysis are excluded ([B&P 22601(b)(2)](https://california.public.law/codes/ca_bus_and_prof_code_section_22601)).
The section is in force from 1 January 2026 ([B&P 22602 history](https://california.public.law/codes/ca_bus_and_prof_code_section_22602)).

### Utah (Utah Code Title 13, Chapter 75)

A supplier using generative AI in a consumer transaction must disclose that the person is interacting with AI and not a human **only if the person asks**, and the question must be "a clear and unambiguous request" ([SB 226 (2025), 13-75-103(1)](https://le.utah.gov/Session/2025/bills/enrolled/SB0226.pdf)).
Licensed or state-certified regulated occupations must **prominently** disclose generative AI in "high-risk" interactions (sensitive health, financial or biometric data, or personalised financial, legal, medical or mental-health advice): verbally at the start of a voice interaction and in writing before a written one ([13-75-101(5), 13-75-103(2)-(3)](https://le.utah.gov/Session/2025/bills/enrolled/SB0226.pdf)).
Safe harbor: no enforcement under 13-75-103 if the AI clearly and conspicuously discloses at the outset and throughout that it is generative AI, not human, or an AI assistant ([13-75-104](https://le.utah.gov/Session/2025/bills/enrolled/SB0226.pdf)).
Using generative AI is no defense to a consumer-protection violation ([13-75-102](https://le.utah.gov/Session/2025/bills/enrolled/SB0226.pdf)).
The AI Policy Act is set to repeal on **1 July 2027** ([SB 332 (2025)](https://le.utah.gov/Session/2025/bills/enrolled/SB0332.pdf)); a September 2026 interim committee recommended renewal with a 1 July 2037 sunset, which needs 2027 legislation ([Utah Interim Highlights, Sept 2026](https://le.utah.gov/interim/2026/pdf/00003528.pdf)).

### FTC position

The FTC's authority over unfair or deceptive acts covers AI claims and AI-enabled deception generally ([15 U.S.C. 45](https://www.law.cornell.edu/uscode/text/15/45)); there is no FTC rule requiring a generic "AI-generated" label.
The FTC's March 2023 business blog post "Chatbots, deepfakes, and voice clones: AI deception for sale" warned against AI tools designed to deceive ([FTC business blog, March 2023 index](https://www.ftc.gov/business-guidance/blog/2023/03)).
The Consumer Reviews and Testimonials Rule (16 CFR Part 465), effective 21 October 2024, bans fake reviews, which the FTC says includes AI-generated fake reviews, with civil penalties for knowing violations ([FTC rule Q&A](https://www.ftc.gov/business-guidance/resources/consumer-reviews-testimonials-rule-questions-answers); [FTC press release](https://www.ftc.gov/news-events/news/press-releases/2024/08/federal-trade-commission-announces-final-rule-banning-fake-reviews-testimonials)).
On 22 December 2025 the FTC reopened and set aside its 2024 Rytr order, citing the AI Action Plan and finding the complaint did not meet FTC Act requirements, while saying it will still pursue AI-enabled deception ([FTC press release](https://www.ftc.gov/news-events/news/press-releases/2025/12/ftc-reopens-sets-aside-rytr-final-order-response-trump-administrations-ai-action-plan)).
In September 2025 the FTC opened a 6(b) study of AI companion chatbots ([FTC press release](https://www.ftc.gov/news-events/news/press-releases/2025/09/ftc-launches-inquiry-ai-chatbots-acting-companions)).
On 1 July 2026 it proposed (not final) a policy statement that steering AI outputs toward undisclosed objectives may be deceptive under Section 5 ([FTC press release](https://www.ftc.gov/news-events/news/press-releases/2026/07/ftc-seeks-public-comment-policy-statement-addressing-ai-accuracy)).
Practical reading: never present an AI agent as a named human, never generate reviews or testimonials, and keep capability claims substantiated.

### Practical UI patterns the skill should apply everywhere

1. Chat and agent UIs: a persistent "AI" badge on the assistant identity plus a first-message disclosure ("You're chatting with an AI assistant"); no human name or photo for the bot; answer "yes, I'm an AI" truthfully when asked.
   Satisfies EU Art. 50(1)/(5) as read with the guidelines, the BOT Act safe harbor, SB 243(a), and the Utah safe harbor (sources above).
2. For apps where minors may be users of a companion-style bot: the 3-hour reminder and crisis-referral protocol (SB 243).
3. Generated images, audio, video: embed C2PA Content Credentials with a `c2pa.created` action whose `digitalSourceType` is `http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia` ([C2PA 2.2 spec, Actions](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)); the latest published C2PA version is 2.5 ([C2PA specifications index](https://spec.c2pa.org/specifications/specifications/2.5/index.html)).
   Add a visible "AI-generated" label wherever the asset is shown, and never strip provenance metadata in image pipelines (resizing and format conversion are "minor modifications" under CA law, but stripping metadata defeats the latent disclosure).
4. Generated text shown to users: a visible "AI-generated" or "Drafted with AI" marker; machine-readable marking is required by Art. 50(2) for text-generating systems too, so store a generation flag and expose it in HTML (e.g. a `data-` attribute) and APIs.
5. Disclosures must themselves be accessible (Art. 50(5)): real text with an accessible name, not color or an icon alone.

## Common misconceptions

- "The EU AI Omnibus delayed AI labelling to 2027."
  False: Article 50 applies from 2 August 2026; only Art. 50(2) marking for systems already on the market before that date got until 2 December 2026 ([Reg. 2026/1744](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
- "California's AI Transparency Act only hits companies with over 1 million users."
  Outdated since 30 September 2026: SB 1000 removed the threshold ([SB 1000](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- "SB 942 starts 1 January 2026."
  Outdated: AB 853 moved it to 2 August 2026 ([B&P 22757.6](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=8.&title=&part=&chapter=25.&article=)).
- "DOJ's Title II deadline is April 2026."
  Outdated: it is 26 April 2027 or 26 April 2028 after the April 2026 IFR ([ADA.gov](https://www.ada.gov/title-ii-web-rule/)).
- "The ADA legally requires WCAG 2.1 AA for private businesses."
  No regulation sets a standard for Title III; DOJ guidance leaves flexibility ([ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/)).
- "The EAA covers every app with EU users."
  It covers listed consumer services only, and exempts microenterprises providing services ([Directive 2019/882, Arts. 2(2), 4(5)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
- "EN 301 549 already requires WCAG 2.2."
  V4.1.1 is published but not yet OJ-cited; V3.2.1 (WCAG 2.1) remains the cited version until then ([NDA Ireland](https://nda.ie/news/en301549-published)).
- "Lighthouse 100 means accessible."
  Lighthouse scores only automated pass/fail audits; axe-core finds on average 57% of issues ([Lighthouse](https://developer.chrome.com/docs/lighthouse/accessibility/scoring); [axe-core](https://github.com/dequelabs/axe-core)).
- "A DMCA agent registration is one-time."
  It expires after three years and lapses lose safe harbor protection ([37 CFR 201.38(c)(4)](https://www.law.cornell.edu/cfr/text/37/201.38)).
- "GPL in a SaaS backend forces us to publish source."
  Not for GPL used server-side; yes for GPL JavaScript sent to browsers, and AGPL s.13 applies once modified ([GPL FAQ](https://www.gnu.org/licenses/gpl-faq.html#UnreleasedMods); [AGPL s.13](https://www.gnu.org/licenses/agpl-3.0.html#section13)).
- "BSL, SSPL and Elastic are open source."
  Not OSI-approved ([OSI](https://opensource.org/blog/the-sspl-is-not-an-open-source-license); [MariaDB BSL](https://mariadb.com/bsl11/); [SPDX list](https://spdx.org/licenses/)).
- "Google Fonts are one license."
  Families are OFL, Apache 2.0 or UFL ([google/fonts](https://github.com/google/fonts)).
- "Subsetting an OFL font is fine as-is."
  Subsetting is a modification and requires renaming if the font declares Reserved Font Names ([OFL FAQ 2.6](https://openfontlicense.org/ofl-faq/)).
- "Font Awesome Free is MIT."
  Only the code is MIT; SVG icons are CC BY 4.0 and font files are OFL ([Font Awesome LICENSE](https://github.com/FortAwesome/Font-Awesome/blob/7.x/LICENSE.txt)).
- "Thaler is still pending at the Supreme Court."
  Cert was denied on 2 March 2026 ([docket 25-449](https://www.supremecourt.gov/docket/docketfiles/html/public/25-449.html)).
- "Utah requires every chatbot to announce it is AI."
  Only on a clear request, or up front in high-risk regulated-occupation services; the Act sunsets 1 July 2027 unless renewed ([SB 226](https://le.utah.gov/Session/2025/bills/enrolled/SB0226.pdf); [SB 332](https://le.utah.gov/Session/2025/bills/enrolled/SB0332.pdf)).
- "The FTC requires AI labels."
  No general rule exists; the FTC acts on deception case by case, and it vacated the Rytr order in December 2025 ([FTC](https://www.ftc.gov/news-events/news/press-releases/2025/12/ftc-reopens-sets-aside-rytr-final-order-response-trump-administrations-ai-action-plan)).
- "`license-checker` is the standard npm tool."
  Its last release was January 2019; use a maintained fork or `npm sbom` ([npm registry](https://www.npmjs.com/package/license-checker)).

## Open questions / needs a lawyer

- **California "covered provider" for API wrappers.** After SB 1000, does an app that sends prompts to a third-party image model (OpenAI, Google, etc.) "create, code, or otherwise produce" a GenAI system?
  The statute does not say; this decides whether every image-generating app we build must ship a verification tool.
  Until resolved, the skill should embed C2PA credentials and link to the upstream provider's verification tool, which 22757.2(e) allows only if that tool complies ([B&P 22757.2(e)](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260SB1000)).
- **EU provider status for apps built on a third-party model.** The Commission guidelines treat a company offering a chatbot or generator "under its own name" as the provider ([Guidelines para. 11](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2026-07/guidelines_on_the_implementation_of_the_transparency_obligations_for_certain_ai_systems_under_article_50_of_the_ai_act_bzptwqhk0ikg1dtlddap41psfy_131215.pdf)), but how much Art. 50(2) marking we must add on top of the upstream model's own watermark needs advice.
- **Art. 50(2) grace period for our existing apps.** Whether an app updated after 2 August 2026 is still "placed on the market before 2 August 2026" for the 2 December 2026 transitional date ([Reg. 2026/1744](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
- **DSA legal representative.** Whether a small US app with some EU users has a "substantial connection" and so needs an Art. 13 representative ([DSA Art. 3(e), 13](https://eur-lex.europa.eu/eli/reg/2022/2065/oj)).
- **EAA reach.** Whether a given consumer subscription app counts as "e-commerce services" (concluding a consumer contract at a distance) for its sign-up and payment flow, and how each Member State's transposition treats non-EU providers ([Directive 2019/882, Art. 3(30)](https://eur-lex.europa.eu/eli/dir/2019/882/oj)).
- **ADA Title III exposure.** With no DOJ web regulation for businesses, which courts treat app-only businesses (no physical location) as public accommodations, and what standard they apply, needs counsel; [ADA.gov web guidance](https://www.ada.gov/resources/web-guidance/) gives only DOJ's non-binding view.
- **512(c)(1)(B) "financial benefit".** Whether subscription or ad revenue on a UGC app is "directly attributable" to infringement is fact-specific ([17 U.S.C. 512(c)(1)(B)](https://www.law.cornell.edu/uscode/text/17/512)).
- **AGPL services.** Whether running an unmodified AGPL component (e.g. a database) behind our app, or a lightly configured one, triggers s.13 ([AGPL s.13](https://www.gnu.org/licenses/agpl-3.0.html#section13)).
- **Adobe Fonts and commercial font EULAs.** Re-read the live Adobe terms in a browser before any use, since helpx.adobe.com could not be fetched directly.
- **Utah renewal.** Whether the 2027 Utah session renews the AI Policy Act and changes its disclosure triggers ([Utah Interim Highlights](https://le.utah.gov/interim/2026/pdf/00003528.pdf)).
- **SB 243 scope.** Whether a general-purpose assistant with a persona in one of our apps is a "companion chatbot" or falls in the productivity exclusion ([B&P 22601](https://california.public.law/codes/ca_bus_and_prof_code_section_22601)).
