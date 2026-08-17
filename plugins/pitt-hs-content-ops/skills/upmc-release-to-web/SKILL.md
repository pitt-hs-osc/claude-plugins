---
name: upmc-release-to-web
description: >-
  Convert a UPMC Media news release (.docx) into a Pitt Health Sciences web
  article. Strips press-release scaffolding (media contacts, embargo line,
  dateline, "Summary:" label, ### marker, "About the University of Pittsburgh"
  boilerplate, the UPMC media footer, and the "Additional Resources" block),
  unlinks UPMC marketing links while keeping scholarly Pitt/DOI/NCANDA links,
  and applies Health Sciences / AP style fixes. ALWAYS lists every proposed
  change for the writer to approve BEFORE editing, and ALWAYS writes the result
  to a dated COPY — the original UPMC file is never modified. Trigger when a
  writer drops a UPMC press release / news release .docx and wants the
  web-ready version, mentions "UPMC release," "press release to web,"
  "strip the press release," or "post this release to the site."
---

# UPMC Release → Pitt HS Web Article

This skill turns a raw UPMC Media press release into the version that goes on the
Pitt Health Sciences website. It is **approval-gated** and **non-destructive**:
the writer signs off on a change list first, and the edited document is always a
new copy.

## Two memory files (read them every run)

- `references/upmc-to-pitt-rules.md` — what to strip, which links to keep vs.
  unlink. The strip/link logic the script enforces.
- `references/pitt-hs-style.md` — hyphenation and dated-language fixes, plus the
  "flag for the writer" items (headline, byline).

These two files plus the `RULES` block in `scripts/transform.py` are the **shared,
versioned source of truth** for the whole team. Do **not** hand-edit them during a
run: your installed copy is read-only, and a local edit would silently drift your
copy away from everyone else's. Instead, when a writer corrects the output,
**capture the correction as a proposal** (Step 7) and let the maintainer merge it.
That way one vetted rule set improves for everyone at once, instead of each person
accumulating their own private tweaks.

## Workflow

**1. Locate the file.** Confirm the path to the UPMC release `.docx`. Do not
proceed against anything but a `.docx`.

**2. Detect — list changes, change nothing.** Run:

```
python3 scripts/transform.py detect "<path-to-release.docx>"
```

This prints a categorized change list and writes `<release>.plan.json`. Show the
writer the full list, grouped by category:

- `STRIP_*` — press-release scaffolding to remove
- `DATELINE` — dateline prefix to drop from the lede
- `UNLINK_UPMC` — UPMC marketing links to unlink (text stays)
- `STYLE_DEGREE` — drop academic degree credentials after names (HS web style:
  "Ashley Parr, Ph.D., research…" → "Ashley Parr, research…")
- `STYLE_SPELLING` — Pitt prefix/decade spellings (non-invasive→noninvasive,
  co-authors→coauthors, mid-twenties→mid-20s)
- `STYLE_DASH` — remove spaces around em/en dashes (Pitt style)
- `STYLE_SPACING` — collapse double spaces (Pitt style)
- `STYLE_PERCENT` — "N percent" → "N%" (Pitt style)
- `STYLE_DATED` — "published today" → "published <Month Day>" (date from the release)
- `STYLE_HYPHEN` — hyphenation safety-net for raw, un-styled releases
- `FLAG_*` — judgment calls (funding, co-authors). **Never auto-applied.** Read
  these out and ask the writer whether to keep, strip, or edit each.

Also raise the **flag-for-writer** items from `pitt-hs-style.md` that the script
can't decide: propose 2–3 web headline options and ask for the **byline** to add.

**3. Get approval.** Ask the writer which categories to apply. Accept "all the
strips and links but leave style," etc. Translate their answer into the
`--approve` list. Do not apply any `FLAG_*` category unless the writer explicitly
says so. **If the writer approves nothing, stop.**

**4. Apply — to a copy.** Run with the approved categories:

```
python3 scripts/transform.py apply "<path-to-release.docx>" \
    --plan "<release>.plan.json" \
    --approve STRIP_CONTACT,STRIP_EMBARGO,STRIP_SUMMARY,STRIP_HASHES,STRIP_MEDIA_FOOTER,STRIP_ABOUT,STRIP_ADDL_RES,DATELINE,UNLINK_UPMC,STYLE_DEGREE,STYLE_SPELLING,STYLE_DASH,STYLE_SPACING,STYLE_DATED \
    --slug "<short-slug>"
```

(Use `--approve ALL` only if the writer approved every non-FLAG category.) The
script writes `YYYY-MM-DD-<slug>-web.docx` next to the source and leaves the
original untouched. Derive `<slug>` from the headline; keep it short and
hyphenated.

**5. Web framing the source lacks.** After the copy is written, settle the items
the release can't supply (open the copy and edit, or hand back to the writer):
the **headline** (the published page even reworded the topic), any **byline**, the
**Pitt HS media contact** (`Media contact: HSNews@pitt.edu`, replacing the stripped
UPMC contacts), and the **hero image + caption** (added in the CMS). Confirm the
lede still reads cleanly now that the dateline is gone.

**6. Confirm.** Tell the writer: what was applied, the path to the new copy, and
that the original is unchanged. Offer to re-run if they want different categories.

**7. Capture corrections so the skill improves.** If the writer changes anything
the skill produced — a scaffolding block it missed, a link it unlinked that should
have stayed (or the reverse), a style fix it made wrongly, or one it should have
made but didn't — record each correction as a rule proposal. This is the mechanism
that lets team edits feed back into the rules *without* every installed copy drifting
apart. Run one `propose` per correction:

```
python3 scripts/transform.py propose \
    --category STYLE_SPELLING \
    --before "healthcare" --after "health care" \
    --example "access to healthcare providers -> access to health care providers" \
    --submitter "<writer name>" --source "<release.docx>" \
    --note "why this is the right call"
```

Use the `--category` that matches — the same identifiers from the change list
(`STRIP_*`, `DATELINE`, `UNLINK_UPMC`, `STYLE_*`). If nothing fits, invent a short
`UPPER_SNAKE` name and explain it in `--note`. Proposals append to two files next to
the release: `upmc-rule-proposals.md` (human-readable) and `upmc-rule-proposals.jsonl`
(for merging). Then tell the writer where that file is and that **sending it to the
skill maintainer is what gets the fix into everyone's next version**. Do not edit the
rules files yourself — the maintainer merges proposals (see below).

## Guardrails

- Never edit the original file. Only ever the dated `-web.docx` copy.
- Never apply a change the writer didn't approve. The `detect` → approve → `apply`
  order is mandatory.
- `FLAG_*` items are suggestions only.
- If a UPMC link isn't clearly marketing, default to unlink and flag it.

## For the maintainer: merging proposals

Proposals are suggestions, not automatic rules — the maintainer decides what becomes
team canon. This gate is deliberate: it keeps one consistent, vetted rule set instead
of letting one writer's edge case quietly become everyone's rule. Periodically gather
the `upmc-rule-proposals.*` files writers send in, and for each proposal you approve:

1. Add or amend the matching rule in `references/upmc-to-pitt-rules.md` or
   `references/pitt-hs-style.md`. A recurring one-off substitution goes under section
   D, "Recurring fixes carried in memory," of the rules file.
2. Mirror any pattern change in the `RULES` block of `scripts/transform.py`. The
   reference files are the human explanation; the script is what actually runs — they
   must agree, or the change list will describe something the script doesn't do.
3. Add an entry to `CHANGELOG.md` (what changed, whose correction it came from), bump
   the version, and publish the update to the marketplace so the team pulls it.

Skip or edit proposals that are one-offs, wrong, or too narrow. A shared rule set is
only worth having if it stays consistent.

## Requirements

`python-docx` (`pip install python-docx --break-system-packages`).
