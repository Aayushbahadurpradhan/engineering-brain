---
name: knowledge-capture
description: Ingest an external source — YouTube video, article, book, PDF, talk, or thread — into the ai-os knowledge base. Distills the source into a provenance-tagged note under knowledge/sources/, then promotes the genuinely durable learnings into the curated knowledge/ folders with [[cross-links]]. Use when the user says "add this to our knowledge/second brain", "capture/ingest this video/article", "go through this and put it in ours", or shares a link/file they want remembered.
---

# Knowledge Capture ("Second Brain" Ingestion)

## Purpose
Turn outside material into curated, cross-linked knowledge. The deliverable is a distilled
source note plus zero-or-more durable learnings promoted into the brain — not a verbatim dump.

## The provenance boundary (read first)
- `knowledge/sources/` = **captured external material**, *as stated by its author*. Attributed,
  lower-trust, the inbox.
- `knowledge/{decisions,patterns,lessons,playbooks,references}/` = **our curated brain** — what we
  will actually reuse, written in our own voice.
- This skill is the **one-way pipe** from `sources/` → curated folders. Keep others' claims in
  `sources/`; only promote what survives our judgment.
- The human owns what lands in the curated folders. Propose promotions; don't silently flood them.

## Activation Criteria
Trigger when ingesting/capturing an external source into the knowledge base, or when the user
shares a link/file with intent to "remember", "add to our knowledge", or "put in ours". Not for
the user's own in-flight learnings discovered while coding (those go straight to the right
`knowledge/` folder), and not for token-frugality concerns (that's `context-and-memory-management`).

## Inputs
- A source: URL (video/article/thread), local file path, or pasted text.
- Optional: which topic/folder the user expects it to inform.
- `knowledge/README.md` for folder conventions; `templates/adr.md` when promoting a decision.

## Outputs
- One note in `knowledge/sources/<slug>.md` (template below).
- Zero-or-more cross-linked promotions into curated `knowledge/` folders.
- A one-line summary: what was captured, what was promoted, what (if anything) conflicts.

## Workflow
1. **Capture.** Get the content. URLs → WebFetch; if a transcript is blocked (e.g. YouTube serves
   only page chrome), fall back to WebSearch for corroborating summaries and **mark the note
   second-hand**. Local files → Read. Never fabricate verbatim quotes from content you couldn't
   retrieve. If a source note for this material already exists, update it instead of duplicating.
2. **Distill.** Write `knowledge/sources/<slug>.md` using the template. Concise. Capture the
   author's claims and structure, not our opinion of them yet.
3. **Extract.** Identify the genuinely durable, reusable learnings — skip the ephemeral, the
   promotional, and the obvious. If nothing is durable, stop here: the source note is the deliverable.
4. **File & cross-link.** Promote each learning into the correct existing folder, following that
   folder's conventions/templates. Each promoted note `[[links]]` back to the source note; the
   source note's "Extracted into the brain" section links forward. Propose, don't force.
5. **Synthesize (optional).** Connect against existing knowledge — where it confirms, contradicts,
   or combines with what's already there. Record contradictions in the source note's
   "Open questions / contradictions" section; supersede curated notes deliberately, never silently.

## Source note template
```markdown
---
title: <source title>
source-url: <url or "local: path">
author: <creator / channel / author>
medium: video | article | book | pdf | talk | thread
captured: YYYY-MM-DD
tags: [<topic>, <topic>]
---

# <title>

**One-line gist.**

## Key points
- <distilled point>
- <distilled point>

## Extracted into the brain
- [[<curated-note-slug>]] — what was promoted and where

## Open questions / contradictions
- <anything that conflicts with or extends existing knowledge>
```

## Checklist
- [ ] Source note created/updated in `knowledge/sources/` with full frontmatter.
- [ ] Second-hand sources (no verbatim transcript) explicitly marked; no fabricated quotes.
- [ ] Durable learnings extracted (or "nothing durable" stated explicitly).
- [ ] Each promotion `[[cross-links]]` to and from the source note.
- [ ] Conflicts with existing knowledge recorded, not silently overwritten.

## Deliverables
- `knowledge/sources/<slug>.md`, any promoted curated notes, and the one-line capture summary.

Pairs with `context-and-memory-management` (keep distillation lean) and the existing
`knowledge/` taxonomy described in `knowledge/README.md`.
