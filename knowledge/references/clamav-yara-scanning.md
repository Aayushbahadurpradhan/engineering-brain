# Reference: ClamAV + YARA for Open-Source Malware Scanning

Source: a Facebook reel (David Bombal, sponsored by Cisco) on **ClamAV** — a free, open-source
antivirus engine — and its **YARA** rule integration for threat hunting and malware defense.

## What it is
- **ClamAV** — open-source AV engine. Signature-based scanning of files/streams; ships `clamscan`
  (CLI) and `clamd` (daemon) + `freshclam` for signature updates. Cross-platform.
- **YARA** — a pattern-matching rule language for identifying/classifying malware by textual or
  binary patterns. ClamAV can load YARA rules, so custom detections sit alongside signatures.

## Where it's relevant to ai-os (and where it isn't)
`ai-os` is an engineering brain, not a security product — so this is a **reference pointer, not a
skill**. It's useful when a task genuinely involves:
- Scanning user-uploaded files / untrusted artifacts in a pipeline (e.g. a SaaS that accepts uploads).
- A CI step that scans build artifacts or container images for known-bad content.
- Pairing with the `threat-modeling` skill / `security-architect` agent when "malware in
  uploads/artifacts" is part of the attack surface.

## Practical notes (if/when used)
- Run `clamd` as a daemon and scan via socket for throughput; one-shot `clamscan` is fine for CI.
- Keep signatures fresh with `freshclam` on a schedule — stale defs = blind spots.
- Add custom YARA rules for org-specific or recently-seen threats not yet in public signatures.
- It's **detection, not prevention** — a layer, not a guarantee. Defence in depth still applies.

Cross-link: this pairs with `threat-modeling` and `standards/security.md` when upload/artifact
scanning enters scope.
