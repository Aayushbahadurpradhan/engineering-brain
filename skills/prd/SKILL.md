---
name: prd
description: Generate a Product Requirements Document (PRD) for a new feature — clear, actionable, sized for implementation. Use when planning a feature, starting a project, or asked to write a PRD. Often the first step before an autonomous build loop turns the PRD into stories. Triggers: "create a prd", "write prd for", "plan this feature", "requirements for", "spec out".
user-invocable: true
---

# PRD Generator

Create detailed Product Requirements Documents that are clear, actionable, and suitable for
implementation by a junior developer or an AI agent. Adapted from the open-source
[snarktank/ralph](https://github.com/snarktank/ralph) PRD format; pairs with any autonomous build
loop that converts a PRD into independently-shippable stories.

## The Job
1. Receive a feature description.
2. Ask 3–5 essential clarifying questions (lettered options).
3. Generate a structured PRD from the answers.
4. Save to `tasks/prd-<feature-name>.md`.

**Do NOT start implementing — only produce the PRD.**

## Step 1: Clarifying Questions
Ask only where the prompt is ambiguous. Focus on: Problem/Goal, Core Functionality,
Scope/Boundaries, Success Criteria. Format so the user can answer "1A, 2C, 3B":
```
1. What is the primary goal of this feature?
   A. ...
   B. ...
   C. Other: [specify]
```

## Step 2: PRD Structure
Generate these sections:
1. **Introduction/Overview** — the feature and the problem it solves.
2. **Goals** — specific, measurable objectives (bullets).
3. **User Stories** — each with Title, Description ("As a [user], I want [feature] so that
   [benefit]"), and a **verifiable** Acceptance Criteria checklist. Each story small enough for
   one focused session. UI stories must include "Verify in browser using dev-browser skill".
4. **Functional Requirements** — numbered, explicit, unambiguous ("FR-1: The system must…").
5. **Non-Goals (Out of Scope)** — what it will NOT do. Critical for scope control.
6. **Design Considerations** (optional) — UI/UX, mockups, components to reuse.
7. **Technical Considerations** (optional) — constraints, dependencies, integration points.
8. **Success Metrics** — how success is measured.
9. **Open Questions** — remaining unknowns.

## Quality bar
- Acceptance criteria are **verifiable**, not vague. Bad: "works correctly". Good: "button
  shows a confirmation dialog before deleting".
- Stories are small and independently shippable (so a build loop can do one per iteration).
- Be explicit; avoid unexplained jargon; number requirements for reference.

## Output
- Markdown, saved to `tasks/prd-<feature-name>.md` (kebab-case).

## Checklist
- [ ] Asked clarifying questions with lettered options.
- [ ] Incorporated the answers.
- [ ] Stories small, specific, dependency-ordered.
- [ ] Functional requirements numbered and unambiguous.
- [ ] Non-goals define clear boundaries.
- [ ] UI stories include browser verification.
- [ ] Saved to `tasks/`.
