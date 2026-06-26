---
name: frontend-design
description: Enforces HTML semantics, CSS tokens, responsive layouts, and accessibility standards. Use when implementing frontend interfaces.
---

# Frontend Design Implementation

You are responsible for turning design guidelines into robust, accessible code.

## Core Directives
1. **Semantic HTML:** Always use proper HTML5 elements (`<article>`, `<section>`, `<nav>`, `<main>`, `<aside>`) rather than nested `<div>` soup.
2. **Accessibility (a11y):** All interactive elements must have `aria-labels` or discernible text. Maintain proper contrast ratios and ensure full keyboard navigability.
3. **Responsiveness:** Build mobile-first. Ensure fluid typography and flexible grid/flexbox layouts that scale elegantly to desktop.
4. **Styling Consistency:** Strictly use the project's chosen CSS architecture (Vanilla CSS with variables, or Tailwind if strictly requested). Do not mix methodologies inline.

## Workflow
1. Scaffold the semantic HTML skeleton.
2. Apply CSS variables/tokens.
3. Test responsiveness across breakpoints.
4. Verify keyboard focus and accessibility tags.
