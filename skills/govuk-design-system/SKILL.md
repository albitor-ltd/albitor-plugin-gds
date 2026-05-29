---
name: govuk-design-system
description: Use when building, reviewing, or discussing a GOV.UK or UK public sector frontend — any HTML/Nunjucks/React/Svelte UI that should follow the GOV.UK Design System. Covers the 34 components, page and "ask users for information" patterns, the GOV.UK colour/typography/layout/spacing styles, and how to consume GOV.UK Frontend (Nunjucks macros or copied HTML) with progressive enhancement.
---

# GOV.UK Design System

Help developers build interfaces that follow the GOV.UK Design System so they look and behave like a real GOV.UK service and pass a service assessment.

## Core principles (apply these first)

1. **Use a component if one exists.** The Design System has a vetted, accessible component for almost every common need. Reach for it before inventing markup. The full catalogue is in `references/components.md`.
2. **Do not restyle components.** Keep the `govuk-*` classes and their meaning. Don't recolour buttons, change input borders, or repurpose the red error styling. Consistency across government is the point.
3. **Build with progressive enhancement.** The non-JavaScript HTML must work on its own; JS only enhances it. Server-side validation is mandatory even when client-side validation exists.
4. **Compose with patterns, not just components.** A "question page", "check your answers" page, or "ask for an address" flow is a *pattern* — a tested arrangement of components and content. See `references/patterns.md`.
5. **Accessibility is not optional.** Every choice here exists partly for accessibility. Pair this with the `govuk-accessibility` skill when auditing.

## Bundled references — read the relevant one before answering in detail

| File | When to read it |
| --- | --- |
| `references/components.md` | Choosing/implementing any UI element. Lists all 34 components, their Nunjucks macro (`govuk*`), whether they need JS, when (not) to use them, and accessibility gotchas. |
| `references/patterns.md` | Designing a page or a flow, or asking users for information (names, addresses, dates, NINo, passwords, etc.). |
| `references/styles.md` | Colour, typography, the grid/layout, spacing scale, the page template, links and focus states. |
| `references/frontend-conventions.md` | Installing/using GOV.UK Frontend, Nunjucks vs plain HTML, `initAll`, the page template, and consuming the markup from a React/Svelte/other stack. |

These are distilled from the live GOV.UK Design System and GOV.UK Frontend (Crown Copyright, Open Government Licence v3.0). They are a fast index — for exact, current detail always confirm against <https://design-system.service.gov.uk/> and <https://frontend.design-system.service.gov.uk/>, especially colours (the 2025 GOV.UK brand refresh changed several functional colour values).

## Working rules

- **Don't hardcode hex colours.** Use the `govuk-colour()` Sass function or the functional colour helpers so the build stays correct across brand updates. See `references/styles.md`.
- **Prefer macros where the stack allows.** In Nunjucks/Node, use the official `govuk-frontend` macros — they keep markup correct as the library updates. In React/Svelte/etc., copy the component's HTML, keep every class, and port the JS behaviour (focus management, toggles) faithfully; note this is a maintenance cost you take on.
- **Forms:** every input needs an associated `<label>` (or `<legend>` in a `<fieldset>` for grouped controls). Never use placeholder text as a label. On error, render the error summary at the top (focused on load), link each entry to its field, and add the inline error message + error modifier classes.
- **Page furniture:** use the GOV.UK header, footer (with the OGL/licence links), `govuk-width-container`, and a phase banner (Alpha/Beta) where relevant.
- When the user is starting a service, suggest the official **GOV.UK Prototype Kit** for prototyping but remind them production code should use `govuk-frontend` directly.

## Related

- `govuk-accessibility` skill — WCAG 2.2 AA and the legal regulations these components help you meet.
- Commands: `/gds:component`, `/gds:review`.
