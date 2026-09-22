# Website Starter

Reusable starter for AI-assisted websites that should feel intentionally designed, brand-specific, and production-ready rather than generically AI-generated.

## Required workflow

1. Fill in `docs/brand-direction.md`.
2. Adapt `docs/design-system.md` to the brand.
3. Keep `docs/anti-ai-slop.md` as the shared quality standard.
4. Let coding agents read `AGENTS.md` and `CLAUDE.md` before UI work.
5. Run the final anti-AI-slop audit before shipping.

Recommended sequence:

`brand direction → design system → composition → implementation → responsive review → anti-AI-slop audit`

Do not start by asking an agent to "make a modern premium website". Define the brand first.

## Starting a new website

```
Use prompts/new-website-project.md.

Project:
[business / context]
```

`prompts/new-website-project.md` is the canonical intake workflow: context and strategy first, art direction next, code last.

## Claude Code skills

Claude gets the same standard as a set of procedures in `.claude/skills/`:

`premium-web-design` (art direction) → `frontend-design` (implementation) → `nextjs-project-standards` (project conventions) → `visual-qa` (inspect the rendered page) → `accessibility-audit` → `performance-audit`

`nextjs-project-standards` holds our own conventions and architectural defaults. Current framework and API knowledge stays with the Vercel plugin's `vercel:nextjs` skill — the two are complementary, and the names are kept distinct on purpose.

The skills describe *how to work*. The rules stay in `docs/`. `AGENTS.md` records which file is canonical for what, so the same rule does not drift into several versions.

This starter standardises quality, not appearance. Every project decides its own art direction before any UI is built — sites built from it should not look like siblings.

## GitHub template usage

Once this repository is marked as a GitHub template repository, start new projects with:

`Use this template → Create a new repository`
