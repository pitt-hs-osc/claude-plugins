# UPMC → Pitt HS Web Transformation Rules

This is the shared, versioned rule set for the `upmc-release-to-web` skill — one
copy the whole team runs against. It is not edited during a run: when a writer
corrects a transformation, the skill captures a proposal (see SKILL.md, Step 7 and
"For the maintainer") and the maintainer merges approved proposals here. Each rule
has an ID so the change list can reference it.

The transform script (`scripts/transform.py`) reads the machine-readable copy of
these rules from the top of the script. If you change a pattern here, mirror it in
the script's `RULES` block (the script is the source of truth at runtime; this file
is the human-readable explanation).

---

## A. Press-release scaffolding to STRIP (remove the whole paragraph)

These are wire-service conventions that never appear on the Pitt HS web article.

| ID | What to remove | How it's detected |
| :-- | :-- | :-- |
| STRIP-CONTACT | Media contact blocks — "Contact: …", "Mobile: …", "E-mail: …" | Line starts with `Contact:`, `Mobile:`, `E-mail:`/`Email:` |
| STRIP-EMBARGO | Embargo line — "EMBARGOED FOR RELEASE UNTIL …" | Line contains `EMBARGOED` |
| STRIP-SUMMARY | The "Summary:" label paragraph | Line starts with `Summary:` |
| STRIP-HASHES | End-of-release marker `# # #` (or `###`, `-30-`) | Line is only `#`, spaces, or `-30-` |
| STRIP-ABOUT | "About the University of Pittsburgh School of Medicine" boilerplate + the 2 paragraphs that follow it | Heading line starts with `About the University of Pittsburgh` → remove it and following body paras until the next blank/section |
| STRIP-MEDIA-FOOTER | "www.upmc.com/media" footer line | Line is `www.upmc.com/media` (with or without `http`) |
| STRIP-ADDL-RES | "Additional Resources:" label and its list of links | From `Additional Resources:` through the end of that list block |

**Judgment calls (flag for writer, don't auto-strip):**
- Funding/grant paragraph ("This research was supported by…") — Pitt HS usually KEEPS this. Flag only.
- Co-authors paragraph ("Pitt co-authors of this research are…") — usually KEEPS. Flag only.

---

## B. Hyperlink rules

Classify every hyperlink by its destination URL.

**KEEP (scholarly / Pitt — leave link and text intact):**
- `doi.org` / `nature.com` and other journal/DOI links (the published study)
- `*.pitt.edu` (e.g., `psychiatry.pitt.edu`, `medschool.pitt.edu`)
- `ncanda.org` and other named research-consortium sites

**UNLINK (UPMC marketing — keep the words, remove the hyperlink):**
- `upmc.com/services/*`
- `upmc.com/conditions/*`
- `upmc.com/locations/*`
- `upmc.com/Pages/*`, `upmc.com` home

**REMOVE WITH PARAGRAPH (UPMC cross-promotion — usually inside a stripped block):**
- `upmc.com/media/news/*` (other press releases)
- Anything inside the "Additional Resources" block (handled by STRIP-ADDL-RES)

When in doubt about a UPMC link, default to UNLINK and flag it.

---

## C. Dateline

| ID | Action |
| :-- | :-- |
| DATELINE | Remove the dateline prefix at the start of the lede, e.g. `PITTSBURGH, June 11, 2026 – `. Keep the sentence that follows. Pattern: `^[A-Z][A-Za-z. ]+, [A-Z][a-z]+ \d{1,2}, \d{4}\s*[–-]\s*` |

---

## D. Recurring fixes carried in memory

Add site-specific recurring substitutions here as writers discover them
(e.g., preferred spelling of a center name, a link that should always be swapped).
The skill applies these every run.

- (none yet — add as discovered)
