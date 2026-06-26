---
name: design-md
description: Generate a DESIGN.md design-system file for a project root so any coding agent builds visually consistent UI. Captures color tokens, typography, spacing, components, and rules in one file the agent reads before building frontend. Use when starting frontend work, when UI is coming out inconsistent, or asked to "set up a design system / DESIGN.md / design tokens / style guide for the agent". Triggers: "design.md", "design system file", "design tokens", "make the agent build consistent UI", "style guide for coding agent".
---

# DESIGN.md Generator

## Purpose
Produce a single `DESIGN.md` at the project root that encodes the project's visual language as
explicit tokens and rules. A coding agent reads it before generating any UI, so pages stay
visually aligned instead of drifting every prompt. One file in, consistent design out.

## Activation Criteria
Trigger when: starting a new frontend/app, UI output is inconsistent across screens, adopting a
brand's look, or an explicit "create a DESIGN.md / design system / design tokens" request. Not for
one-off styling of a single component (use `web-design-guidelines` directly).

## Inputs
- Brand or product references: existing site/app, logo, brand colors, any Figma, or "make it look
  like X".
- Target stack (Tailwind, CSS vars, styled-components, etc.) so tokens are emitted in a usable form.
- If a design exists, the current UI to reverse-engineer tokens from.

## Workflow
1. **Gather the design language.** From references/brand, extract the palette, type, mood (e.g.
   "clean fintech", "playful"). If reverse-engineering, sample real values from the live UI.
2. **Define tokens, not one-offs.** Color (semantic: bg/surface/primary/accent/danger + states),
   typography (font families, scale, weights, line-heights), spacing scale, radius, shadow/elevation,
   breakpoints, motion (durations/easings).
3. **Codify rules.** The do/don't list: never use browser-default colors, contrast/a11y minimums,
   when to use primary vs accent, density, focus-ring style, dark-mode handling.
4. **Map components.** For core components (button, input, card, modal, nav) state the variants and
   which tokens each uses — so the agent composes from the system, not ad hoc.
5. **Emit in the project's format.** Provide tokens both as a readable table AND as a paste-ready
   block for the stack (e.g. Tailwind `theme.extend`, or CSS custom properties).
6. **Place & wire it.** Write `DESIGN.md` to the project root and add a one-line pointer so the
   agent loads it before frontend work (in this repo: reference it from `standards/frontend.md`).

## DESIGN.md structure (the file you generate)
```
# DESIGN.md — <project> design system
## Brand & mood          # one paragraph: the feeling the UI should evoke
## Color tokens          # semantic names → values, + states (hover/active/disabled), + dark mode
## Typography            # families, type scale, weights, line-heights
## Spacing & layout      # spacing scale, container widths, breakpoints, grid
## Radius / shadow / motion
## Components            # per component: variants + tokens used
## Rules (do / don't)    # the guardrails an agent must follow
## Tokens for <stack>    # paste-ready config block
```

## Checklist
- [ ] Colors are semantic tokens with states, not raw hex scattered in prose.
- [ ] Type scale + spacing scale are explicit numeric ramps.
- [ ] Accessibility minimums (contrast, focus rings) stated as rules.
- [ ] Tokens emitted in the actual target stack's format (paste-ready).
- [ ] `DESIGN.md` written to project root and referenced so the agent auto-loads it.

## Deliverables
- `DESIGN.md` at the consuming project's root, following the structure above.

Pairs with `web-design-guidelines` (aesthetic rules), `frontend-design`, and `standards/frontend.md`.
Concept based on the Google-style `DESIGN.md` / project-root design-spec convention.
