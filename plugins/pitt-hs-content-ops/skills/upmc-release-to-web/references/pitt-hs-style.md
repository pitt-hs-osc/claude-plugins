# Pitt Health Sciences Style — points the skill enforces

Shared, versioned rule set for the `upmc-release-to-web` skill — the maintainer
merges approved writer corrections here (see SKILL.md, "For the maintainer"); it is
not edited mid-run. Rules are drawn from the **University of Pittsburgh Writing Style
Manual, October 2025 Edition** (AP-aligned with Pitt overrides). Full PDF:
`PITT Strategy Resources/Pitt_Writing_Style_Manual.pdf`.

Auto-applied fixes are shown in the change list before they're applied; "flag for
writer" items are surfaced as suggestions only. The script's `RULES` block mirrors
the auto-applied lists below — change both together.

> **Validated** against the published article
> `medschool.pitt.edu/news/lower-dopamine-may-drive-teen-risk-taking-fades-age`
> (June 2026). The rules below reproduce the writer's actual mechanical edits.

---

## Auto-applied

### 1. Drop academic degree credentials after names  *(HS web practice)*
In body copy, Health Sciences news **removes** the degree credential after a name,
rather than keeping it: `Ashley Parr, Ph.D., research…` → `Ashley Parr, research…`;
`Daniel Petrie, Ph.D., Finnegan Calabro, Ph.D.…` → `Daniel Petrie, Finnegan
Calabro…`; `Duncan Clark, M.D., Ph.D.;` → `Duncan Clark;`. The script removes a
comma-led credential (or chain) for Ph.D., M.D., M.S., M.A., M.P.H., M.F.A.,
Pharm.D., D.O., Sc.D., Ed.D., D.N.P., M.S.N., M.B.A., J.D., B.S., B.A., R.N.,
Dr.P.H. (and the unambiguous ≥3-char periodless forms PhD, MPH, MFA, PharmD…).
> 2-letter periodless forms (MD, MA, MS, BA, BS, DO, RN, JD) are intentionally NOT
> matched, so a state code like `Bethesda, MD` is never eaten. The Style Manual's
> bare rule is "if a degree IS written, use no periods (PhD)"; HS news goes further
> and drops it in running text.

### 2. Pitt prefix/decade spellings
`non-invasive`→`noninvasive`, `co-author(s)`→`coauthor(s)` (the `non`/`co` prefixes
aren't hyphenated), and decade words to numerals: `mid-twenties`→`mid-20s`,
`early/late twenties`→`early/late 20s` (likewise thirties). (Manual: "Hyphens,
Compounds" #7; "Numbers".)

### 3. Dated language → specific date
`published today` → `published <Month Day>`, with the date parsed from the release's
dateline/embargo (e.g., `published June 11`). The Style Manual says use specific
dates, not vague references like "today." (Manual: "Dates, Years" #6.)

### 4. Dashes — no surrounding space  *(Pitt overrides AP here)*
Em (—) and en (–) dashes used between words get the spaces removed:
`pattern — increasing` → `pattern—increasing`. (Manual: "Dashes.")

### 5. One space after sentence punctuation
Collapse any run of 2+ spaces to a single space; one space after periods, colons,
semicolons. (Manual: "Spacing.")

### 6. Percent
`8 percent` → `8%` (figure + symbol, even under 10). (Manual: "Percent" / "Numbers" #4.)

### 7. Hyphenation safety-net (compound modifiers)
Restore hyphens dropped in transit: longheld→long-held, risktaking→risk-taking,
longterm→long-term, shortterm→short-term, decisionmaking→decision-making,
wellknown→well-known, reallife→real-life. (Usually a no-op on AP-copyedited
releases; catches raw ones.)

---

## Flag for writer (suggest, don't auto-change)

- **Headline.** Wire headlines run long and title-cased; Pitt favors **active
  voice** (Top Tips #14). The published page even reworded the topic
  ("Risk-Taking" → "Substance Use"). Offer 2–3 web options; let the writer pick.
- **Byline / author.** The web article may carry a byline; the release doesn't. Ask.
- **HS media contact.** The published page replaces the UPMC press contacts (which
  this skill strips) with a Pitt HS line: `Media contact: HSNews@pitt.edu`. Offer
  to append it.
- **Hero image + caption.** The web article leads with a headshot/graphic and a
  `Caption:` line (e.g., "Ashley Parr and Beatriz Luna"). Writer adds in the CMS.
- **Title caps before a name.** A professional title *immediately before* a name is
  capitalized ("Pitt **Professor of Psychiatry** Beatriz Luna"); the same title
  *after* the name stays lowercase. Position-dependent — flag, don't auto-change.
- **Affiliation detail.** The page added ", School of Medicine," to Parr's title.
  Flag for the writer to confirm unit attribution.
- **Lede.** After the dateline is removed, confirm the opening sentence still reads.
- **Numbers.** Spell out one–nine, figures 10+; numerals always for age, money,
  measurements, times, pages. Flag deviations.
- **Jargon.** Pitt asks for plain English for external audiences (Top Tips #13).
  Flag dense clinical jargon for a plain-language gloss.
- **Months/dates.** Spell out March–July always; abbreviate Jan., Feb., Aug.,
  Sept., Oct., Nov., Dec. only with a specific date.
- **Institution name.** Only "University of Pittsburgh," "Pitt," or "the University."
- **Advisor** (academic), **orthopaedic** (SOM dept spelling), **African American**
  (never hyphenated), **Black** (capitalized) — flag if the copy differs.
