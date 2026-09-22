# New Website Project — Intake and Build Workflow

The canonical starting point for **any** new website built from this starter.

This workflow is fixed. The website it produces must not be. The starter standardises **quality and process**, never appearance.

It is deliberately niche-agnostic. It must work equally well for a local trade business, a restaurant, a hair salon, a construction firm, a sole trader, a law firm, a SaaS product, a B2B manufacturer, a webshop, a luxury label, an industrial supplier, a service provider, or a startup. No sector is the default, and no sector's conventions are assumed.

## The rule that governs everything below

> **Never infer the visual direction from previous projects, previous clients, common AI website patterns, or generic industry templates. Treat every new business as a new design problem.**

Do not assume the site should be premium, minimal, SaaS-like, modern, dark, playful, luxurious, or corporate. Each of those is a *choice* that must be earned by the business, its market, its audience and its conversion goal — never a starting position.

If a direction feels obvious before Phase 4 is finished, that is a warning sign, not progress.

## How this gets invoked

```
Use prompts/new-website-project.md for this project.

Business: [name, what they do]
What we already know: [context, assets, constraints]
Website goal: [primary outcome]
Available assets: [logo, photography, copy, brand guide, existing site]
```

Any of those lines may be missing or thin. Work with what is given.

## Operating rules

**Be autonomous.** Work through the phases without stopping to confirm each one. Produce the full chain of thinking and then the work.

**Use what already exists before asking anything.** Read the repository, any supplied documents, the existing website, and any linked profiles. Never ask for information that has already been provided or that is discoverable from the material at hand.

**Make reasonable assumptions and label them.** Where information is missing but a defensible assumption exists, state it explicitly as an assumption, record it in `docs/brand-direction.md`, and continue.

**Only ask when genuinely blocked.** Stop for a question only when a missing fact would change a strategic or technical decision materially and no safe assumption exists — for example the primary conversion action, a legal or regulatory constraint, whether real photography exists, or a required integration. Batch such questions into one short list rather than interrupting repeatedly.

**Write deliverables in the audience's language.** The language of this prompt is not the language of the website. A local business serving Dutch customers gets Dutch copy. Match the audience, not the briefing.

**The rules live elsewhere.** This file is the *procedure*. The constraints stay canonical in their own homes:

| File | Canonical for |
| --- | --- |
| `docs/anti-ai-slop.md` | Forbidden patterns, composition rules, copy rules, final audit checklist |
| `docs/design-system.md` | Token guardrails: typography, colour, spacing, radius, containers, grids, buttons, forms, motion |
| `docs/brand-direction.md` | This project's creative direction — filled in during Phase 6 |
| `AGENTS.md` | Cross-agent baseline and the canonical-source map |
| `CLAUDE.md` | Skill routing and the short workflow summary |

Read them; do not restate them.

---

## Phase 1 — Take stock of the context

Gather everything already known before asking for anything:

business name; products and services; audience; region and service area; price level; USPs; competitors; existing website; social profiles; logo; existing brand or house style; photography; supplied documents; the client's own stated wishes; technical requirements; required functionality.

Then state plainly:

- what is known;
- what is assumed, and on what basis;
- what is genuinely missing and would change a real decision.

Nothing else in this workflow may proceed on invented facts presented as known ones.

## Phase 2 — Business and conversion strategy

Before any design thinking, answer:

- What exactly is sold, and how does the business make money?
- Who buys it, and who else is involved in the decision?
- Why would a customer choose this business over the alternatives?
- What objections, hesitations or risks does a visitor bring?
- Which trust signals matter here — credentials, reviews, guarantees, photography of real work, prices, certifications, membership, years in business, named people?
- What is the **primary action**? Exactly one.
- Which secondary actions are worth supporting for visitors who are not ready?

The primary action varies enormously by business, and the whole site follows from it. It might be: calling, WhatsApp, booking an appointment, requesting a quote, placing an order, requesting a demo, submitting a lead form, visiting the physical shop, or buying a product directly.

Then classify the site, because it changes the architecture: local, national or international; B2C or B2B; ecommerce, lead generation, or informational.

A local business whose customers phone has almost nothing structurally in common with a B2B product that needs a demo request. Do not let one template serve both.

## Phase 3 — Market and competitive research

Where research tooling is available and the assignment allows it, examine real competitors and sector patterns. Public websites only.

Look past whether sites are attractive. Analyse:

which content recurs; which CTAs are used; trust elements; how price is communicated or avoided; photography style and quality; information architecture; how reviews are used; form length and friction; the mobile experience; recurring design patterns; what has become generic or overused in this sector; where there is room to differentiate credibly.

Two rules: **do not copy competitors**, and do not treat sector convention as a requirement. Research exists to make better decisions — including the decision to deliberately break a convention where that is credible, and to keep one where breaking it would confuse buyers.

If research is not possible, say so and proceed on stated assumptions rather than silently guessing.

## Phase 4 — Positioning

State concisely:

- audience;
- primary need;
- core value proposition;
- brand personality;
- desired feeling;
- conversion goal;
- differentiation.

**Vague adjectives are not answers.** "Modern", "clean", "premium" and "professional" mean nothing on their own — make them concrete and visual.

Not this:

> "Premium and modern."

This:

> "Calm and self-assured: generous negative space, editorial photography, short copy, subtle interaction. No glossy luxury clichés."

The test: could a designer who has never met this client produce work in the right direction from your positioning alone? If not, it is not specific enough yet.

## Phase 5 — Art direction

Now use the **`premium-web-design`** skill. It owns the creative direction.

Decide explicitly, each with a reason tied to this business:

visual direction; typography; colour strategy; spacing; composition; imagery and visual language; iconography; motion; UI density; shapes and radii; section rhythm; tone of voice.

Check the direction against `docs/anti-ai-slop.md` as you form it, and run that document's brand-transfer test.

The art direction must be specific to this project. No automatic repetition of earlier client sites, and no reaching for whatever is currently fashionable.

## Phase 6 — Brand direction document

Write the direction into `docs/brand-direction.md`. This becomes the project-specific source of truth for everything creative that follows.

Fill in at minimum: brand and context; audience; positioning; desired perception; primary conversion; tone of voice; typography direction; colour strategy; imagery direction; layout direction; motion direction; do's; don'ts; references or inspiration where they exist; and the assumptions made along the way.

The standard to meet: **another developer or designer could read this document and work in the same direction without having been in the conversation.** If it only makes sense to someone who saw the chat, it is not finished.

## Phase 7 — Site architecture

Only now decide structure:

single page versus multi-page; navigation; sections; page hierarchy; content flow; CTA placement; where trust signals sit relative to each decision point; forms; contact; footer; and any ecommerce or application flows.

**Every section needs a reason.** For each one, answer the three questions in `docs/anti-ai-slop.md`: why it exists, what question it answers, what the visitor does next.

Do not reach for hero → three cards → testimonials → FAQ → CTA as a default skeleton. That sequence is the single most recognisable AI-website structure. Some businesses genuinely need parts of it; assemble the structure this business needs, and delete anything that exists only because sites usually have it.

Trust and proof belong *above* the ask, not after it.

## Phase 8 — Content strategy

Before implementing, outline the content. For each significant page or section define:

- **purpose** — what it is for;
- **message** — what it says;
- **proof** — what makes it believable;
- **CTA** — what happens next, if anything.

Copy must sound human and specific, fit this business, and avoid AI marketing register. `docs/anti-ai-slop.md` holds the copy rules.

Where real business information exists, use it. Placeholder fluff is only acceptable where genuine content is unavailable, and it must be flagged as needing replacement rather than shipped quietly.

## Phase 9 — Build plan

Produce a concrete implementation plan, using **`frontend-design`** for the design implementation approach and **`nextjs-project-standards`** for engineering conventions.

Cover: pages and routes; component structure; data and its source; forms and their handling; integrations; image requirements; fonts; animations; the responsive approach; and technical risks.

**Do not over-engineer.** Most sites built from this starter are marketing or small-business sites. No CMS, state library, or abstraction layer before there is a real need for it.

## Phase 10 — Implementation

Only now write code.

While implementing: follow `docs/brand-direction.md`, `docs/design-system.md` and `docs/anti-ai-slop.md`; use the skills; keep the brand consistent across every surface; design desktop and mobile as two deliberate compositions rather than one scaled layout; and where shadcn or any component library is used, restyle it to this project's direction — a library default is a starting point, never finished design.

## Phase 11 — QA

Run, as relevant: **`visual-qa`**, then **`accessibility-audit`**, then **`performance-audit`**.

A build that compiles is not a finished website. Where browser or dev-server tooling is available, inspect the real rendered result on desktop and at a narrow viewport. If that tooling is genuinely unavailable, say the work was not visually verified rather than implying it was.

## Phase 12 — Final design review

Answer these explicitly before delivering:

1. Does the site have a recognisable identity of its own?
2. Does it genuinely suit *this* business?
3. Is the hierarchy clear?
4. Was mobile deliberately designed?
5. Is the desktop version composed and confident?
6. Have any generic AI patterns crept in?
7. Do sections look too much like one another?
8. Are components repeated because it was easy, or because it is functionally right?
9. Is the copy specific enough?
10. Is every animation doing a job?
11. Is the primary CTA unmistakable?
12. Could this credibly have been made by a human designer?

Then run the final checklist in `docs/anti-ai-slop.md`.

Where the answer to a relevant question is no: **fix it and re-inspect before calling the project done.** Report what was found and fixed rather than presenting the first pass as final.

---

## Anti-monoculture rule

A shared starter does **not** mean projects should share a visual language. The opposite is the point.

These may differ fundamentally from one project to the next, and usually should:

fonts · grid · spacing · border radius · button shapes · colour system · imagery · interaction style · hero composition · section structure · navigation · visual density · motion

Two sites built from this starter should not be recognisable as siblings. If a new project is drifting toward the same solution as a previous one, that is a defect in the process — return to Phase 4 and 5 and decide again from this business.

The starter standardises **quality and process, not appearance.**

## Definition of done

- Context, strategy and positioning were established before any design decision.
- The art direction is specific to this business and reasoned, not defaulted.
- `docs/brand-direction.md` is filled in well enough for someone else to continue from it.
- Every section earns its place.
- Copy is specific and in the audience's language.
- The rendered result was inspected on desktop and mobile, or the absence of tooling was stated.
- Accessibility and performance were audited.
- The final review in Phase 12 and the checklist in `docs/anti-ai-slop.md` both pass.
- Assumptions are documented, and anything still needing real content or a client decision is listed plainly.
