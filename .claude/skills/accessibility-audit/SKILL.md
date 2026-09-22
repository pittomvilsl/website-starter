---
name: accessibility-audit
description: Final-pass accessibility review of a site or page — semantic HTML, heading hierarchy, form labels, alt text, keyboard navigation, focus states, colour contrast, tap targets, reduced motion, error messaging and screen-reader basics. Practical fixes using native HTML first, ARIA only where it earns its place. Use before shipping, and whenever a page has been substantially built or changed.
---

# Accessibility Audit

Practical accessibility: a site that real people can actually use with a keyboard, a screen reader, a magnifier, or on a phone in bright sunlight.

**Native HTML first. ARIA only where native markup cannot express the meaning.** Incorrect ARIA is worse than no ARIA — it overrides what the browser already communicated correctly.

## Semantic structure

- Landmarks present and used once each where appropriate: `header`, `nav`, `main`, `footer`. Exactly one `<main>`.
- Content elements match their meaning: lists as `<ul>`/`<ol>`, tables as `<table>` with `<th>` and scope, quotes as `<blockquote>`.
- `<button>` for actions, `<a href>` for navigation. A clickable `div` fails keyboard use, focus, and screen readers simultaneously.
- `lang` set correctly on `<html>`, and on any inline passage in another language.
- A skip link to main content on pages with substantial navigation.

## Heading hierarchy

- One `<h1>` per page that describes the page.
- Levels descend without skipping — no `h2` followed by `h4`.
- Headings describe the section; they are not chosen for their font size. If the correct level looks wrong, fix the CSS, not the markup.
- Read the headings alone, in order. They should work as an outline of the page.

## Forms

- Every input has a real `<label>` associated by `for`/`id`. A placeholder is not a label — it disappears on typing and often fails contrast.
- Group related controls with `<fieldset>` and `<legend>` (radio groups, address blocks).
- Required fields marked in text, not by colour or an asterisk alone.
- Correct `type`, `autocomplete` and `inputMode`.
- Errors: specific, in text, adjacent to the field, associated via `aria-describedby`, and announced on submit. Never colour alone.
- Focus moves to the first error on a failed submit, or to a summary that links to each error.
- Success is announced, not only shown.

## Images and media

- Meaningful images have `alt` text describing their function in context. A product photo in a link describes the product, not the photograph.
- Decorative images use `alt=""` so they are skipped.
- Text in images avoided; where unavoidable, the text is repeated accessibly.
- Icon-only buttons have an accessible name (visually hidden text or `aria-label`).
- Video has captions; no media autoplays with sound.

## Keyboard navigation

Tab through the whole page and confirm:

- Everything interactive is reachable and operable by keyboard.
- Tab order follows the visual order — beware of layout reordering via CSS grid or flex `order`.
- No keyboard trap. Focus can always move forward and back.
- Menus, dialogs, dropdowns and accordions: open and close with the keyboard, `Escape` closes, focus moves into the open element and returns to the trigger on close.
- Custom controls respond to the expected keys (`Enter`/`Space` for buttons, arrow keys within a composite widget).
- Nothing is reachable while visually hidden — off-screen menus must be removed from the tab order when closed.

## Focus states

- Every focusable element has a clearly visible focus indicator. Never remove an outline without replacing it with something equally visible.
- Use `:focus-visible` so keyboard users get the indicator without mouse users seeing it on every click.
- The indicator must have sufficient contrast against its background, including on coloured or image backgrounds.
- Focus is never hidden behind a sticky header when tabbing down the page.

## Colour and contrast

- Body text at 4.5:1 minimum; large text at 3:1. Check the real rendered colours, including text over images and gradients at every crop.
- Interactive elements, borders, icons and form field outlines at 3:1 against their surroundings.
- Placeholder and helper text is frequently too light — check it specifically.
- Information is never conveyed by colour alone: links inside body text need an additional cue, and status needs text as well as colour.
- Check dark mode separately if the site has one. Low-contrast dark mode is on the blacklist in `docs/anti-ai-slop.md`.

## Tap targets and zoom

- Tap targets comfortably large — around 44px — and adequately separated. Adjacent links in a footer or nav should not merge into one ambiguous area.
- Never disable zoom (`user-scalable=no` or `maximum-scale=1`).
- Layout survives 200% browser zoom without content being cut off or overlapped.
- Layout survives a larger default font size without breaking.

## Motion

- Respect `prefers-reduced-motion`: reduce or remove non-essential animation, parallax and autoplaying movement.
- No content that flashes more than three times per second.
- Carousels and auto-advancing content can be paused, and do not advance on their own without control.

## Screen-reader basics

- Verify the accessibility tree, not only the visual output: names, roles and states should be correct.
- Link text makes sense out of context. Several links called "read more" on one page are ambiguous — give each a distinct accessible name.
- Dynamic updates that matter (form results, filter counts, cart changes) are announced via a live region.
- Content hidden visually is hidden from assistive technology too, unless it is intentionally visually-hidden text.
- Modals: correct role, an accessible name, focus trapped while open, and the rest of the page inert.

## ARIA discipline

Before adding any ARIA attribute, confirm a native element could not do the job.

- Do not put a role on an element that already has it (`<nav role="navigation">` is redundant).
- Do not use `aria-label` on a static element that is not interactive.
- Never leave `aria-hidden="true"` on anything focusable.
- If a custom widget needs ARIA, implement the full expected pattern — roles, states *and* keyboard behaviour. A partial implementation is worse than a plain button.

## How to run the audit

1. Read the rendered accessibility tree of each key page.
2. Tab through the page from the top; note where focus goes and where it disappears.
3. Check contrast on real rendered colours, including over imagery.
4. Inspect at a narrow viewport for tap targets and zoom behaviour.
5. Check form flows, including a deliberately failed submission.
6. Fix what is broken, then re-verify — fixes shift focus order and contrast in ways that are easy to miss.

Report what was checked, what was fixed, and what remains with a reason. Do not report a clean audit for checks that were not actually performed.
