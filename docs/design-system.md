# Design System Guardrails

This file defines the default system. Adjust deliberately per project.

## Typography

Define:
- primary font
- optional secondary/accent font
- heading scale
- body scale
- line height
- weights
- maximum text width

Do not choose fonts purely because they are currently trendy.

## Color

Define:
- primary brand color
- neutrals
- semantic colors
- surface/background colors
- interaction states

Avoid gratuitous gradients and low-contrast styling.

## Spacing

Use a consistent 4px-based scale, favoring:

`4, 8, 12, 16, 24, 32, 48, 64, 80, 96`

Prefer repeated values over arbitrary one-offs.

## Radius

Define a small, deliberate radius system.

Do not turn every section into a rounded floating card.

## Borders and shadows

Prefer subtle structure over heavy shadow stacks.

Glassmorphism is not a default surface style.

## Buttons

Define:
- primary
- secondary
- destructive if needed
- hover
- focus
- disabled
- loading

Do not use decorative glow or opacity-only hover effects.

## Forms

Prioritize:
- clear labels
- error states
- focus behavior
- mobile tap targets
- progress clarity
- confidence around data entry

Do not hide essential labels inside placeholders.

## Icons

Use icons sparingly and consistently.

An icon should communicate meaning faster than text or support a control.

## Motion

Default to subtle state transitions.

Use larger motion only for meaningful state changes, navigation, progression, or storytelling.

No blanket fade-in-on-scroll system.

## Responsive behavior

Mobile is a first-class layout.

Explicitly review:
- heading wrapping
- CTA placement
- form usability
- image crops
- stacking order
- section spacing
- touch targets

A desktop layout may be recomposed on mobile instead of merely stacked.
