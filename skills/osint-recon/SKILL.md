---
name: osint-recon
description: Run a structured, defensive OSINT (open-source intelligence) sweep on a person, org, username, email, or domain — map the public digital footprint using only publicly available data. Use for authorized footprint/exposure assessments, attack-surface recon before a threat model, due-diligence, or "what can someone find about us/this account online". Triggers: "osint", "footprint", "what's exposed about", "recon this domain/username/email", "digital exposure check".
---

# OSINT Recon

## Purpose
Discover what an adversary could learn about a target from public sources, so the exposure can be
reduced. This is **reconnaissance for defense** — the deliverable is an exposure report, not an
intrusion.

## Authorization & Ethics (read first)
- **Authorized scope only.** Run against your own org/accounts, or a target you have written
  permission to assess (engagement scope, bug-bounty rules, consent). State the authorization in
  the report header.
- **Public data only.** No login bypass, no credential stuffing, no breach-data purchase, no
  social engineering, no accessing non-public systems. If a step needs a password you don't own,
  stop.
- **Minimize + report, don't hoard.** Collect only what's needed to show exposure; do not retain
  sensitive PII beyond the assessment. Purpose is to *close* exposure, not exploit it.
- If a request shifts from "what's exposed" to "track/locate a specific private individual without
  their consent," refuse and say why.

## Activation Criteria
Trigger when: assessing your own/an authorized target's public footprint; gathering external
attack-surface before `threat-modeling`; vendor/acquisition due-diligence; verifying a takedown
worked. Not for surveillance of private individuals, doxxing, or anything outside an authorized
scope.

## Inputs
- One or more seeds: full name, username, email, phone, domain, company, profile URL, or image.
- Authorization basis (engagement, ownership, consent) — required.
- `standards/security.md` for how findings feed remediation.

## Outputs
- Exposure report: what's publicly discoverable, where, severity, and how to reduce it.

## Workflow
1. **Define scope & authorization.** Record target, seeds, what's in/out of scope, and the
   authorization basis. Pick the pivots you'll allow (e.g. username → accounts, email → breach
   *exposure* only).
2. **Seed expansion.** From each seed, branch to linked identities — keep a pivot graph (seed →
   discovered handle → linked profile). Note confidence per edge; don't assert a link you can't
   corroborate twice.
3. **Username sweep.** Check handle reuse across platforms (tools like *Sherlock*, *Maigret*).
   Record only existence + public profile data.
4. **Email / account discovery.** Map which services an email is registered against and whether it
   appears in *public* breach indexes (tools like *Holehe*, *Epieos* / Hunter-style lookups).
   Report exposure; never use leaked credentials.
5. **Domain / infra footprint.** Public DNS, subdomains, WHOIS, certificate transparency, exposed
   metadata in docs/images (EXIF). For automation, *SpiderFoot* orchestrates many sources at once.
6. **Geolocation / media (only if in scope).** Public geotags, background landmarks via
   *OpenStreetMap* / *Overpass Turbo*. Used to demonstrate location-leak risk, not to surveil.
7. **Corroborate.** Every claimed link needs ≥2 independent public sources or it's marked
   "unverified". Kill false positives (common names, recycled handles).
8. **Assess & remediate.** Rate each finding by sensitivity × ease-of-discovery; for each, give a
   concrete reduction step (lock down profile, scrub EXIF, rotate exposed email, takedown request).

## Tool reference (all public-data, open-source)
- **Sherlock / Maigret** — username presence across sites.
- **Holehe / Epieos** — email → registered services & public breach exposure.
- **SpiderFoot** — automation engine that fans out across hundreds of OSINT sources.
- **Overpass Turbo / OpenStreetMap** — geospatial lookups for media geolocation.
- **IntelTechniques** — workflow checklists & search tooling.
- Document the trail (a Hunchly-style capture log) so findings are reproducible and auditable.

## Checklist
- [ ] Authorization basis stated in the report header.
- [ ] Only public sources used; no credentials/breach-data used to authenticate anywhere.
- [ ] Every identity link corroborated (≥2 sources) or flagged unverified.
- [ ] Each finding has a severity and a concrete remediation step.
- [ ] Sensitive PII minimized; not retained beyond the assessment.

## Deliverables
- Markdown report: `## Scope & authorization`, `## Pivot graph (seeds → discovered)`,
  `## Findings (source, evidence, confidence, severity)`, `## Exposure remediation`,
  `## Residual exposure`.

Pairs with `threat-modeling` (external attack-surface input) and the `security-architect` agent.
