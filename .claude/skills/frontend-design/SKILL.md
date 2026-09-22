---
name: frontend-design
description: Implement an agreed art direction as production-grade UI — composition, typographic rhythm, spacing, responsive layout, visual hierarchy, custom components, interaction states, content density, section transitions, consistency and polish. Use when building or refining pages and components after the direction is set. Does not choose the art direction; premium-web-design does that.
---

# Frontend Design

This skill turns an agreed direction into real, polished interface code.

**Boundary:** `premium-web-design` decides *what it should look like and why*. This skill decides *how to build that well*. If no direction exists yet, stop and run `premium-web-design` first. If a direction exists, do not quietly re-invent it — implement it, and raise a conflict explicitly if the direction cannot survive contact with real content.

Read before implementing:

- `docs/brand-direction.md` — the direction being implemented
- `docs/design-system.md` — the token guardrails
- `docs/anti-ai-slop.md` — the forbidden-pattern list and the final audit

## Start from content, not from components

Get the real content, or a realistic approximation, before building. Layouts designed around placeholder text fail as soon as a heading runs to three lines, a product name is 40 characters, or a list has two items instead of six.

For each section decide the layout from the content it holds, then reach for a component. Not the reverse.

## Typography and rhythm

- Establish the type scale once, from `docs/design-system.md`, and use it. Arbitrary one-off sizes are the fastest route to an incoherent page.
- Set a deliberate measure for body text. Long-form prose that runs the full width of a desktop container is unreadable.
- Line height varies by role: tight for large display type, looser for body copy. One global value for everything is a default, not a decision.
- Control headline breaks at the sizes that matter. A headline that breaks badly on a laptop is a visible defect.
- Weight and size do the hierarchy work. Reaching for colour to create hierarchy usually means the scale is too flat.

## Spacing and vertical rhythm

- Use the project spacing scale. Repeat values rather than inventing new ones.
- Space belongs between *related* things in smaller amounts and between *sections* in larger amounts. If the gap inside a group equals the gap between groups, the grouping is invisible.
- Section padding should vary with the weight of the section, not be a single constant applied everywhere.
- Whitespace is structural. Filling it with a decorative element is almost always a downgrade.

## Layout and responsive implementation

- Build the container and grid rules once, per `docs/design-system.md`, and compose inside them.
- Full-bleed elements should be a deliberate break from the container, not an accident of overflow.
- Implement the mobile composition that `premium-web-design` specified. Where it differs structurally from desktop, build it as a different composition — not as the same DOM squeezed narrower.
- Choose breakpoints from where *this* layout actually breaks, not from a default device list.
- Prefer intrinsic layout (flex wrapping, grid auto-placement, `clamp()`) over stacks of breakpoint overrides where it produces the same intent with less fragility.
- Guard against horizontal overflow at every step: wide tables, long unbroken strings, fixed-width media, and negative margins are the usual causes.

## Custom components over library defaults

Treat Tailwind, shadcn/ui and Radix as primitives. A component is finished when its typography, spacing, proportions, borders, radius and states come from this project's direction — not when it renders.

For every interactive component, implement all of its states, not just the resting one: hover, focus-visible, active, disabled, loading, error, and empty. A hover state that only lowers opacity is a placeholder.

Build the component once, in one place, and reuse it. The same button rendered three slightly different ways across a site is the most common source of "looks almost right but feels cheap".

## Content density

Match density to the audience and context. A takeaway menu wants dense and scannable; a campaign page wants air. Neither is a universal default.

Watch for the two failure modes: a page so sparse the visitor scrolls past nothing to reach anything, and a page so dense nothing is emphasised.

## Section transitions

Consider how one section meets the next. The options — a colour or surface change, a full-bleed image, a rule, a change of measure or alignment, a shift in density, or simply a larger gap — are design decisions.

Avoid alternating background greys as the only structural device, and avoid separating every section with an identical rounded container.

## Interaction design

- Motion must do a job: feedback, state change, orientation, or continuity. Decorative motion is removed.
- Keep transitions short for feedback and reserve longer ones for genuine state or route changes.
- Never gate content on scroll animation. Text must be present and readable without JavaScript having run.
- Respect `prefers-reduced-motion`.
- Interactive targets need visible focus states — this is a design requirement, not only an accessibility one.

## Consistency pass

Before considering the work done, check the whole surface for drift:

- One type scale, not several that nearly match.
- One radius system, applied with intent — not the same radius on every element.
- One spacing rhythm.
- One button and link vocabulary, with clear primary and secondary roles.
- One icon treatment, at consistent size and weight, used only where it aids comprehension.
- Images cropped and sized to a consistent logic.

## Polish

The difference between competent and premium is usually here:

- Optical alignment where mathematical alignment looks wrong.
- Real content edge cases handled: long names, missing images, one-item lists, empty states, error states.
- No layout shift as fonts and images load.
- Text remains legible over every image it sits on, at every crop.
- Loading and empty states designed, not defaulted.

## Handoff

Implementation is not finished at a successful build. Hand to **visual-qa**, which inspects the rendered result on desktop and at a narrow viewport. Then **accessibility-audit** and **performance-audit** before shipping.
