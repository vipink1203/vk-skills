# Accessibility gates

Our bar is WCAG 2.2 level AA on every screen.
No US regulation fixes a WCAG version for private businesses, so 2.2 AA is our chosen bar.
It covers the WCAG 2.1 AA that DOJ's Title II rule requires for state and local government content, including content a vendor provides on a government's behalf.
In the EU, EN 301 549 V4.1.1 (based on WCAG 2.2) was published in September 2026, but V3.2.1 (WCAG 2.1) stays the officially cited version until the new one is cited, expected 16 December 2026.
Evidence: [`research/03-app-accessibility-ip-and-ai.md`](../research/03-app-accessibility-ip-and-ai.md) sections 1 and 2.

Automated tools find on average about 57% of issues (axe-core's own figure), and a Lighthouse score of 100 does not mean conformance.
So each gate pairs automated checks with a dated human check where a script cannot judge.
For fixes, an accessibility or colour skill helps if you have one installed (for example `better-accessibility` and `better-colors`).

## A11Y-1 Automated scan is clean

- **Build:** Run axe-core in the end-to-end suite (`@axe-core/playwright`) on every route and every modal state, with tags `wcag2a, wcag2aa, wcag21a, wcag21aa, wcag22aa`.
  Review every "incomplete" result by hand.
- **Done when:** the scan reports zero violations on every route in CI, and each incomplete result has a recorded human verdict.

## A11Y-2 Contrast

- **Rule:** Text 4.5:1, large text (18pt, or 14pt bold) 3:1 (1.4.3); UI component boundaries, states and meaningful graphics 3:1 (1.4.11).
  Setting a text color without a background color, or the reverse, fails.
- **Build:** Define colors as tokens with contrast checked per pair in light and dark themes, including hover, focus, placeholder and error states.
  Text over images or gradients gets a solid backing or scrim.
- **Done when:** every token pair used for text or controls meets its ratio in both themes, and text over images is measured at its worst point (lightest or darkest pixel behind it) and meets its ratio.

## A11Y-3 Text alternatives

- **Rule:** Every meaningful image, icon button and control has a text alternative serving the same purpose (1.1.1); decorative images use `alt=""`, which differs from a missing `alt`.
- **Build:** Write alt text that states what the image tells the user, not "image of".
  Icon-only buttons get an accessible name (`aria-label` or visually hidden text).
- **Done when:** the scan reports no missing alternatives, and a dated human read of each alt text confirms it carries the image's meaning.

## A11Y-4 Keyboard, focus, timing and targets

- **Rule:** Everything works by keyboard (2.1.1), with no trap (2.1.2), a skip link or landmarks to bypass repeated blocks (2.4.1), logical focus order (2.4.3), a visible focus indicator (2.4.7), and focus never fully hidden behind sticky headers, cookie banners or chat widgets (2.4.11).
  A time limit on a user's task can be turned off, extended to ten times the default, or extended with a warning giving at least 20 seconds and a simple action, at least ten times (2.2.1).
  Auto-updating content shown alongside other content can be paused, stopped, hidden or slowed, and moving, blinking or scrolling content lasting over five seconds can be paused, stopped or hidden (2.2.2).
  Pointer targets are at least 24 by 24 CSS pixels, or spaced so a 24px circle around each touches no other (2.5.8).
- **Build:** Native elements first (`<button>`, `<a href>`); no positive `tabindex`; dialogs move focus in and return it to the trigger on close; a "Skip to main content" link; `scroll-padding-top` equal to any sticky header; no `outline: none` without a `:focus-visible` replacement.
- **Done when:** a Playwright test tabs through each route and asserts every interactive element is reached, visibly focused and not fully covered by a fixed or sticky overlay, that every dialog can be left by keyboard, that the skip link exists, and that every interactive element's `getBoundingClientRect()` meets 2.5.8, apart from an exceptions list kept in the test with a reason per entry (inline links in sentences, browser-default controls, controls with an equivalent elsewhere on the page); and a dated human pass confirms the focus order is logical and every time limit and moving or auto-updating element meets 2.2.1 and 2.2.2.

## A11Y-5 EU accessibility statement (only for larger EU consumer commerce)

- **Rule:** The European Accessibility Act (applying since 28 June 2025) covers listed consumer services, including e-commerce, and exempts microenterprises providing services (fewer than 10 staff and EUR 2M or less turnover or balance sheet).
  Covered providers publish, in their terms or equivalent, how the service meets the accessibility requirements, and may claim disproportionate burden only after a documented assessment kept for five years.
- **Build:** When scope shows EU consumer sales and we are past microenterprise size: an accessibility statement linked from the terms, and any burden assessment filed in the compliance record.
- **Done when:** the statement is published and linked; or the record marks n/a with the scope answer (no EU consumer sales, or microenterprise).
