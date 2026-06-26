# Knowledge

This is where real, hard-won learnings accumulate over time. Unlike `standards/` (timeless rules) these are specific, dated, and written by me as I work. AI tools should consult here before re-deriving, and propose additions when something durable is learned — but the human owns what lands here.

## Folders
- **decisions/** — Architecture Decision Records (ADRs). Why we chose X over Y, with context and consequences. Use `templates/adr.md`.
- **patterns/** — Reusable solutions that worked: idioms, designs, and conventions proven in this context.
- **lessons/** — What we learned the hard way, often from incidents/postmortems. The "don't do this again" file.
- **playbooks/** — Step-by-step runbooks for recurring operational tasks (deploys, migrations, incident response).
- **references/** — Pointers to external tools, repos, and resources worth remembering (not executable workflows). Note what it is, why it's relevant, and how to action it.
- **sources/** — Captured external material (videos, articles, books, PDFs), distilled *as stated by the author*. The provenance boundary: `sources/` holds others' ideas at lower trust; the other folders hold our curated brain. The `knowledge-capture` skill is the one-way pipe from `sources/` into the curated folders.

## Conventions
- One learning per file; short, dated, kebab-case filename.
- Cross-link related entries with `[[name]]`.
- Prune or supersede when something becomes false — stale knowledge is worse than none.
