# claude-plugins

The Pitt Health Sciences digital team's Claude plugin library. Add it once in Claude;
new tools and improvements show up automatically.

Currently ships one plugin:

- **pitt-hs-content-ops** — Pitt HS content operations, including the
  `upmc-release-to-web` skill (UPMC release → Pitt HS web article).

> **Non-technical teammate?** You don't need any of this README. Follow
> `docs/TEAM-SETUP.md` (or the setup guide Nick shared) — it's click-by-click.

Assumed names below: GitHub org **`pitt-hs-osc`**, repo **`claude-plugins`**. If you
pick different names, swap them everywhere they appear.

---

## Publish it (maintainer, one time)

Host this as a **public** repo. Public matters here: anyone can add a public
marketplace with **no GitHub account and no login**, which is the whole point for a
non-technical team. The contents are just editorial style rules and a transform
script — nothing sensitive — so public is appropriate.

Create the org first (github.com/organizations/new → handle `pitt-hs-osc`, display
name "University of Pittsburgh Health Sciences Office of Strategic Communications"),
then:

```bash
cd claude-plugins
git init
git add .
git commit -m "claude-plugins: pitt-hs-content-ops v1.1.0"
git branch -M main
git remote add origin https://github.com/pitt-hs-osc/claude-plugins.git
git push -u origin main
```

Make sure the repo is **Public** (GitHub → repo Settings → General → Danger Zone →
Change visibility, or pick Public when creating it).

> Before pushing, optionally set the `owner`/`author` email in
> `.claude-plugin/marketplace.json` and
> `plugins/pitt-hs-content-ops/.claude-plugin/plugin.json` to the address the team
> should treat as maintainer.

## Teammates: install it (the easy, no-GitHub way)

In the Claude desktop app: **Customize → Plugins → Browse plugins**, add the library
by its address `pitt-hs-osc/claude-plugins` if it isn't already listed, then pick
**pitt-hs-content-ops** and click **Install**. No GitHub account, no commands.

Then turn on auto-update once — **Customize → Plugins → (the marketplace) → Enable
auto-update** — so future improvements arrive on their own.

<details>
<summary>Command-line equivalent (for anyone who prefers it)</summary>

```
/plugin marketplace add pitt-hs-osc/claude-plugins
/plugin install pitt-hs-content-ops@pitt-hs
```
</details>

## Staying up to date

With auto-update enabled (above), Claude checks this repo in the background after a
session starts and loads any new version next session (or after `/reload-plugins`).
New *plugins* added to the library appear under **Customize → Plugins → Browse**.

If a teammate left auto-update off, they can pull the latest manually with
`/plugin marketplace update` then `/plugin update pitt-hs-content-ops@pitt-hs`.

Updates are triggered by the `version` field in
`plugins/pitt-hs-content-ops/.claude-plugin/plugin.json`, so **every release must bump
it** (and note it in `CHANGELOG.md`). Because of a current quirk, a version bump is
only picked up after the marketplace catalog refreshes — which auto-update does
automatically — so when you ship an important fix, a one-line "new version, restart
your session" to the team is the reliable nudge.

---

## The improvement loop

The library gets better over time *for the whole team at once*:

1. A writer corrects the skill's output. The skill captures the correction as a
   proposal file (it does **not** edit its own rules — installed copies are read-only
   and would otherwise drift apart).
2. The writer sends the proposal file to the maintainer (Nick).
3. The maintainer merges the approved proposals into the plugin's rules, adds a
   `CHANGELOG.md` entry, **bumps the version** in `plugin.json`, commits, and pushes.
4. Teammates get it automatically (auto-update) or with the two update commands.

Adding more skills later is just a new subdirectory under `plugins/` and a new entry
in `marketplace.json` — teammates get them through the same library they already added.

## Continuous validation

`.github/workflows/validate.yml` runs on every push and pull request. It lints both
manifests and exercises the transform engine end to end (`tests/smoke_test.py`), so a
broken rule edit fails the check *before* the team pulls it. Run it locally anytime
with `python tests/smoke_test.py` (needs `python-docx`).

## Repo layout

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json                 # lists the plugins in this library
├── .github/workflows/validate.yml       # CI: lint manifests + smoke-test the engine
├── tests/smoke_test.py                  # the CI smoke test (also runnable locally)
├── docs/TEAM-SETUP.md                   # click-by-click guide for non-technical staff
├── plugins/
│   └── pitt-hs-content-ops/
│       ├── .claude-plugin/plugin.json   # version lives here — bump on each release
│       ├── README.md
│       └── skills/
│           └── upmc-release-to-web/
│               ├── SKILL.md
│               ├── CHANGELOG.md
│               ├── references/
│               └── scripts/transform.py
└── README.md                            # this file
```
