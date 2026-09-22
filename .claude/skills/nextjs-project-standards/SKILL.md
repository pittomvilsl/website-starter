---
name: nextjs-project-standards
description: Project conventions and architectural defaults for websites built from this starter — Next.js App Router, TypeScript, Tailwind, shadcn/ui where useful, deployed on Vercel. Covers server and client component boundaries, images, fonts, metadata, semantic markup, forms, loading and error states, dependencies, environment variables and security basics. Use when scaffolding a project or writing application code here. For current framework and API details, defer to the Vercel Next.js skill.
---

# Next.js Project Standards

House engineering rules for sites built from this starter. These are conventions, not dogma — a good reason to deviate, stated in the code or the PR, beats compliance.

**Scope versus the Vercel plugin.** This skill holds *our* project conventions and architectural defaults — the decisions that should be the same across every site we build. The `vercel:nextjs` skill (and the rest of the Vercel plugin) holds *current framework and API knowledge* — caching semantics, Server Actions details, middleware, routing APIs, deployment behaviour. When the framework changes, the Vercel skill is right and this file is the thing to re-check. Use both: this one for how we build, that one for how the framework currently works.

## First: check what the project actually is

**This starter ships no application code.** It is design and process scaffolding. Every project built from it picks its own versions.

Before applying any version-specific guidance, read what is actually there:

- `package.json` — Next.js, React and Tailwind major versions; package manager
- `next.config.*` — existing configuration
- `tsconfig.json` — paths, strictness
- `app/` vs `pages/` — which router is in use
- Tailwind v3 (`tailwind.config.*`) vs v4 (CSS-first `@theme`) — these configure very differently

Never write instructions or code that contradict the installed versions. If the project is on the Pages Router, work with the Pages Router rather than half-migrating it mid-task.

For deep framework API questions — caching semantics, Server Actions details, middleware, deployment behaviour — prefer the `vercel:nextjs` skill if it is available in the session. This file covers *how we build here*, not the framework reference.

## Rendering and component boundaries

- App Router by default on new projects.
- **Server Components are the default.** Add `"use client"` only when the component needs state, effects, browser APIs, or event handlers.
- Push `"use client"` to the leaves. A client directive at the top of a page turns the whole subtree into client code — this is the single most common cause of bloated bundles in these projects.
- Keep data fetching on the server. Do not fetch in a client `useEffect` what the server could have rendered.
- Isolate the interactive part: a mostly static section with one interactive control should be a server component wrapping a small client component, not a client page.
- Pass serialisable props across the boundary; keep the payload small.

## Images

- Use `next/image`. Always set `width`/`height` or `fill` with a sized container — unsized images cause layout shift.
- Set `priority` on the LCP image, typically the hero. Do not set it on anything else.
- Use `sizes` whenever the rendered width varies responsively, otherwise oversized images are downloaded on phones.
- Write real `alt` text, or `alt=""` for genuinely decorative images.
- Art direction from `premium-web-design` may require different crops per breakpoint — implement that deliberately rather than letting one crop fail on mobile.

## Fonts

- Load fonts through `next/font` so they are self-hosted and preloaded, with no render-blocking third-party request.
- Set `display: "swap"` and choose fallbacks that limit shift.
- Subset to the character sets actually needed, and load only the weights the design uses. Loading nine weights to use two is a common and expensive mistake.
- The typeface is a brand decision made in `premium-web-design` — this is only how it gets loaded.

## Metadata and SEO

- Use the Metadata API. Every route needs a title and description.
- Set `metadataBase`, canonical URLs, Open Graph and Twitter metadata for anything shareable.
- Use `generateMetadata` for dynamic routes.
- Provide a favicon set, `robots` and a sitemap for public sites.
- Add structured data where it genuinely applies (local business, product, article) — not as decoration.
- Set `lang` on `<html>` correctly, particularly for non-English sites.

## Semantic HTML

Native elements first. This is the cheapest accessibility and SEO win available.

- One `<h1>` per page; heading levels descend without skipping.
- `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` where they apply.
- `<button>` for actions, `<a>` for navigation — never a `div` with a click handler.
- `<form>` with real inputs and real labels.
- Lists as lists, tables as tables with proper headers.

## Forms

- Progressive enhancement where practical: a form that works before JavaScript loads is more robust.
- Validate on the server. Client validation is a convenience, never the boundary.
- Use a schema validator (for example Zod) and share the schema between client and server rather than defining the rules twice.
- Design the full state machine: idle, submitting, success, field error, form-level error. Disable submit while in flight and prevent double submission.
- Errors must be specific, adjacent to the field, and programmatically associated with it.
- Preserve user input on failure. Never clear a form because the server rejected one field.
- Use correct `type`, `inputMode`, `autocomplete` and `name` attributes — this is most of mobile form usability.
- Protect public endpoints against spam and abuse (rate limiting, and a honeypot or a privacy-respecting challenge) before launch.

## Loading and error states

- Provide `loading.tsx` and `error.tsx` where a route can be slow or fail.
- Use Suspense boundaries around genuinely slow sections rather than blocking the whole page.
- Design skeletons to match the real layout so nothing jumps when content arrives. A generic spinner in the middle of the page is a fallback, not a design.
- Add `not-found.tsx` and a designed 404. It is a real page and gets real traffic.
- Error states should be understandable to a visitor, not a stack trace.

## Dependencies

- Add a dependency only when it does something meaningful that would otherwise be substantial to write and maintain.
- Check the installed weight and whether it ships client-side before adding it. A large date or animation library pulled in for one call is not worth it.
- Prefer platform features: CSS grid, container queries, `Intl`, the native `<dialog>` element, the View Transitions API where support allows.
- Use shadcn/ui when it saves real work, particularly on accessible primitives — then restyle it to the project's direction. An unmodified shadcn component is a starting point, not a finished one (see `docs/anti-ai-slop.md`).
- Do not add a state-management library, an ORM, or a component library to a brochure site.

## Avoid over-engineering

Most sites built from this starter are marketing and small business sites. Build for that:

- No abstraction until there are at least two real uses.
- No premature CMS, feature-flag system, or micro-frontend split.
- Co-locate components with their route until reuse is real.
- Typed props, clear names, no cleverness that the next person has to decode.

## TypeScript

- `strict: true`. Fix type errors rather than casting past them.
- Avoid `any`; prefer `unknown` plus narrowing at boundaries.
- Type external data where it enters the application — API responses, form payloads, environment variables.

## Environment variables and security basics

- Only `NEXT_PUBLIC_*` variables reach the browser. **Anything with that prefix is public** — never put a secret behind it.
- Keep secrets server-side: Server Components, route handlers, Server Actions.
- Validate environment variables at startup and fail loudly on a missing one, rather than shipping an undefined value into a template.
- Commit `.env.example` with keys and no values. Never commit `.env*` files with real values, and confirm `.gitignore` covers them.
- Validate and escape anything user-supplied. Avoid `dangerouslySetInnerHTML`; sanitise if it is genuinely unavoidable.
- Treat CMS and third-party content as untrusted input.
- Set sensible security headers before launch; add a Content Security Policy if the site accepts input or handles anything sensitive.
- Never log secrets or personal data.

## Performance defaults

- Static rendering wherever the content allows; revalidate on a schedule when content changes occasionally.
- Keep third-party scripts minimal and load them with the appropriate strategy. Analytics and chat widgets are usually the heaviest thing on a small site.
- Confirm the real cost before shipping — see the `performance-audit` skill.

## Relationship to the design skills

This skill covers implementation quality. It does not decide layout, typography or visual treatment — `premium-web-design` sets the direction and `frontend-design` implements it. Where a technical convention and the design direction genuinely conflict, raise it rather than silently resolving it in either direction.
