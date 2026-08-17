# Changelog — upmc-release-to-web

The rule set and skill behavior are versioned so the team can see what changed and
pull updates. When you merge a writer proposal (see SKILL.md, "For the maintainer"),
add an entry here, bump the version, and publish to the marketplace.

## 1.1.0 — 2026-08-14
- Added the `propose` command. Writer corrections are captured as portable rule
  proposals (`upmc-rule-proposals.md` + a `.jsonl` mirror) for the maintainer to
  review and merge, rather than editing installed rule files during a run — so a
  distributed, read-only copy can still feed improvements back to the shared rules.
- SKILL.md: new **Step 7** (capture corrections) and a **"For the maintainer:
  merging proposals"** section. Reference-file headers reworded from "editable
  memory" to the shared, versioned, maintainer-merged model.

## 1.0.0 — 2026-06 (baseline)
- Detect → approve → apply transform of a UPMC Media release into a Pitt HS web
  article: strips press-release scaffolding, unlinks UPMC marketing links (keeps
  scholarly/DOI/Pitt links), applies HS/AP style fixes.
- Non-destructive (writes a dated `-web.docx` copy) and approval-gated.
- Rules validated against the published article
  `medschool.pitt.edu/news/lower-dopamine-may-drive-teen-risk-taking-fades-age`.
