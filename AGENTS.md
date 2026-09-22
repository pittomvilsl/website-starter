# Agent Instructions

These instructions apply to every coding agent working in this repository.

## Where the rules live

To prevent the same rule drifting into three different versions, each rule has exactly one home. Update the canonical file; everything else points at it.

| File | Canonical for | Duplicates rules? |
| --- | --- | --- |
| `docs/anti-ai-slop.md` | Forbidden patterns, composition rules, copy rules, final audit checklist | — |
| `docs/design-system.md` | Token guardrails: typography, colour, spacing, radius, containers, grids, buttons, forms, motion, responsive | — |
| `docs/brand-direction.md` | The per-project brand brief. A template until a project fills it in | — |
| `AGENTS.md` | The cross-agent baseline that applies to every tool | Points to docs |
| `CLAUDE.md` | Claude's entry point and workflow routing | Points to docs and skills |
| `.cursor/rules/design.mdc` | Cursor's entry point | Points to docs |
| `.claude/skills/*/SKILL.md` | **Procedures** — how to work, step by step | Points to docs for the rules |

The distinction that keeps this coherent: **documents state the rules, skills describe the procedure.** A skill that restates the blacklist instead of referencing it has introduced drift — fix the skill, not the document.

Claude additionally has skills in `.claude/skills/`: `premium-web-design`, `frontend-design`, `visual-qa`, `nextjs-project-standards`, `accessibility-audit`, `performance-audit`. Agents without skill support get the same standard from this file and `docs/` — the rules do not depend on the skills existing.

## Mandatory UI workflow

Before creating, redesigning, or materially modifying any user-facing UI, read:

1. `docs/anti-ai-slop.md`
2. `docs/brand-direction.md`
3. `docs/design-system.md`

These files are hard design constraints. If a proposed UI pattern conflicts with them, the repository rules win.

## Before coding UI

State briefly:
- the art direction being applied;
- the visual hierarchy;
- which generic AI-design patterns are being avoided;
- whether the change introduces a new component or reuses an existing branded primitive.

Do not begin a broad redesign from a generic SaaS template or component-library default.

## During implementation

- Preserve established spacing, typography, color, radius, motion, and content rules.
- Treat shadcn/Radix/Tailwind primitives as implementation tools, not finished visual design.
- Prefer brand-specific composition over generic card grids.
- Use icons only when they improve comprehension.
- Keep mobile as a deliberate layout, not a scaled-down desktop.
- Do not add decorative gradients, glassmorphism, grain, glows, beams, pills, or scroll animations unless the brand direction explicitly justifies them.

## Required final UI audit

Before declaring UI work complete, run the checklist in `docs/anti-ai-slop.md` and fix violations.

A change is not done merely because it looks modern. It must look intentional, brand-specific, coherent, usable, and difficult to transplant unchanged to an unrelated SaaS/AI/crypto site.
