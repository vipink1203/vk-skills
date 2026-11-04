# Terms and payments gates

Terms acceptance, the record of it, refunds, prices, subscriptions and cancellation.
Evidence: [`research/02-app-commerce-and-claims.md`](../research/02-app-commerce-and-claims.md) sections 1 to 4.

## TERMS-1 Terms of service exist and bind users

- **Rule:** Courts enforce clickwrap and reject browsewrap; the user must be told which exact action means agreement, in text a reasonably prudent user would see (Berman 2022, Chabolla v. ClassPass 2025, where small gray text away from the button failed).
- **Build:** A `/legal/terms` page, versioned (immutable ID or content hash per version).
  On every screen that creates an account or takes payment, an unchecked checkbox "I agree to the [Terms of Service]" that must be ticked before the button enables, or at minimum the sentence "By clicking **Create account**, you agree to the [Terms of Service]" directly beside the button, naming that button's exact label.
  Body-size, high-contrast text; links styled as links (color plus underline).
  Privacy is acknowledged, never agreed to: "and acknowledge the [Privacy Policy]" (see PRIV-1).
- **Done when:** a test on every account-creation and payment screen asserts the notice sits in the same container as its button, its computed font size is at least the body size, its contrast is at least 4.5:1, its links are underlined and colored, and the named label matches the button text exactly; no screen relies on a footer link alone.

## TERMS-2 Acceptance is recorded

- **Rule:** Courts decide on the screens actually shown, so the record must reproduce them; California requires subscription consent records for 3 years or 1 year after termination, whichever is longer, which we use as the floor for all acceptance records.
- **Build:** An append-only `consent_events` table (shared with CONSENT-3 and PAY-3) with: `user_id`, email at the time, `document_type`, `document_version`, `accepted_at` (UTC, server-side), `ip_address`, `user_agent`, platform and app version, `ui_surface`, `ui_version` (build or commit), the exact notice string and button label rendered, `method` (checkbox plus button, or button only), `locale`.
  Archive every terms version so it stays retrievable, and a screenshot of each acceptance screen per UI version (the end-to-end suite can capture these).
- **Done when:** a test creates an account and asserts a `consent_events` row with every field filled, the referenced `document_version` resolves to the archived text, and the current UI version has an archived screenshot of each acceptance screen.

## TERMS-3 Changes to terms reach existing users

- **Rule:** Case law, read here through secondary summaries (Douglas v. U.S. District Court, 9th Cir. 2007), holds that posting revised terms does not bind existing users without notice and acceptance.
  The FTC warns that quietly widening data use through a terms or policy change can be unfair or deceptive (Feb 2024).
  Subscription changes have their own notices (PAY-3).
- **Build:** Material change: advance email notice, then a blocking re-acceptance on next sign-in, recorded as a new TERMS-2 event.
  Non-material change: banner plus a public changelog; still a new version.
  New data uses apply only to data collected after fresh consent.
- **Done when:** bumping the terms version with `material: true` forces the re-acceptance screen in an end-to-end test.

## PAY-1 Prices are the full price

- **Rule:** California SB 478 (Civil Code 1770(a)(29)) requires every displayed price to include all mandatory fees except government taxes and actual shipping; revealing fees at checkout does not comply.
  EU/UK consumer prices include VAT, and subscriptions show the total cost per billing period.
  The EU Price Indication Directive requires a "was" price on goods to be the lowest price of the prior 30 days; we apply it to everything as a stricter choice.
- **Build:** One pricing source of truth that renders the all-in amount per period everywhere a price appears.
  A card surcharge counts as mandatory when card is the only way to pay.
  Strike-through prices only with a stored 30-day price history.
- **Done when:** the amount on the pricing page, the checkout summary and the first charge are identical for a test purchase, excluding only sales tax in the US.

## PAY-2 Refund policy is published and honoured

- **Rule:** The US has no general federal refund duty, but any stated policy must be honoured (FTC deception).
  EU/UK consumers have a 14-day withdrawal right with refund within 14 days (see PAY-5).
  For in-app purchases Apple runs refunds; Google refunds within 48 hours, then the developer's own policy applies.
- **Build:** A `/legal/refunds` page linked from checkout and the footer, stating the actual policy, the EU/UK 14-day right where it applies, and that store purchases are refunded through Apple or Google with links to their process.
  Handle Apple `REFUND` server notifications by revoking the entitlement.
- **Done when:** the page exists, is linked from checkout, and every promise on it maps to a code path or an owner process named in the compliance record.

## PAY-3 Auto-renewal is disclosed, consented and reminded

- **Rule:** ROSCA (15 USC 8403) requires clear and conspicuous disclosure of all material terms before billing information is taken, and express informed consent before charging.
  California's Automatic Renewal Law (as amended by AB 2863, contracts from 1 July 2025) is the strictest common standard; build to it everywhere.
  New York requires material-change notice 5 business days to 30 days ahead, and for price increases new consent or a cancel window with a pro-rata refund.
- **Build:** Above the payment fields, in larger or contrasting type: it renews until cancelled, the recurring price and period, whether and how the price may change, the renewal term, any minimum term, how to cancel, and for trials the price charged after the trial and when.
  A separate unchecked checkbox for the auto-renewal terms, apart from TERMS-1.
  A confirmation email containing the terms, the cancellation policy, how to cancel, and for trials how to cancel before paying.
  Notices, each stating that the plan renews, the term, the amount and frequency, how to cancel, a cancellation link, and our contact details: trials or promo prices over 31 days get one 3 to 21 days before they end; terms of a year or more get one 15 to 45 days before renewal; an annual reminder goes to every subscriber.
  Price increases: notice 7 to 30 days before, with how to cancel, and a pro-rata refund on cancellation in that window.
  Other material changes: notice 5 business days to 30 days before, with how to cancel.
  Record every consent and notice (type, sent time, content version) for at least 3 years or 1 year after termination, whichever is longer.
- **Done when:** a test checkout asserts the renewal terms render above the card fields in emphasised type, the purchase cannot complete without the renewal checkbox, a consent record is written, and the confirmation email is sent; each notice type has a scheduled job and a template test asserting its required contents.

## PAY-4 Cancelling is as easy as signing up

- **Rule:** ROSCA requires a simple mechanism; California requires online cancellation via a prominent direct link or button when signup was online, in the same medium, and a save offer only beside a continuously shown "click to cancel" button.
  The FTC click-to-cancel rule was vacated on 8 July 2025, so ROSCA and state law are the binding rules.
- **Build:** A "Cancel subscription" button in account settings.
  Our house rule: cancelling takes no more steps than signing up.
  Any retention offer sits beside a visible "Click to cancel" button that ends the subscription immediately.
  A path for users who cannot sign in (for example a prefilled cancellation email address).
  Cancellation confirmation by email with the effective date.
- **Done when:** an end-to-end test cancels from the logged-in home screen in no more steps than signup took, and the cancellation is recorded and confirmed by email.

## PAY-5 EU/UK withdrawal right and withdrawal button

- **Rule:** EU/UK consumers may withdraw from a distance contract within 14 days; a SaaS service keeps that right until fully performed, and the user owes a pro-rata amount only after expressly asking to start immediately.
  One-off digital content loses the right once supply starts, only with express consent, acknowledgment, and confirmation on a durable medium.
  The EU order button must state the obligation to pay, or the consumer is not bound.
  From 19 June 2026 EU online contracts need a withdrawal function labelled "withdraw from contract here" (or an unambiguous equivalent), a confirmation step labelled "confirm withdrawal", and a timestamped acknowledgment on a durable medium.
  The binding wording is each country's transposition; the English labels come from the Directive.
- **Build:** Applies when EU/UK consumers can buy.
  Order button labelled with payment ("Subscribe and pay").
  Unchecked checkbox "Start my subscription now. I understand I will pay for what I use if I withdraw within 14 days."
  For one-off digital content: "I consent to immediate delivery and acknowledge I lose my right of withdrawal once delivery starts", confirmed by email.
  A "Withdraw from contract here" link visible in account settings for the 14 days, leading to a "Confirm withdrawal" step and an emailed acknowledgment with content, date and time.
  Refund within 14 days through the original payment method.
  Translated labels for each target country are an owner question for a lawyer.
- **Done when:** for an EU test account, the order button text states payment, the immediate-start consent is recorded, the withdrawal link shows during the 14 days, the flow completes in two steps, the acknowledgment email is sent, and the refund is issued within 14 days; or the record marks EU/UK sales n/a with the reason.
