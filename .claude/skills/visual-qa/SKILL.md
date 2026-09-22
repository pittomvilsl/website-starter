---
name: visual-qa
description: Verify how a site actually renders before calling UI work done — inspect the real page on desktop and on a narrow mobile viewport, checking composition, spacing, typography, alignment, image crops, CTA prominence, tap targets, overflow and section rhythm, then fix what is wrong and re-inspect. Use after building or changing any user-facing UI, when investigating responsive problems, and before shipping.
---

# Visual QA

## The premise

A website is not finished because TypeScript compiles, the build passes, or tests are green. None of those look at the page.

**UI work is verified by looking at the rendered result.** If browser or dev-server tooling is available in this session, use it. Reporting UI as complete without having seen it render — when you could have — is an incomplete job, and say so plainly if tooling genuinely is not available.

## Set up the inspection

1. Start the dev server using the available preview or dev-server tooling.
2. Open the actual page or pages that changed.
3. Inspect at a desktop width and at **at least one narrow viewport** (a 375px-class phone width).
4. Use rendered screenshots for composition and proportion judgements; use the accessibility tree or page text for verifying content, structure and headings. Console and network output will surface errors that a screenshot hides.

Inspect with real content loaded. An empty state or a lorem-ipsum page proves very little.

## Desktop inspection

- **Hero composition** — does it establish the brand in the first screen, or is it a generic centred headline with a button?
- **Maximum content width** — is there a deliberate container, and does long-form text have a readable measure rather than running edge to edge?
- **Whitespace** — is it structural and varied, or the same padding repeated down the page?
- **Alignment** — do elements line up to a grid? Are there near-misses that read as sloppiness?
- **Typography** — real rendered sizes, weights and line heights. Check headline breaks at this width.
- **Section rhythm** — does the page vary, or is every section the same shape at the same height?
- **Image cropping** — are subjects cropped sensibly at this aspect ratio? Any stretching or letterboxing?
- **CTA prominence** — is the primary action findable without hunting, and clearly primary against secondary actions?
- **Header and footer** — is the header behaviour on scroll intentional? Is the footer designed, or a dumped link list?
- **Hover states** — hover the interactive elements. Anything that only changes opacity is unfinished.
- **Horizontal overflow** — confirm the page does not scroll sideways at any width.
- **Loading and font swap** — watch the page load. Note any layout shift or flash of unstyled text.

## Mobile inspection

Inspect a narrow viewport explicitly. This is where generated sites fail most often.

- **Hero** — is it composed for the phone, or a desktop hero with everything squeezed?
- **Line breaks** — do headlines break at sensible points? Any orphaned single words?
- **Font sizes** — is body text comfortably readable without zoom? Are display sizes scaled down, or still desktop-sized and overflowing?
- **Buttons** — full width where appropriate, comfortably tappable, not stacked into a wall of identical blocks.
- **Forms** — labels visible, fields wide enough, correct input types and keyboards, errors readable, submit reachable.
- **Cards and grids** — do multi-column layouts collapse into something intentional, or an endless single-column scroll of identical boxes?
- **Navigation** — does the menu open, close, trap focus sensibly, and is it operable one-handed?
- **Image crops** — do wide desktop crops still work? Faces and products should not be cut in half.
- **Spacing** — desktop section padding is usually too large on a phone. Check it was adjusted.
- **Tap targets** — adequately sized and adequately separated; adjacent links should not be a single ambiguous mass.
- **Overflow** — the most common mobile defect. Confirm no horizontal scroll.

Compare what you see against the mobile composition intent recorded by `premium-web-design`. A mobile layout that is merely a shrunken desktop is a defect, not a compromise.

## Design review

At the final review, ask the question directly:

> Does this look like a good designer deliberately designed it, or like an AI assembled a standard website?

Then actively hunt for the evidence of the second answer:

- repetitive sections with the same shape and rhythm
- too many cards doing work that typography, tables, or images should do
- the same border radius on every element on the page
- generic decorative iconography
- weak or accidental whitespace
- no discernible art direction — nothing that ties the page to *this* brand
- inconsistent spacing between comparable elements
- a cluttered or unresolved desktop layout
- a mobile layout that is only a scaled-down desktop

Run the final checklist in `docs/anti-ai-slop.md`, including the brand-transfer test. The page should be difficult to transplant unchanged onto an unrelated business.

## Fix and re-inspect

When something is wrong: fix it, then **look at it again**. A fix is not verified until it has been re-rendered and re-checked — repairs frequently break something adjacent, especially in responsive layouts.

Iterate until the page holds up at both widths.

## Report honestly

State which viewports were actually inspected, what was found, what was fixed, and what remains. If a problem was found and deliberately left, say so and why. If no browser tooling was available, say that the work was not visually verified rather than implying it was.

## Scope

- Changing button text or a copy string — no full visual QA needed.
- A new page, hero, or section — full desktop and mobile inspection.
- A reported responsive problem — targeted inspection at the failing widths, then confirm neighbouring widths still hold.
- Preparing for production — full inspection, then `accessibility-audit` and `performance-audit`.
