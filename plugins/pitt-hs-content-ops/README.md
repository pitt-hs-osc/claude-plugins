# pitt-hs-content-ops

Content-operations toolkit for the Pitt Health Sciences digital team.

## What's inside

### Skill: `upmc-release-to-web`
Converts a UPMC Media news release (`.docx`) into a Pitt HS web article. It is:

- **Approval-gated** — lists every proposed change grouped by category and waits for
  the writer to approve before touching anything.
- **Non-destructive** — always writes a dated `-web.docx` copy; the original UPMC
  file is never modified.
- **Self-improving (team-safe)** — when a writer corrects the output, the skill
  records the correction as a *rule proposal* rather than editing its own files.
  The maintainer reviews proposals and merges the good ones into the shared rules,
  bumps the version, and republishes — so every teammate improves at once instead
  of each copy drifting apart.

It strips press-release scaffolding (media contacts, embargo line, dateline,
"Summary:" label, `###` marker, "About the University of Pittsburgh" boilerplate,
the UPMC media footer, "Additional Resources"), unlinks UPMC marketing links while
keeping scholarly Pitt/DOI/NCANDA links, and applies Health Sciences / AP style
fixes from the Pitt Writing Style Manual.

The rules live in `skills/upmc-release-to-web/references/` (human-readable) and the
`RULES` block of `skills/upmc-release-to-web/scripts/transform.py` (what runs).
See `skills/upmc-release-to-web/CHANGELOG.md` for version history.

## How corrections flow back into the rules

1. A writer corrects Claude's output during a run.
2. The skill runs `transform.py propose …`, appending the correction to
   `upmc-rule-proposals.md` (+ a `.jsonl` mirror) next to the release.
3. The writer sends that file to the maintainer.
4. The maintainer merges approved proposals into the reference files + the script's
   `RULES` block, adds a `CHANGELOG.md` entry, bumps `version` in
   `.claude-plugin/plugin.json`, and republishes.
5. Teammates run `/plugin update pitt-hs-content-ops@pitt-hs` to pull it.

## Requirements

`python-docx` — `pip install python-docx --break-system-packages`.
