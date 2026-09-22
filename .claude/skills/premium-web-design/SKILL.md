---
name: premium-web-design
description: Decide the art direction for a website before any UI is built — brand, audience, positioning, emotion, typography, composition, imagery, desktop and mobile intent, interaction and conversion flow. Use when starting a new site, a new page or template, a redesign, a hero or landing page, or whenever a visual direction has not yet been consciously chosen and written down. This skill owns the creative direction; frontend-design implements it.
---

# Premium Web Design

This is the primary design skill of this starter. It decides **what the site should look and feel like, and why**, before a single component is written.

Rules live in the docs; this skill is the procedure.

| Source of truth | Owns |
| --- | --- |
| `docs/anti-ai-slop.md` | The forbidden-pattern list, composition rules, copy rules, and the final audit checklist |
| `docs/design-system.md` | Token guardrails: typography, color, spacing, radius, containers, grids, buttons, forms, motion |
| `docs/brand-direction.md` | The per-project brand brief — this skill fills it in |
| `AGENTS.md` | The cross-agent baseline that applies to every tool, not just Claude |

Read `docs/anti-ai-slop.md` before producing a direction. Do not restate its list here or in your output — apply it.

## The one hard rule

**No layout, component, colour, or font is written before the brand brief exists.**

If `docs/brand-direction.md` is still a template full of `[placeholder]` values, filling it in is the first deliverable. Everything downstream depends on it.

## Step 1 — Interrogate the brand

Establish, in writing, before designing:

- **Business** — what is actually sold, at what price level, how the money is made.
- **Audience** — who visits, what they already believe, how much they trust this business, what they fear or hesitate about.
- **Positioning** — the nearest three competitors and what this business must *not* look like.
- **Desired emotion** — the feeling on first paint, in three words that are not "modern", "clean", or "professional".
- **Context of use** — phone in a hurry? desktop at work? evening browsing? That changes the whole composition.
- **Constraints** — real photography available or not, existing logo, existing colours, languages, legal or regulatory requirements.

Ask the user for anything missing that would change the design materially. If the user is unavailable, choose defensible answers, **state them as explicit assumptions in your output**, and continue — do not stall, and do not silently invent a premium luxury brand because it is the easiest thing to style.

## Step 2 — Commit to an art direction

Write the answers into `docs/brand-direction.md`. Then commit to a direction and record **a reason tied to the brand** for each of these. A choice without a reason is a default, and defaults are what make sites look AI-generated.

1. **Core direction** — three attributes, e.g. `heritage × warmth × premium editorial`.
2. **Typography strategy** — which typeface does the work, why it suits *this* business, how heading and body relate. Never pick a face because it is currently fashionable.
3. **Colour strategy** — where the colour comes from (product, material, place, history, ink, signage) and how it is distributed. Dominant plus a restrained accent beats an evenly spread palette.
4. **Layout strategy** — the structural idea: editorial columns, full-bleed imagery, a strict grid, asymmetry, a list-driven utility page, a catalogue. Name it.
5. **Imagery strategy** — photography, illustration, type-only, product shots, or texture. Decide crops and treatment. If no real imagery exists, design a direction that does not depend on it rather than filling space with stock.
6. **Motion strategy** — what moves, and what job the movement does. The default is almost nothing.
7. **Signature element** — the one memorable, brand-specific idea (see `docs/anti-ai-slop.md`).

## Step 3 — The anti-monoculture test

This starter exists to produce a consistent *quality standard*, never a consistent *look*. Two sites built from it should not be recognisable as siblings.

Run these three checks on the direction before continuing:

- **Brand-transfer test** — remove the logo and name. Could this be a crypto, AI, or SaaS site? If yes, redesign.
- **Sector test** — would this direction be wrong for a different sector? It *should* be. A direction that suits everybody suits nobody.
- **Default test** — list every choice made because it was the obvious option rather than the right one. Replace them.

Concrete illustration of how far apart legitimate outcomes should sit:

| Business | Plausible direction | Layout instinct | Imagery | Motion |
| --- | --- | --- | --- | --- |
| Hair salon | Tactile, personal, portfolio-led | Full-bleed work gallery; booking never more than one tap away | Real client photography, tight crops | Almost none; fast image transitions |
| Frituur / takeaway | Loud, legible, local, appetite-driven | Menu and opening hours above everything; dense and scannable | Food shot honestly, warm and close | None — speed matters more |
| Energy company | Institutional, calm, evidence-led | Tariffs and comparison tables; wide readable measure | Diagrams and infrastructure, not smiling stock | Only state feedback on calculators |
| Law firm | Restrained, precise, authoritative | Typographic hierarchy, generous margins, quiet structure | Portraits and place; possibly no imagery at all | Effectively none |
| Luxury clothing label | Editorial, spacious, image-first | Full-bleed campaign imagery; type as a minor voice | Campaign photography carries the page | Slow, deliberate, few moments |

These illustrate *distance*, not templates to copy. A real brief may land somewhere none of these rows predict.

## Step 4 — Plan the composition

For every page, list its sections in order, and for each one answer the three questions from `docs/anti-ai-slop.md`: why it exists, what question it answers, what the visitor does next. Delete any section that cannot answer all three.

Then decide, per section, how it is *composed* — before reaching for a card grid. The alternatives listed in `docs/anti-ai-slop.md` (editorial layout, split composition, comparison tables, timelines, diagrams, photography, asymmetric grids, numbered sections, full-width statements) exist so that the card grid has to earn its place.

Vary the rhythm deliberately. If every section is a centred heading over a three-column row, the page reads as generated no matter how good the tokens are.

## Step 5 — Design desktop and mobile as two compositions

Decide the mobile composition on purpose — not as the desktop layout stacked.

State for each key section: what the phone shows first, what gets cut or reordered, how the headline breaks, where the CTA sits, and whether a desktop element (a wide table, a multi-column grid, a large hero crop) needs a genuinely different mobile form.

`docs/design-system.md` holds the responsive review list. The mobile intent decided here is what `visual-qa` later verifies against.

## Step 6 — Interaction and conversion flow

Name the primary action of the site and the single path to it. Then:

- Where does the primary CTA appear, and how many times?
- What is the secondary path for visitors who are not ready?
- What proof (prices, credentials, reviews, photographs, guarantees) sits next to each decision point?
- What must the visitor trust before acting, and is that on the page *above* the decision?
- Which interactions need feedback — forms, filters, bookings, calculators?

Conversion is composition, not a button colour. If the proof arrives after the ask, restructure the page.

## Step 7 — Write the brief and hand off

Produce a short design brief containing:

1. Brand, audience, positioning, desired emotion.
2. The seven art-direction decisions from Step 2, each with its reason.
3. The section-by-section composition plan.
4. Mobile composition intent.
5. The conversion path.
6. Explicit assumptions where information was missing.
7. Which generic patterns were deliberately avoided, and what replaced them.

Update `docs/brand-direction.md` so the decisions survive the conversation. If the direction requires token changes (a type scale, a radius, a container width), record them in `docs/design-system.md` for that project.

Hand implementation to the **frontend-design** skill. That skill executes this direction at production quality — it does not re-decide it. If implementation reveals the direction is wrong, come back here and change the brief deliberately rather than letting it drift during coding.

## Scope

Use the full procedure for a new site, a new page or template, or a redesign.

For a small change inside an existing, already-directed site, do not re-run the whole thing — read `docs/brand-direction.md`, stay inside the established direction, and move on.
