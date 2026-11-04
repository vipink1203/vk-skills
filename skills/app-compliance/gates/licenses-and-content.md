# Licenses and content gates

Code, fonts, images and icons we ship, and content our users provide.
Evidence: [`research/03-app-accessibility-ip-and-ai.md`](../research/03-app-accessibility-ip-and-ai.md) sections 3 to 6.

## LIC-1 Dependency licenses are allowed and attributed

- **Rule:** MIT, BSD and ISC need the copyright and permission notice to travel with every copy, minified bundles included; Apache-2.0 also needs its NOTICE file contents reproduced.
  MPL-2.0 is file-level: when MPL files ship in executable form (a browser bundle or app), their source must be available and recipients told how to get it, modified or not.
  GPL code that runs only on our servers needs no source release, but GPL code shipped to browsers or inside a mobile app does.
  AGPL-3.0 requires offering source to network users once we modify it.
  SSPL, BUSL (BSL) and the Elastic License are source-available, not OSI-approved open source.
- **Build:** Allowed by default: MIT, BSD-2-Clause, BSD-3-Clause, ISC, Apache-2.0, OFL-1.1 (fonts), and MPL-2.0 used unmodified with a source link in the notices.
  Owner sign-off required, recorded once per license and then added to the project's allow list: any other license, including other permissive ones, plus LGPL, GPL in server-only code, and AGPL as an unmodified separate service.
  Blocked: GPL or AGPL in client bundles or mobile binaries, AGPL in our request path, SSPL, BUSL and Elastic in production, unlicensed code.
  CI fails on anything outside the allow list: `license-checker-rseidelsohn --production --onlyAllow '...'` for Node (the original `license-checker` is unmaintained since 2019), `pip-licenses --allow-only=...` for Python, and the platform's license report for native mobile dependencies.
  Generate an SBOM (`npm sbom --sbom-format spdx --omit dev`) and ship `THIRD_PARTY_NOTICES.txt` (plus an "Open source licenses" screen on mobile) with each component's name, version, SPDX ID, copyright lines, full license text, verbatim Apache NOTICE contents, and source links for MPL files.
  Scan vendored or copied code and CDN-loaded scripts with ScanCode, since no manifest describes them.
- **Done when:** the license check runs in CI and passes for every package ecosystem in the app; ScanCode has been run on vendored code and CDN scripts with results in the record; every sign-off item has an owner decision; MPL files are unmodified (diff against the published package); and the notices file is generated from the SBOM and reachable from the shipped app.

## LIC-2 Fonts are licensed for how we use them

- **Rule:** SIL OFL 1.1 allows bundling and web serving with the copyright and license included; subsetting counts as modification, so a subset font with Reserved Font Names must be renamed.
  Google Fonts families are OFL, Apache-2.0 or the Ubuntu Font License: check each family.
  Adobe Fonts' own help pages could not be read during research; quoted excerpts say they cannot be self-hosted or embedded in mobile or desktop apps.
- **Build:** Default to self-hosted OFL or Apache fonts, with their license files in the notices.
  Never copy a font file from a Creative Cloud sync folder or a desktop-only license into an app.
  Commercial or Adobe fonts only after the owner has read the current license terms in a browser and filed the license.
- **Done when:** every font file in the build has its license recorded, and subset fonts with Reserved Font Names are renamed.

## LIC-3 Images and icons are licensed

- **Rule:** Unsplash photos need no attribution but cannot be sold without significant modification or compiled to replicate a similar or competing service; CC BY needs attribution and a mark of changes; CC NC is unusable in a monetised app; CC ND forbids edits.
  Font Awesome Free splits licenses: icons are CC BY 4.0, font files OFL, code MIT; its embedded attribution comments must survive the build.
  Lucide is ISC, Heroicons MIT.
  Purely AI-generated images get no US copyright (Thaler v. Perlmutter stands; cert denied 2 March 2026), so competitors may copy them.
  Photos showing identifiable people or trademarks need separate judgment, since the Unsplash license does not address model or property releases.
- **Build:** An asset register in the compliance record: each image, icon set and illustration with its source URL, license, attribution text and where it appears.
  CC BY attributions shown on a credits page; Font Awesome listed in the notices file.
  Photos with identifiable people or brands go to the owner for a release decision.
- **Done when:** every asset file in the build has a register row with an allowed license, no NC or ND asset is used or edited, and every photo with identifiable people or brands has an owner decision.

## UGC-1 User content can be reported and taken down (only if the app stores content users provide)

- **Rule:** Applies when users can upload or post anything we store and serve: posts, comments, files, images, profiles, avatars.
  The DMCA 512(c) safe harbor needs a designated agent registered with the US Copyright Office ($6, online only, expires after 3 years, listing every domain and app name the public uses), published on the site, expeditious removal on notice, a counter-notice flow, and a repeat-infringer policy that is actually enforced.
  The EU DSA requires any hosting service to offer an electronic notice mechanism for illegal content, confirm receipt, decide diligently, notify the decision with redress options, give the affected user a statement of reasons, and publish a single point of contact; a non-EU provider offering services in the EU must designate an EU legal representative.
- **Build:** A `/legal/copyright` page with the agent's name, address, phone and email and the notice requirements.
  A "Report" control on user content, feeding two flows.
  Copyright: notice received, content disabled, uploader notified, counter notice, complainant forwarded, restore 10 to 14 business days later unless suit is filed, strike recorded, account terminated on reaching the repeat-infringer threshold set in the terms.
  Other illegal content (DSA): receipt confirmed, decision made and recorded, notifier told the outcome and redress options, uploader sent a statement of reasons.
  The DSA single point of contact listed on the imprint page (BIZ-1).
- **Done when:** end-to-end tests run both flows, including a counter notice with scheduled restore and an account reaching the strike threshold and being terminated; the owner has registered the DMCA agent with every domain and app name, and its expiry date is in the record; whether an EU legal representative is needed is recorded as an owner question; or the record marks n/a because the app stores no user-provided content.
