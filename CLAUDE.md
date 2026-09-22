# Claude Project Instructions

For all UI, visual design, landing-page, form, content-layout, and responsive work:

- Read `AGENTS.md`.
- Read `docs/anti-ai-slop.md`.
- Read `docs/brand-direction.md`.
- Read `docs/design-system.md`.

Treat those documents as mandatory project constraints.

Do not default to generic AI/SaaS aesthetics. Do not introduce untouched shadcn styling, generic three-card feature rows, gradient hero text, badge-over-headline patterns, excessive Lucide icons, glassmorphism, random grain, cursor beams, or universal fade-in-on-scroll.

Before completing visual work, perform the anti-AI-slop audit and repair anything that feels template-derived or transferable to an unrelated brand.

## Starting a new website project

Follow `prompts/new-website-project.md`. It is the canonical intake and build workflow for any new site — context, business and conversion strategy, research, positioning, art direction, architecture, content, build plan, implementation, QA and final review. It is not duplicated here.

## Skills

This repository ships its own skills in `.claude/skills/`. They are the *procedures*; the documents above remain the *rules*.

| Skill | Use it for |
| --- | --- |
| `premium-web-design` | Deciding the art direction before building: brand, audience, positioning, emotion, typography, composition, imagery, mobile intent, conversion flow. **Owns the creative direction.** |
| `frontend-design` | Implementing that direction at production quality: composition, rhythm, spacing, responsive layout, custom components, states, polish. |
| `visual-qa` | Looking at the actually rendered page on desktop and a narrow viewport, fixing what is wrong, and re-inspecting. |
| `nextjs-project-standards` | Our project conventions and architectural defaults: App Router, server/client boundaries, images, fonts, metadata, forms, dependencies, environment variables, security. For current framework and API details, defer to the `vercel:nextjs` skill. |
| `accessibility-audit` | Final accessibility pass. Native HTML first, ARIA only where it earns its place. |
| `performance-audit` | LCP, CLS, client-component creep, bundle and asset cost — without degrading the design. |

## Workflow for website work

```
Research / context
      ↓
premium-web-design      ← art direction decided and written down
      ↓
frontend-design         ← direction implemented
      ↓
Implementation          ← nextjs-project-standards
      ↓
visual-qa               ← the rendered result is inspected
      ↓
accessibility-audit
      ↓
performance-audit
      ↓
Final anti-AI-slop review (docs/anti-ai-slop.md)
```

Use judgement about how much of it applies. Not every change needs the full chain:

- Changing button text or a copy string — just do it.
- A new page, hero, or full site — the complete workflow.
- A reported responsive problem — `visual-qa`, targeted at the failing widths.
- Preparing for production — `visual-qa`, then accessibility and performance audits.
- Writing application code inside an existing design — `nextjs-project-standards`.

Two rules that do not bend:

1. **No UI is designed before the brand direction exists.** If `docs/brand-direction.md` is still a template, filling it in is the first deliverable.
2. **UI is not done because it compiles.** Where browser or dev-server tooling is available, look at the rendered page before reporting the work complete.

## No design monoculture

This starter enforces a consistent *quality standard*, never a consistent *look*. A hair salon, a takeaway, an energy company, a law firm and a luxury clothing label must not end up with the same hero, cards, fonts, motion, borders, layout, or colour strategy. Every project decides its own art direction in `premium-web-design` first.
