---
name: performance-audit
description: Audit and fix front-end performance without damaging the design — LCP, CLS, unnecessary JavaScript, client component creep, heavy dependencies, oversized images, font loading, image dimensions, lazy loading, hydration cost, animation cost, third-party scripts and bundle impact. Use before shipping, when a site feels slow, or when Core Web Vitals need to improve.
---

# Performance Audit

Fast because it is built well, not fast because the design was stripped out.

**The constraint:** performance work must not quietly degrade the art direction. Removing the hero image, dropping a custom typeface, or deleting a considered interaction to win a score is a design regression, not an optimisation. Where a real trade-off exists, fix the implementation first, and only then raise the trade-off explicitly.

## Measure before changing anything

Guessing wastes effort on the wrong bottleneck. Establish what is actually slow:

- Load the real page and inspect network requests: what is requested, how large, in what order, and what blocks rendering.
- Identify the LCP element and what delays it.
- Check the console for errors and warnings.
- Build the project and read the output — route-level JavaScript sizes and the shared bundle.
- Measure on a throttled connection and a slow-CPU profile. A site that is fast on a developer laptop tells you very little.

Record the baseline so improvements can be demonstrated rather than asserted.

## LCP

Usually the hero image or the main headline.

- Preload or prioritise the LCP image — `priority` on `next/image` for exactly that image, and nothing else.
- Do not lazy-load anything above the fold. This is a frequent and severe self-inflicted regression.
- Serve it at the right size with a correct `sizes` attribute, in a modern format.
- Remove render-blocking resources from the critical path: blocking scripts, third-party stylesheets, and fonts loaded from an external origin.
- If the LCP element is text, ensure the font is not blocking paint.
- Prefer static or cached rendering so the document arrives quickly; a slow server response caps everything downstream.

## CLS

- Every image has explicit dimensions or a sized container with a known aspect ratio.
- Fonts loaded with `display: swap` and fallbacks matched for size, so the swap does not reflow the page.
- Space reserved for anything that arrives late: embeds, ads, banners, consent dialogs.
- Nothing is injected above existing content after load.
- Skeletons match the dimensions of the content they stand in for.
- Watch the page load and reload it several times — CLS is often only visible on a cold, throttled load.

## Unnecessary JavaScript and client component creep

The most common cause of a slow site built this way.

- Audit every `"use client"`. Does it need state, effects, browser APIs or event handlers? If not, it belongs on the server.
- Find client directives placed too high in the tree — a page marked as client makes its entire subtree client code. Move the boundary down to the smallest interactive leaf.
- Server-render static content instead of hydrating it.
- Remove dead code, unused components, unused exports, and leftover experiments.
- Dynamically import genuinely heavy, genuinely below-the-fold components — modals, rich editors, maps, charts, video players.
- Avoid shipping data to the client that was only needed to render on the server.

## Dependencies and bundle impact

- Check the installed size and the client-side cost of each dependency. Large date, icon, animation and utility libraries are the usual offenders.
- Import only what is used; avoid barrel imports that defeat tree-shaking.
- Import icons individually rather than pulling in an entire icon set — and per `docs/anti-ai-slop.md`, most decorative icons should not be there at all.
- Replace a heavy library used for one function with a small local implementation or a platform API (`Intl`, native `<dialog>`, CSS animation).
- Check for duplicate libraries doing the same job, and for multiple versions of the same package.

## Images

- Correct format — modern formats for photography, SVG for flat graphics.
- Correct dimensions: never ship a 3000px image to render at 600px.
- Responsive `sizes` so phones do not download desktop assets.
- Compress. Large unoptimised photography is routinely the largest payload on a small site.
- Lazy-load below-the-fold images only; never the LCP image.
- Video: no autoplaying background video without a strong reason, a poster frame, and a mobile fallback.

## Fonts

- Self-host through `next/font` rather than a third-party stylesheet request.
- Load only the weights and styles the design actually uses.
- Subset to the required character sets.
- `display: swap` with a size-matched fallback.
- Preload only the font that renders first; preloading everything defeats the purpose.
- Variable fonts can replace several static weights at lower total cost — check before assuming.

## Hydration

- Large hydrated trees delay interactivity even when the HTML arrives quickly. Reduce the amount of client code rather than trying to make hydration faster.
- Avoid expensive work in effects that run on mount.
- Stabilise dependencies so components are not re-rendering on every state change.
- Keep the props crossing the server–client boundary small; large serialised payloads are shipped twice.

## Animation

- Animate only `transform` and `opacity`. Animating layout properties forces reflow and will feel bad on a phone.
- Avoid continuous animation, scroll-linked effects and large blur or backdrop-filter surfaces — these are expensive, and mostly on the blacklist already.
- Use CSS for simple transitions instead of pulling in an animation library.
- Honour `prefers-reduced-motion`, which is both an accessibility and a performance win.

## Third-party scripts

Often the single heaviest thing on an otherwise well-built site.

- List every third-party script and justify each one. Remove the ones nobody uses.
- Load non-essential scripts after the page is interactive, with the appropriate loading strategy.
- Prefer lightweight, privacy-respecting analytics.
- Chat widgets, cookie banners, tag managers and embeds each carry real cost — load them late, and consider loading an embed only on interaction.
- Self-host what can be self-hosted to avoid extra connections.

## Caching and delivery

- Static rendering where content allows; revalidate on a schedule where it changes occasionally.
- Correct cache headers for static assets.
- Avoid unnecessary redirect chains.
- Verify what the production build actually does — development performance is not representative.

## Verify and report

Re-measure after the changes and compare against the baseline. Then confirm the design survived: run `visual-qa` again if anything structural moved, particularly if images, fonts or animations changed.

Report the baseline, what changed, the measured result, and any trade-off that was made or deliberately declined.
