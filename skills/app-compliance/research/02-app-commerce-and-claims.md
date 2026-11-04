# 02 - App Commerce and Marketing Claims Compliance

Research date: 2026-10-31.
Scope: rules an AI coding agent must apply to every small web or mobile app we ship (indie or SaaS, US-based owner, users in the US, EU/UK and elsewhere), covering terms acceptance, subscriptions, refunds, pricing, urgency, reviews, claims, security badges, logos, business identity, marketing email and uptime promises.
Every claim links to its source, usually the statute, regulation, court opinion or regulator page itself.
Where only a secondary source (law firm, vendor) was available, the text says so.
"Derived" marks an engineering practice we infer from the law, not something the law states.
"Unconfirmed" marks anything a primary source did not state.
This is research, not legal advice.

## Answer first

| Topic | Binding rule today (2026-10-31) | Biggest trap |
| --- | --- | --- |
| Terms acceptance | Case law: reasonably conspicuous notice plus an action the user is explicitly told means assent [chabolla] | A footer "Terms" link (browsewrap) or a button whose text does not say clicking means agreeing |
| Subscriptions (US) | ROSCA [rosca]; state laws, strongest is California as amended by AB 2863 [bpc17602] | The FTC click-to-cancel rule is vacated and the CFR text was rolled back [cfr425] |
| Subscriptions (EU) | 14-day withdrawal right [crd]; withdrawal function from 19 June 2026 [d2673] | SaaS is a "service", so the right exists until the service is fully performed [crd] |
| Refunds | No general US duty; CA Civ 1723 only for goods [civ1723]; EU withdrawal [crd] | Store refunds are run by Apple, not you [apple-refund] |
| Fees / drip pricing | FTC Fees Rule only for live-event tickets and short-term lodging [ftc-fees-faq]; California SB 478 for almost all consumer prices [civ1770] | Showing the total only at checkout does not comply in California [ca-ag-fees] |
| Fake urgency | EU UCPD Annex I item 7 [ucpd]; UK DMCC Sch 20 para 7 [dmcc-sch20]; FTC Act Section 5 [ftc-dark] | A timer that resets is a false limited-time claim |
| Reviews | FTC Rule 16 CFR 465, civil penalties up to $53,088 per violation [ftc-review-warn] | Paying for reviews conditioned on positive sentiment [ftc-reviews-qa] |
| Claims | Reasonable basis before the claim runs [ftc-subst] | "AI-powered", "98% accurate", "HIPAA compliant" without evidence [workado][ftc-hipaa] |
| SOC 2 | A CPA attestation report, not a certification [aicpa-soc2-guide] | "SOC 2 certified" |
| Logos | Lanham Act false association [lanham] | Logo of a trial user or a former customer |
| Business identity | EU E-Commerce Directive Art 5 [ecd]; Germany DDG section 5 [ddg5]; UK reg 6 [uk-ecr6] | Old "section 5 TMG" and the EU ODR link, both obsolete [odr-repeal] |
| Marketing email | CAN-SPAM [ftc-canspam]; Gmail/Yahoo bulk rules [gmail][yahoo]; EU/UK consent [eprivacy][pecr22] | Gmail and Yahoo expect unsubscribes honored in about 2 days, far faster than CAN-SPAM's 10 business days |
| Uptime | No statute; FTC deception covers "failure to perform promised services" [ftc-deception] | Marketing "99.99% uptime" without measurement or a contractual SLA |

## 1. Terms of service enforceability

### The legal test

Courts apply ordinary contract formation to online terms: there must be notice of the terms and the user must manifest assent [chabolla].
The Ninth Circuit test for sign-in wrap: the site gives "reasonably conspicuous notice of the terms" and the user "takes some action, such as clicking a button or checking a box, that unambiguously manifests his or her assent to those terms" [chabolla].
Berman v. Freedom Financial Network, 30 F.4th 849 (9th Cir. 2022), says New York and California rules are "substantially similar", citing Meyer v. Uber, 868 F.3d 66 (2d Cir. 2017) [chabolla].
Meyer enforced Uber's app sign-up terms, judging notice from the view of a reasonably prudent smartphone user [meyer].

The four patterns, as the Ninth Circuit describes them [chabolla]:
- Browsewrap: the user supposedly accepts by browsing; "Courts consistently decline to enforce browsewraps."
- Clickwrap: the user clicks or checks a box stating she agrees; "Courts routinely enforce clickwraps."
- Scrollwrap: the user must scroll through the terms before agreeing; it gives "the strongest notice."
- Sign-in wrap: a link to terms plus text saying an action binds the user, without requiring review; enforceable only if both prongs are met.

### What "conspicuous notice" requires in UI terms

The notice "must be displayed in a font size and format such that the court can fairly assume that a reasonably prudent Internet user would have seen it" (quoting Berman) [chabolla].
"Website users are entitled to assume that important provisions ... will be prominently displayed, not buried in fine print" (Berman) [chabolla].
A hyperlink "must be readily apparent", and "simply underscoring words or phrases ... will often be insufficient" (Berman, via Keebaugh) [chabolla].
Blue link text has been accepted, but there is "no bright-line test"; the court looks at how the element appears on the whole page [chabolla].
Small gray text on a white background, away from the action button, failed in Chabolla v. ClassPass (9th Cir. Feb. 27, 2025) [chabolla].
Context matters: a simple, one-off transaction does not alert a user to look for extra terms [chabolla].

### What "unambiguous assent" requires

"A user's click of a button can be construed as an unambiguous manifestation of assent only if the user is explicitly advised that the act of clicking will constitute assent" (Berman) [chabolla].
Berman rejected "I understand and agree to the Terms & Conditions" next to buttons labelled "This is correct, Continue!" because the text did not say which action meant assent [chabolla].
Chabolla rejected "By signing up you agree..." where no button said "Sign up", and "I agree to the Terms" above a "Redeem now" button [chabolla].
The fix the court itself gave: "By clicking the Continue >> button, you agree to the Terms & Conditions" [chabolla].
Wording upheld in the Ninth Circuit: "By tapping 'Play' I agree to the Terms of Service" (Keebaugh), and "by clicking on this button, you agree to our Terms of Use" (Oberstein) [chabolla].

Implementable pattern (derived from the cases above):
- Put the notice directly above or below the action button, same visual block, body-size text, high contrast.
- Name the exact button in the sentence: "By clicking **Create account**, you agree to the [Terms of Service] and acknowledge the [Privacy Policy]."
- Style links as obvious links (color plus underline), not just underline.
- Best: an unchecked checkbox "I agree to the [Terms of Service]" that must be ticked before the button enables (clickwrap, "routinely" enforced) [chabolla].
- Repeat the notice on every screen where an account or payment is created, with the same button-naming wording; do not rely on a multi-screen "flow" adding up [chabolla].
- Never rely on a footer link alone (browsewrap) [chabolla].

### What to record as proof of acceptance (derived)

No statute lists these fields; courts decide on the screens actually shown, so the record must let us reproduce them.
Store, per acceptance event, in an append-only table:
- `user_id`, `account_email` at the time.
- `document_type` (terms, privacy acknowledgment, subscription terms) and `document_version` (immutable ID or content hash of the exact text).
- `accepted_at` in UTC, server-side timestamp.
- `ip_address`, `user_agent`, platform and app version.
- `ui_surface` (screen ID) and `ui_version` (build or commit), plus the exact notice string and button label rendered.
- `method` (checkbox plus button, button only) and `locale`.
- Keep an archived, retrievable copy of every terms version and a screenshot of each acceptance screen per UI version.
California requires subscription consent records to be kept "at least three years, or one year after the contract is terminated, whichever period is longer" [bpc17602]; use that as the floor for all acceptance records.

### Changes to terms

Posting revised terms on a website without notice does not bind existing customers; a revised contract is only an offer they must know about and accept (Douglas v. U.S. District Court, 495 F.3d 1062 (9th Cir. 2007), per secondary summaries) [douglas].
FTC staff warn that adopting more permissive data practices "through a surreptitious, retroactive amendment" to terms or a privacy policy may be unfair or deceptive (Feb. 13, 2024) [ftc-tos-change].
For subscriptions, California requires "clear and conspicuous notice of the material change" plus how to cancel [bpc17602], and New York requires notice of material changes 5 business days to 30 days before the change [ny527a].

Implementable pattern (derived):
- Material change: email notice in advance plus a blocking in-app re-acceptance (clickwrap) on next sign-in; record it as a new acceptance event.
- Never apply new data uses retroactively to data collected under old terms without fresh consent [ftc-tos-change].
- Non-material change: notice banner and changelog; still version the document.

## 2. Subscriptions, auto-renewal and cancellation

### US federal: ROSCA (binding)

ROSCA, 15 U.S.C. 8403, applies to anyone charging consumers online through a negative option feature [rosca].
It requires three things [rosca]:
- "text that clearly and conspicuously discloses all material terms of the transaction before obtaining the consumer's billing information";
- "express informed consent before charging" the card or account;
- "simple mechanisms for a consumer to stop recurring charges".
The FTC enforces it hard: Amazon paid a $1 billion civil penalty plus $1.5 billion in refunds over Prime enrollment and cancellation (Sept. 25, 2025) [ftc-amazon].

### US federal: the "click-to-cancel" rule is dead, rulemaking restarted

The Eighth Circuit vacated the 2024 amended Negative Option Rule on July 8, 2025 in Custom Communications v. FTC, on procedural grounds, before its July 14, 2025 compliance date (secondary summaries; the court's judgment says the rule "is vacated") [8th-cir].
The FTC then conformed the CFR: 16 CFR part 425 now cites 91 FR 6509 (Feb. 12, 2026), restoring the old prenotification-plan rule [cfr425].
On March 11, 2026 the FTC issued a new Advance Notice of Proposed Rulemaking asking whether to amend the rule, including whether to adopt provisions of the vacated rule [ftc-anprm].
No proposed rule has been found as of 2026-10-31 (unconfirmed beyond law-firm reporting).
So the binding federal rules are ROSCA and FTC Act Section 5, not click-to-cancel.

### California Automatic Renewal Law (Bus. & Prof. Code 17600 et seq.), as amended by AB 2863

Applies to a business making an automatic renewal or continuous service offer to a consumer in California [bpc17602].
"Consumer" means an individual acquiring goods or services "for personal, family, or household purposes", so pure B2B plans are outside it [bpc17601].
The AB 2863 amendments apply to contracts "entered into, amended, or extended" on or after July 1, 2025 [bpc17602].
Free-to-pay trials are covered [bpc17601].

Before the purchase:
- Show the auto-renewal terms "in a clear and conspicuous manner ... in visual proximity" to the consent request [bpc17602].
- The terms are: continues until cancelled; the cancellation policy; the recurring charge and whether and to what it may change; the renewal term length; any minimum purchase [bpc17601].
- "Clear and conspicuous" means larger type, contrasting type or color, or set off by symbols so it "clearly calls attention to the language" [bpc17601].
- For a trial, explain "the price that will be charged after the trial ends" [bpc17602].
- Get "affirmative consent to the agreement" and separately "express affirmative consent to the automatic renewal ... offer terms" [bpc17602]; a dedicated unchecked checkbox next to the renewal terms is the usual way to show this (derived).
- Nothing in the contract may undermine that consent [bpc17602].
- Keep verification of consent for 3 years or 1 year after termination, whichever is longer [bpc17602].

After the purchase:
- Send an acknowledgment "capable of being retained" (email) with the terms, cancellation policy and how to cancel; for trials, how to cancel before paying [bpc17602].
- Trials or promo prices lasting over 31 days: notice 3 to 21 days before the trial or promo ends [bpc17602].
- Initial term of one year or longer: notice 15 to 45 days before renewal [bpc17602].
- Those notices must state that it renews, the term, the amount and frequency, how to cancel, a cancellation link if sent electronically, and business contact information [bpc17602].
- Price increase: notice "no less than 7 days and no more than 30 days" before it takes effect, plus how to cancel [bpc17602].
- Material change of terms: clear and conspicuous notice plus how to cancel [bpc17602].
- Annual reminder with the product, the frequency and amount of charges, and how to cancel, sent in the same medium [bpc17602].
  The text says "a consumer under an annual automatic renewal agreement or continuous service agreement"; whether monthly plans are covered is ambiguous, so send it yearly to every California subscriber (derived).

Cancellation:
- If the user can sign up online, they must be able to cancel "exclusively online, at will", via "a prominently located direct link or button" in account or settings, or a prefilled termination email [bpc17602].
- You may require sign-in, but a user who cannot authenticate must still be able to cancel another way [bpc17602].
- Save offers online are allowed only if a "prominently located and continuously and proximately displayed direct link or button entitled 'click to cancel'" is shown alongside them [bpc17602].
- Cancellation must be available in the same medium used to sign up [bpc17602].

### Other US states (brief)

New York GBL 527-a, amended effective November 2025: cancellation "as easy to use" as sign-up and in "the same medium"; material change notice 5 business days to 30 days before; price increases need new consent or a cancel window with pro-rata refund; renewal notices for terms of a year or more and for trials over a month [ny527a].
Secondary sources say the amended NY law likely reaches B2B subscriptions (unconfirmed) [ny-b2b].
Minnesota: annual written notice "at least once per calendar year via mail or email" for continuous service [mn57]; an online "termination election" that asks only for information needed to cancel [mn60].
Secondary sources report Massachusetts AG regulations (940 CMR 38.00, Sept. 2025), Virginia amendments (July 1, 2026), Colorado (Feb. 2026) and Louisiana (Jan. 1, 2027) (unconfirmed against primary text) [state-roundup].
Practical rule (derived): build to the California standard everywhere; it covers most of the others.

### EU: 14-day withdrawal right

Consumers have "a period of 14 days to withdraw from a distance ... contract, without giving any reason" [crd].
For services the period runs from the day the contract is concluded [crd].
The trader must refund "all payments ... not later than 14 days" after notice of withdrawal, using the same payment method [crd].
Exceptions [crd]:
- Services (16(a)): only after "the service has been fully performed", and only if performance began with "prior express consent and acknowledgement" that the right will be lost on full performance.
- Digital content not on a tangible medium (16(m)): lost once supply begins, but only with prior express consent, acknowledgment of losing the right, and a confirmation on a durable medium.
A SaaS subscription is a service that is not "fully performed" in 14 days, so the right exists; if the user expressly asked to start immediately, they owe a pro-rata amount on withdrawal [crd].
Without that express request and the withdrawal information, the consumer owes nothing for the service used [crd].
A free trial converting to paid gives only one withdrawal right, at the start, unless the price information was inadequate (CJEU C-565/22 Sofatutor, Oct. 5, 2023, per court press release and commentary) [sofatutor].
The order button must say "order with obligation to pay" or an unambiguous equivalent, or the consumer is not bound [crd].
For subscriptions the pre-contract total price must include "the total costs per billing period" [crd].
UK keeps the same 14-day model and the digital-content consent rule in the Consumer Contracts Regulations 2013 [uk-ccr29][uk-ccr37].

Checkout UI for EU/UK consumers (derived from the above):
- Unchecked checkbox: "Start my subscription now. I understand I will pay for what I use if I withdraw within 14 days." (services)
- For one-off digital content: "I consent to immediate delivery and acknowledge I lose my right of withdrawal once delivery starts."
- Order button: "Subscribe and pay" or "Buy now" style label that states payment; avoid "Continue" or "Start".
- Confirmation email containing the terms and the consent given.

### EU: withdrawal function ("withdrawal button"), from 19 June 2026

Directive (EU) 2023/2673 inserts Article 11a into the Consumer Rights Directive; member states had to transpose by 19 December 2025 and "apply those measures from 19 June 2026" [d2673].
It applies to "distance contracts concluded by the means of an online interface", only where a withdrawal right exists [d2673].
Requirements [d2673]:
- A withdrawal function "labelled with the words 'withdraw from contract here' or an unambiguous corresponding formulation".
- "Continuously available throughout the withdrawal period", "prominently displayed" and "easily accessible".
- It lets the consumer send an online statement with name, contract identification, and where the confirmation should go.
- A confirmation step labelled "only with the words 'confirm withdrawal'" or an unambiguous equivalent.
- An acknowledgment of receipt "on a durable medium, including its content and the date and time of its submission, without undue delay".
- The withdrawal counts if submitted before the period ends.
Secondary sources report some member states (for example Belgium) transposed late; the national law of the consumer's country is what applies (unconfirmed per country) [d2673-commentary].

### UK subscription regime (not yet in force)

The DMCC Act 2024 subscription contracts regime has draft regulations listing 1 January 2027 as commencement [uk-sub-si], and the Prime Minister announced a January 2027 start [uk-sub-pm].
Earlier government statements said spring 2027, so treat the date as likely but not final [uk-sub-pm].

### Subscription backend records (derived)

Per subscription: offer terms version, price, period, trial end, consent event (checkbox ID, text version, timestamp, IP), acknowledgment email ID, every reminder sent (type, sent_at, channel, content version), price-change notices, cancellation request time and channel, cancellation effective time, refund issued.

## 3. Refund policy

### US

No federal statute requires a general refund policy; ROSCA only requires disclosure of material terms, consent and simple cancellation [rosca].
California Civil Code 1723 applies only to retail sellers of goods whose policy gives less than a full refund, credit or exchange within 7 days; they must conspicuously display the policy (time limit, what is covered, conditions) [civ1723].
If they fail, the buyer can return the goods for a refund within 30 days [civ1723].
It does not apply to services or software subscriptions, which are not "goods" in its text (derived from the statute's wording) [civ1723].
A stated refund policy must be honored; the FTC lists "failure to perform promised services" and false refund promises as deception [ftc-deception][ftc-ai-comply].
Operation AI Comply targets included "false refund guarantees" (FBA Machine) [ftc-ai-comply].

### EU/UK

The 14-day withdrawal right with refund within 14 days is mandatory for consumer distance contracts (section 2) [crd][uk-ccr29].

### App stores

Apple processes refunds for In-App Purchases; customers ask Apple Support, use reportaproblem.apple.com, or their card issuer, and your server receives a REFUND notification [apple-refund].
The developer must revoke the entitlement and handle the transaction on receipt [apple-refund].
Google Play: within 48 hours of purchase a buyer may get a refund through Google; after that Google directs them to the developer [gplay-refund].
Google says developers must set and follow their own refund policy and ensure it complies with law; refunds are issued in Play Console or via the orders API [gplay-dev-refund].
Google and developers share chargeback costs for orders after 3 August 2026 [gplay-chargeback].

Implementable (derived): publish one refund page linked from checkout and the footer; for EU/UK consumers state the 14-day right; for store purchases say refunds go through Apple or Google and link to their process.

## 4. Hidden fees and drip pricing

### FTC Rule on Unfair or Deceptive Fees (16 CFR 464)

Effective May 12, 2025 [ftc-fees-faq].
Scope: only businesses that offer, display or advertise live-event tickets or short-term lodging [ftc-fees-faq].
Requirement: any price shown must come with the "total price" disclosed clearly and conspicuously and "more prominently than any other pricing information" [cfr464-2].
Only government charges, shipping and optional add-ons may be excluded from the total, and they must be disclosed before payment [ftc-fees-faq][cfr464-2].
Outside those two industries, drip pricing is still policed under FTC Act Section 5 [ftc-dark].

### California SB 478 (Civil Code 1770(a)(29))

Unlawful to advertise, display or offer "a price for a good or service that does not include all mandatory fees or charges" other than government taxes/fees and actual shipping costs [civ1770].
Operative July 1, 2024 [civ1770].
Applies to most consumer goods and services; not to purchases for commercial use [ca-ag-fees].
The AG: "The advertised or listed price must be the full price that the consumer is required to pay." [ca-ag-fees]
Disclosing required fees before the consumer finalizes the transaction does not comply; show the total first [ca-ag-fees].
A credit card fee is mandatory if card is the only way to pay [ca-ag-fees].
Restaurants have a separate exemption under SB 1524 [ca-ag-fees].

### EU and UK price rules

The pre-contract price must be the "total price ... inclusive of taxes", and for subscriptions "the total costs per billing period" [crd].
An invitation to purchase must state "the price inclusive of taxes" [ucpd].
Any announced price reduction must show the prior price, meaning "the lowest price applied by the trader during a period of time not shorter than 30 days" (Price Indication Directive Art 6a, applies to goods) [pid].
UK: the DMCC Act regime in force since April 2025 bans drip pricing and lets the CMA fine up to 10% of global turnover [cma-dmcc][cma207].
UK prices online must say whether they include tax and delivery [uk-ecr6].

Implementable (derived): every displayed price is the all-in amount the user will pay per period (excluding only sales tax/VAT where law allows in the US, and shipping); show VAT-inclusive prices to EU/UK consumers; strike-through prices only with a real 30-day lowest prior price on record.

## 5. Fake countdown timers and false urgency or scarcity

FTC staff report "Bringing Dark Patterns to Light" (Sept. 15, 2022) names countdown timers that suggest "they only have a limited time to purchase" when "the offer is not actually time-limited" [ftc-dark-pr].
Its appendix lists "Baseless Countdown Timer" (a clock that resets or disappears when it runs out) and false low-stock and false high-demand messages [ftc-dark].
These are judged under FTC Act Section 5 deception; we found no FTC case built solely on a timer [ftc-dark].
EU: always unfair is "Falsely stating that a product will only be available for a very limited time, or ... on particular terms for a very limited time, in order to elicit an immediate decision" (UCPD Annex I item 7) [ucpd].
UK: the same ban is DMCC Act Schedule 20 paragraph 7 [dmcc-sch20].
EU DSA Article 25 bars online platforms from interfaces that deceive or manipulate users, and lets the Commission address giving more prominence to some choices, repeated prompts, and making cancellation harder than signup [dsa].
Article 25 does not apply to practices already covered by the UCPD or GDPR [dsa], and does not apply to micro or small platforms [dsa19].

Implementable (derived):
- A timer may show only a real deadline stored server-side; when it hits zero, the offer ends for everyone and does not restart per visit.
- Stock or "N people viewing" messages only from real live data.
- No preselected upsells, no confirmshaming copy, no extra friction on cancel compared to signup.

## 6. Fake reviews and testimonials

### FTC Consumer Reviews and Testimonials Rule (16 CFR 465)

In effect since October 21, 2024 [ftc-reviews-qa].
Sections [cfr465][ftc-reviews-qa]:
- 465.2: no writing, creating or selling fake or false consumer reviews, consumer testimonials or celebrity testimonials; no knowingly using them.
- 465.4: no compensation conditioned on a review's sentiment.
- 465.5: insider reviews (officers, employees, relatives) need clear and conspicuous disclosure of the relationship.
- 465.6: no presenting a company-controlled review site as independent.
- 465.7: no review suppression by threats, intimidation or false accusations.
- 465.8: no buying or selling fake social media indicators (followers, views) the business knew or should have known were fake.
Incentives for reviews are allowed "as long as there isn't an express or implied requirement that the reviews have to express a particular sentiment" [ftc-reviews-qa].
Sorting by helpfulness is fine; filtering is fine only on neutral grounds applied to positive and negative reviews alike [ftc-reviews-qa].
Penalty: up to $53,088 per violation [ftc-review-warn]; that figure stays in force for 2026 because the FTC made no 2026 inflation adjustment [ftc-penalty-2026].
First public enforcement: warning letters to 10 companies on December 22, 2025 [ftc-review-warn].
The FTC set aside its 2024 Rytr order (AI review generator) on December 22, 2025 [ftc-rytr], but the rule's ban on fake reviews is unaffected.
Verkada's 2024 settlement included undisclosed five-star reviews by employees and an investor [ftc-verkada].

### FTC Endorsement Guides (16 CFR 255, revised 2023)

Revised guides published at 88 FR 48092 (July 26, 2023); they are guidance, not a rule [ftc-endorse-2023].
An endorsement is any message consumers likely believe reflects the views of someone other than the advertiser [cfr255-0].
Testimonials about key attributes imply typical results; "Results not typical" does not cure that, and you must disclose generally expected performance [cfr255-2].
Use actual customers or clearly disclose actors [cfr255-2].
Do not procure, suppress, boost, organize or edit reviews so they distort what consumers think [cfr255-2].

### EU and UK

When a trader gives access to reviews, how it ensures they come from real users is "material" information that must be disclosed [ucpd].
Banned in all cases: saying reviews come from real users without "reasonable and proportionate steps to check", and submitting or commissioning fake reviews or misrepresenting reviews (Annex I 23b, 23c) [ucpd].
UK bans submitting or commissioning fake reviews (DMCC Act Sch 20 para 13) [dmcc-sch20], with CMA guidance CMA208 [cma208].

Implementable (derived): show only reviews tied to a verified account or order; label incentivized reviews; label employee reviews; publish a short "How we verify reviews" note next to reviews (EU); never seed reviews from staff or AI; moderation rules applied equally to negative and positive.
Testimonials with a person's name or photo need that person's prior consent in California [civ3344].

## 7. Unsupported claims (performance, AI, Made in USA, health)

### General substantiation

"Firms lacking a reasonable basis before an ad is disseminated violate Section 5" (FTC Substantiation Policy, Nov. 23, 1984) [ftc-subst].
If an ad claims a level of support ("tests prove"), the firm must have "at least the advertised level of substantiation" [ftc-subst].
Deception: a representation, omission or practice "likely to mislead the consumer", judged from a consumer "acting reasonably", that is material (Deception Policy Statement, Oct. 14, 1983) [ftc-deception].

### AI capability claims

Operation AI Comply (Sept. 25, 2024): "there is no AI exemption from the laws on the books"; cases included DoNotPay's "robot lawyer" claims made without testing against lawyers [ftc-ai-comply].
Workado (Apr. 28, 2025): advertised "98 percent" AI-detection accuracy; independent testing found 53% on general content; the order requires competent and reliable evidence for effectiveness claims [workado].
In 2026 the FTC kept acting on false AI claims: Air AI (Mar. 2026) and Cox Media Group's "active listening" AI service (orders finalized Aug. 2026) [ftc-ai-hub].
The FTC set aside the Rytr order, citing the federal AI Action Plan [ftc-rytr]; that signals less appetite for "means and instrumentalities" theories, not tolerance of false capability claims (derived).

### Made in USA

16 CFR 323 (86 FR 37032, July 14, 2021): a "Made in USA" label is unlawful unless final assembly or processing is in the US, all significant processing is in the US, and "all or virtually all ingredients or components" are made and sourced in the US [cfr323-2].
It reaches online sales material because "mail order promotional material" includes materials "disseminated in print or by electronic means" [cfr323-1][cfr323-3].
A software app is rarely a "product" for this rule, but merchandise and hardware are (derived).

### Health claims

Health-related claims need "competent and reliable scientific evidence", generally "randomized, controlled human clinical testing" [ftc-health].
The guidance covers apps and devices, with an acne-treatment app as an example [ftc-health].

### EU green claims

From 27 September 2026, EU member states must apply Directive (EU) 2024/825, which bans generic environmental claims without recognized excellent environmental performance [d825].

Implementable (derived): the agent must not write numeric performance, accuracy, speed, savings, "AI-powered", health, environmental or origin claims into marketing copy unless a dated evidence file (test method, dataset, results) exists in the repo; otherwise use qualitative, verifiable wording.

## 8. SOC 2 and security or compliance claims

### What SOC 2 is

SOC is "a suite of service offerings CPAs may provide" on controls at a service organization [aicpa-soc].
A SOC 2 is an "Assertion-based examination of a service organization's description of its system" and its controls relevant to security, availability, processing integrity, confidentiality or privacy [aicpa-soc2-guide].
It is an attestation report by an independent CPA firm, not a certification; there is no "SOC 2 certified" status (derived from the AICPA description) [aicpa-soc2-guide].
Type 1 covers the design of controls at a point in time; Type 2 adds operating effectiveness over a period; the free AICPA pages we could read do not define these, so this is the practitioner reading of the paywalled AICPA guide (unconfirmed against AICPA text) [aicpa-soc2-guide].
SOC 3 reports are "general use reports and can be freely distributed" because they lack SOC 2's detail [aicpa-soc3]; SOC 2 reports are typically shared under NDA (practice).
The AICPA proposed revised 2027 Trust Services Criteria on Oct. 28, 2026, effective for engagements on or after Dec. 31, 2027 if adopted [aicpa-2027].
The AICPA is looking into allegations about a compliance vendor's SOC practices and urges that SOC services be "thoroughly evaluated" [aicpa-soc].

### FTC enforcement on false security and compliance claims

Zoom (2020): claimed "end-to-end, 256-bit encryption" while holding the keys and using 128-bit AES; order bars security misrepresentations [ftc-zoom].
Verkada (Aug. 30, 2024): misled consumers about HIPAA compliance and Privacy Shield compliance, plus fake reviews and CAN-SPAM; $2.95 million penalty [ftc-verkada].
Monument (2024 complaint): advertised itself as HIPAA compliant when it was not [ftc-monument].
The FTC tells businesses to avoid false claims that they are "HIPAA Compliant," "HIPAA Secure," "HIPAA Certified" or the like [ftc-hipaa].
Privacy Shield: at least 17 FTC actions against companies falsely claiming participation, including lapsed certifications still advertised [ftc-ps-medable][ftc-ps-2018].
EU: displaying a trust mark without authorization, or claiming approval by a body that did not give it, is always unfair [ucpd].

### Safe wording (derived)

| Situation | Allowed wording | Never |
| --- | --- | --- |
| Completed SOC 2 Type II, current period | "SOC 2 Type II report available on request under NDA" | "SOC 2 certified", "SOC 2 compliant" |
| Audit in progress | "SOC 2 Type II audit in progress; expected {quarter}" only if an engagement letter exists | Showing the AICPA SOC badge |
| No audit | Describe actual controls: "Data encrypted at rest with AES-256 via {provider}" | Badges for SOC 2, ISO 27001, HIPAA, GDPR |
| Hosted on a certified cloud | "Hosted on {provider}, which holds {cert}" | Implying the cloud's certification is ours |
| HIPAA | "We sign BAAs" only if true | "HIPAA certified" (no such certification) [ftc-hipaa] |
| GDPR | "We process EU data under GDPR; see our DPA" | "GDPR certified" |
| EU-US transfers | "Self-certified to the EU-U.S. Data Privacy Framework" only while listed and current | Lapsed or never-completed participation [ftc-ps-2018] |

Every security claim needs an evidence pointer (report, config, contract) and a re-check date; remove the claim when the evidence lapses.

## 9. Customer logos and "trusted by" sections

Lanham Act 15 U.S.C. 1125(a)(1)(A) creates civil liability for using a name, symbol or mark in a way "likely to cause confusion, or to cause mistake, or to deceive" about affiliation, sponsorship or approval [lanham].
Section 1125(a)(1)(B) covers false or misleading claims in advertising about goods or services [lanham].
A customer logo implies an organization's endorsement; FTC guides treat organizational endorsements as "representing the judgment of a group" [cfr255-4].
An endorsement is any message consumers likely read as the views of a party other than the advertiser [cfr255-0].
No statute we found requires written permission to show a customer logo; written permission is the practical defense against a false-association claim and is often required by the customer's contract (derived; contract terms vary).
Individuals' names, photos or likeness in ads need prior consent in California [civ3344].

Implementable (derived):
- Show a logo only for a current paying customer who gave written permission (email is fine), stored with date and scope.
- Remove logos within a set period after a customer churns or revokes.
- "Trusted by" counts must be true and dated ("Used by 1,200 teams as of Oct 2026").
- No logos of free-trial users, investors, partners or press mentions presented as customers.

## 10. Business contact details

### EU (E-Commerce Directive Art 5) and consumer contracts

Information society service providers must make "easily, directly and permanently accessible": name, geographic address, contact details "including his electronic mail address", trade register and number, supervisory authority if licensed, professional details if regulated, and VAT number if any [ecd].
Before a consumer distance contract: trader identity, "the geographical address at which the trader is established as well as the trader's telephone number and email address" [crd].
The EU ODR platform link obligation ended when Regulation (EU) 2024/3228 repealed the ODR Regulation with effect from 20 July 2025; remove ODR links [odr-repeal].

### Germany: Impressum under DDG section 5

The Digitale-Dienste-Gesetz replaced the Telemediengesetz on 14 May 2024, with section 5 TMG content carried into section 5 DDG (secondary sources) [ddg-date].
Business-like, usually paid digital services must keep "leicht erkennbar, unmittelbar erreichbar und ständig verfügbar": name and address, legal form and authorized representative for companies, fast electronic contact including email, supervisory authority, register and number, VAT ID, profession details if regulated [ddg5].
Missing or incorrect information is an administrative offense with fines up to EUR 50,000 [ddg33].
Replace any "Angaben gemäß § 5 TMG" with § 5 DDG or no citation [ddg-date].

### UK (Electronic Commerce Regulations 2002, reg 6)

Same list: name, geographic address, email and contact details, register number, supervisory authority, regulated profession details, VAT number [uk-ecr6].
Prices must be clear and say whether they include tax and delivery [uk-ecr6].

### US

CAN-SPAM: every commercial email needs a valid physical postal address; a USPS-registered PO box or a registered private mailbox is acceptable [ftc-canspam].
California Civil Code 1789.3: a provider of an "electronic commercial service" must give consumers its name, address and phone, its charges, and complaint procedures including the Department of Consumer Affairs Complaint Assistance Unit, at contracting and annually [civ17893].
That statute's definition covers electronic shopping for "tangible items or physical services" and excludes "computerized data", so it likely does not reach pure SaaS (derived) [civ17892].
California's ARL requires contact information in renewal notices [bpc17602].

Implementable (derived): one `/legal/imprint` (Impressum) page linked from every page footer and the app's settings, with legal entity name, legal form, registered address, email, phone, representative, register number and VAT ID; reuse the same data in email footers and receipts.
Do not use a home address unless the owner accepts that; use a registered business address or virtual office.

## 11. Marketing email unsubscribe

### CAN-SPAM (15 U.S.C. 7704; 16 CFR 316)

Applies to all commercial email, including B2B; "primary purpose" decides whether a message is commercial or transactional [ftc-canspam].
Requirements [ftc-canspam]:
- Accurate header and From information; non-misleading subject line.
- Clear disclosure that the message is an ad (flexible wording).
- Valid physical postal address.
- A working opt-out for at least 30 days after sending; honor within 10 business days.
- No fee, no information beyond email address and preferences, nothing beyond a reply email or "a single page on an Internet website" [cfr316-5].
- No selling or transferring opted-out addresses.
- You cannot contract compliance away to your email vendor.
Penalty: up to $53,088 per email [ftc-canspam]; unchanged for 2026 [ftc-penalty-2026].

### Gmail and Yahoo bulk sender requirements

Gmail: since February 1, 2024, all senders to personal Gmail need SPF or DKIM, valid PTR, TLS and low spam rates [gmail].
Senders of 5,000+ messages a day to Gmail need SPF, DKIM and DMARC (p=none allowed) with From alignment, and one-click unsubscribe plus a visible unsubscribe link in marketing mail [gmail].
One-click means both headers: `List-Unsubscribe-Post: List-Unsubscribe=One-Click` and `List-Unsubscribe: <https://...>` (RFC 8058) [gmail].
Spam rate must stay below 0.30%; Google recommends below 0.10% [gmail].
Gmail recommends honoring unsubscribes within 48 hours and lists not doing so as a requirement issue [gmail-faq].
Transactional mail (password resets, receipts) is exempt from one-click [gmail-faq].
Since November 2025 Gmail is "ramping up its enforcement", including temporary and permanent rejections [gmail-faq].
Yahoo: SPF and DKIM, DMARC at least p=none, aligned From, one-click unsubscribe via RFC 8058, "Honor unsubscribes within 2 days", spam rate below 0.3% [yahoo].
Microsoft Outlook.com: senders over 5,000 a day need SPF, DKIM and DMARC p=none or stronger; non-compliant mail is rejected with 550 5.7.515 [outlook].

### EU and UK consent

EU: marketing email to individuals needs prior consent, except the soft opt-in for a trader's own customers about its own similar products, with an easy free opt-out at collection and in every message [eprivacy].
Every marketing email needs a valid address for opt-out and must not hide the sender [eprivacy].
Consent must be "freely given, specific, informed and unambiguous" by "a clear affirmative action", provable, and "as easy to withdraw as to give" [gdpr].
UK PECR reg 22: same consent rule and soft opt-in; since 5 February 2026 charities also have a soft opt-in [pecr22].
The ICO can now fine PECR breaches up to £17.5 million or 4% of global turnover [ico-duaa].

Implementable (derived):
- Signup: separate unchecked "Email me product news and offers" checkbox; never bundled with terms; log consent (text version, timestamp, IP, source).
- Existing customers (soft opt-in): offer the opt-out at signup and in every email.
- Every marketing email: one-click headers, visible unsubscribe link, postal address, honor within 24 hours (meets Gmail, Yahoo and CAN-SPAM).
- Keep a suppression list forever; send marketing only via a provider that sets the one-click headers and DKIM on our domain.

## 12. Uptime commitments and SLAs

No US federal or EU statute requires a consumer app to promise any uptime (none found).
Failure to deliver what you promised is deception: the FTC lists "failure to perform promised services" among deceptive practices [ftc-deception].
Claims need a reasonable basis when made [ftc-subst], so "99.99% uptime" in marketing needs measured history.

What a typical SLA contains, using AWS EC2 as the model [aws-sla]:
- The commitment (for example 99.99% region-level, 99.5% per instance) as a monthly uptime percentage.
- Measurement: 100% minus the percentage of minutes in the month the resource was "Unavailable", with "Unavailable" defined precisely.
- Credit tiers (10%, 30%, 100% of the monthly bill by band).
- Claim process and deadline (by the end of the second billing cycle after the incident), with required evidence.
- Exclusions: force majeure, internet problems outside the provider, customer actions, customer equipment, suspension.
- Credits as "sole and exclusive" remedy; credits are not refunds.

Implementable (derived):
- Marketing pages: no uptime number unless we publish a status page with measured history for at least the stated period; prefer "Live status at status.example.com".
- Never promise more than our dependencies' SLAs combined allow.
- If we sell an SLA, it lives in the contract with definitions, measurement source, exclusions, credits and claim deadline, not in marketing copy.

## Common misconceptions

- "The FTC click-to-cancel rule applies."
  It was vacated July 8, 2025, the CFR was rolled back on Feb. 12, 2026, and only an ANPRM exists [8th-cir][cfr425][ftc-anprm].
  ROSCA and state laws still require easy cancellation [rosca][bpc17602].
- "A Terms link in the footer binds users."
  Courts consistently decline to enforce browsewrap [chabolla].
- "'By continuing you agree' is enough."
  Only if the sentence names the exact button the user clicks [chabolla].
- "We can update the terms by posting them."
  Not for existing users without notice and acceptance [douglas][ftc-tos-change].
- "EU withdrawal doesn't apply to SaaS."
  It does until the service is fully performed; the user owes pro-rata only after an express request to start [crd].
- "The withdrawal button is only for shops selling goods."
  It covers any online distance contract with a withdrawal right, from 19 June 2026 [d2673].
- "We must have a refund policy by US law."
  No general federal duty; California 1723 covers goods only [civ1723].
  Whatever policy you state, you must honor [ftc-deception].
- "The FTC fees rule bans drip pricing everywhere."
  Only live-event tickets and short-term lodging [ftc-fees-faq]; California SB 478 is the broad one [civ1770].
- "Showing fees at checkout before payment is fine in California."
  It is not [ca-ag-fees].
- "Incentivized reviews are banned."
  Allowed if not conditioned on sentiment and disclosed [ftc-reviews-qa].
- "'Results not typical' fixes a testimonial."
  It does not [cfr255-2].
- "We're SOC 2 certified."
  SOC 2 is a CPA attestation report, not a certification [aicpa-soc2-guide].
- "HIPAA/GDPR certified."
  No such certifications; the FTC has acted against these claims [ftc-hipaa][ftc-verkada].
- "CAN-SPAM's 10 business days is the deadline."
  Gmail expects about 48 hours and Yahoo 2 days for bulk senders [gmail-faq][yahoo].
- "Impressum per section 5 TMG" and "EU ODR link required."
  TMG was replaced by DDG in May 2024; the ODR link duty ended 20 July 2025 [ddg-date][odr-repeal].
- "FTC civil penalty is $51,744."
  It is $53,088 since January 2025, unchanged for 2026 [ftc-penalty-2026].
- "DSA Article 25 bans dark patterns for every app."
  It applies to online platforms, not micro or small ones, and defers to the UCPD and GDPR [dsa][dsa19].

## Open questions / needs a lawyer

- Whether the California annual reminder (17602(h)) applies to monthly plans; current wording is ambiguous [bpc17602].
- Whether the amended New York law reaches B2B subscriptions (secondary sources say likely) [ny-b2b].
- Exact text and status of Massachusetts, Virginia, Colorado and Louisiana auto-renewal rules; not verified against primary text [state-roundup].
- Whether the FTC will propose a new negative option rule after the March 2026 ANPRM [ftc-anprm].
- National transposition of the EU withdrawal function in each target country, including exact label translations [d2673-commentary].
- UK subscription regime final regulations and start date (draft says 1 January 2027) [uk-sub-si].
- EU Digital Fairness Act: a proposal was expected in November 2026 per secondary sources; not yet published [dfa].
- Whether any app counts as an EU "online platform" under the DSA, and whether we qualify as a small enterprise [dsa19].
- Whether a European consumer's mandatory home-country rules override our choice-of-law clause (not researched here).
- Arbitration and class-action waivers in our terms (enforceability turns on the formation issues above; not researched here).
- Health apps that make treatment claims may also be FDA-regulated medical device software (not researched here).
- Whether showing a client's logo requires permission under that client's specific contract.

## Sources

[chabolla]: https://cdn.ca9.uscourts.gov/datastore/opinions/2025/02/27/23-15999.pdf
[meyer]: https://www.uschamber.com/assets/documents/Opinion20-20Meyer20v.20Kalanick2C20Uber20Technologies2C20Inc.2028Second20Circuit29.pdf
[douglas]: https://blog.ericgoldman.org/archives/2007/07/ninth_circuit_s_1.htm
[ftc-tos-change]: https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/02/ai-other-companies-quietly-changing-your-terms-service-could-be-unfair-or-deceptive
[rosca]: https://www.law.cornell.edu/uscode/text/15/8403
[ftc-amazon]: https://www.ftc.gov/news-events/news/press-releases/2025/09/ftc-secures-historic-25-billion-settlement-against-amazon
[8th-cir]: https://infobytes.orrick.com/wp-content/uploads/Vacated-Opinion.pdf
[cfr425]: https://www.law.cornell.edu/cfr/text/16/part-425
[ftc-anprm]: https://www.ftc.gov/news-events/news/press-releases/2026/03/ftc-seeks-public-comment-response-advance-notice-proposed-rulemaking-regarding-negative-option
[bpc17602]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17602
[bpc17601]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17601
[ny527a]: https://www.nysenate.gov/legislation/laws/GBS/527-A
[ny-b2b]: https://www.ashurstperkinscoie.com/en/insights/update/new-york-and-colorado-update-auto-renewing-subscription-requirements/
[mn57]: https://www.revisor.mn.gov/statutes/cite/325G.57
[mn60]: https://www.revisor.mn.gov/statutes/cite/325G.60
[state-roundup]: https://www.kelleydrye.com/viewpoints/blogs/ad-law-access/auto-renewal-laws-2025-round-up
[crd]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02011L0083-20220528
[d2673]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32023L2673
[d2673-commentary]: https://vbb.com/wp-content/uploads/2026/06/8-06-26-The-online-withdrawal-button.pdf
[sofatutor]: https://curia.europa.eu/jcms/upload/docs/application/pdf/2023-10/cp230154en.pdf
[uk-ccr29]: https://www.legislation.gov.uk/uksi/2013/3134/regulation/29
[uk-ccr37]: https://www.legislation.gov.uk/uksi/2013/3134/regulation/37
[uk-sub-si]: https://www.legislation.gov.uk/ukdsi/2026/9780348287912
[uk-sub-pm]: https://www.gov.uk/government/news/pm-starts-roll-out-of-everyday-fixes-on-the-cost-of-living-ending-rip-off-discounts-and-subscription-traps
[civ1723]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1723
[apple-refund]: https://developer.apple.com/documentation/storekit/handling-refund-notifications
[gplay-refund]: https://support.google.com/googleplay/answer/15574908?hl=en-GB
[gplay-dev-refund]: https://support.google.com/googleplay/android-developer/answer/2741495?hl=en
[gplay-chargeback]: https://support.google.com/googleplay/android-developer/answer/17068375?hl=en-GB
[ftc-fees-faq]: https://www.ftc.gov/business-guidance/resources/rule-unfair-or-deceptive-fees-frequently-asked-questions
[cfr464-2]: https://www.law.cornell.edu/cfr/text/16/464.2
[civ1770]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1770
[ca-ag-fees]: https://oag.ca.gov/hiddenfees
[ucpd]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02005L0029-20220528
[pid]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:01998L0006-20220528
[cma-dmcc]: https://www.gov.uk/government/news/cma-to-boost-consumer-and-business-confidence-as-new-consumer-protection-regime-comes-into-force
[cma207]: https://www.gov.uk/government/publications/unfair-commercial-practices-cma207/unfair-commercial-practices
[cma208]: https://assets.publishing.service.gov.uk/media/67eeb64fe9c76fa33048c790/CMA208_-_Fake_reviews_guidance.pdf
[dmcc-sch20]: https://www.legislation.gov.uk/ukpga/2024/13/schedule/20
[ftc-dark-pr]: https://www.ftc.gov/news-events/news/press-releases/2022/09/ftc-report-shows-rise-sophisticated-dark-patterns-designed-trick-trap-consumers
[ftc-dark]: https://www.ftc.gov/system/files/ftc_gov/pdf/P214800%20Dark%20Patterns%20Report%209.14.2022%20-%20FINAL.pdf
[dsa]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32022R2065
[dsa19]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32022R2065
[cfr465]: https://www.law.cornell.edu/cfr/text/16/part-465
[ftc-reviews-qa]: https://www.ftc.gov/business-guidance/resources/consumer-reviews-testimonials-rule-questions-answers
[ftc-review-warn]: https://www.ftc.gov/news-events/news/press-releases/2025/12/ftc-warns-10-companies-about-possible-violations-agencys-new-consumer-review-rule
[ftc-penalty-2026]: https://www.federalregister.gov/documents/2026/09/15/2026-18853/civil-penalty-inflation-adjustments
[ftc-rytr]: https://www.ftc.gov/news-events/news/press-releases/2025/12/ftc-reopens-sets-aside-rytr-final-order-response-trump-administrations-ai-action-plan
[ftc-verkada]: https://www.ftc.gov/news-events/news/press-releases/2024/08/ftc-takes-action-against-security-camera-firm-verkada-over-charges-it-failed-secure-videos-other
[ftc-endorse-2023]: https://www.federalregister.gov/documents/2023/07/26/2023-14795/guides-concerning-the-use-of-endorsements-and-testimonials-in-advertising
[cfr255-0]: https://www.law.cornell.edu/cfr/text/16/255.0
[cfr255-2]: https://www.law.cornell.edu/cfr/text/16/255.2
[cfr255-4]: https://www.law.cornell.edu/cfr/text/16/255.4
[civ3344]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=3344
[ftc-subst]: https://www.ftc.gov/legal-library/browse/ftc-policy-statement-regarding-advertising-substantiation
[ftc-deception]: https://www.ftc.gov/system/files/documents/public_statements/410531/831014deceptionstmt.pdf
[ftc-ai-comply]: https://www.ftc.gov/news-events/news/press-releases/2024/09/ftc-announces-crackdown-deceptive-ai-claims-schemes
[workado]: https://www.ftc.gov/news-events/news/press-releases/2025/04/ftc-order-requires-workado-back-artificial-intelligence-detection-claims
[ftc-ai-hub]: https://www.ftc.gov/news-events/news/press-releases/2026/08/ftc-finalizes-orders-cox-media-group-two-other-firms-settling-charges-they-deceived-customers-about
[cfr323-1]: https://www.law.cornell.edu/cfr/text/16/323.1
[cfr323-2]: https://www.law.cornell.edu/cfr/text/16/323.2
[cfr323-3]: https://www.law.cornell.edu/cfr/text/16/323.3
[ftc-health]: https://www.ftc.gov/business-guidance/resources/health-products-compliance-guidance
[d825]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32024L0825
[aicpa-soc]: https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2
[aicpa-soc2-guide]: https://www.aicpa-cima.com/cpe-learning/publication/soc-2-reporting-on-an-examination-of-controls-at-a-service-organization-relevant-to-security-availability-processing-integrity-confidentiality-or-privacy
[aicpa-soc3]: https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-3
[aicpa-2027]: https://www.aicpa-cima.com/news/article/aicpa-proposes-update-of-soc-2-r-trust-services-criteria-to-enhance-the-relevance-usability-and-value-of-cpas-reports
[ftc-zoom]: https://www.ftc.gov/news-events/news/press-releases/2020/11/ftc-requires-zoom-enhance-its-security-practices-part-settlement
[ftc-monument]: https://www.ftc.gov/system/files/ftc_gov/pdf/MonumentComplaintFiled.pdf
[ftc-hipaa]: https://www.ftc.gov/business-guidance/resources/collecting-using-or-sharing-consumer-health-information-look-hipaa-ftc-act-health-breach
[ftc-ps-medable]: https://www.ftc.gov/news-events/news/press-releases/2019/11/california-company-settles-ftc-allegations-it-falsely-claimed-participation-eu-us-privacy-shield
[ftc-ps-2018]: https://www.ftc.gov/news-events/news/press-releases/2018/09/ftc-reaches-settlements-four-companies-falsely-claimed-participation-eu-us-privacy-shield
[lanham]: https://www.law.cornell.edu/uscode/text/15/1125
[ecd]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32000L0031
[odr-repeal]: https://eur-lex.europa.eu/eli/reg/2024/3228/oj/eng
[ddg5]: https://www.gesetze-im-internet.de/ddg/__5.html
[ddg33]: https://www.gesetze-im-internet.de/ddg/__33.html
[ddg-date]: https://ihk-bonn.de/recht-und-steuern/recht/aktuelles/das-digitale-dienste-gesetz-ersetzt-das-telemediengesetz
[uk-ecr6]: https://www.legislation.gov.uk/uksi/2002/2013/regulation/6
[civ17893]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1789.3
[civ17892]: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1789.2
[ftc-canspam]: https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
[cfr316-5]: https://www.law.cornell.edu/cfr/text/16/316.5
[gmail]: https://support.google.com/a/answer/81126
[gmail-faq]: https://support.google.com/a/answer/14229414
[yahoo]: https://senders.yahooinc.com/best-practices/
[outlook]: https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730
[eprivacy]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219
[gdpr]: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679
[pecr22]: https://www.legislation.gov.uk/uksi/2003/2426/regulation/22
[ico-duaa]: https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/02/statement-on-the-commencement-of-the-data-use-and-access-act-duaa
[aws-sla]: https://aws.amazon.com/compute/sla/
[dfa]: https://cms.law/en/aut/legal-updates/inside-the-eu-s-planned-digital-fairness-act-digital-design-subscription-traps-and-influencer-marketing
