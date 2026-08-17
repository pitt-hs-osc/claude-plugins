# Setting up the Pitt HS Claude tools

A quick, one-time setup. No GitHub, no accounts, no commands — just a few clicks in
the Claude desktop app. Takes about two minutes.

## What this gives you

A tool inside Claude that turns a UPMC news release into a Pitt Health Sciences web
article — stripping the press-release parts, fixing the style, and always saving a
clean copy (your original is never changed).

## Step 1 — Open the plugins menu

In the Claude desktop app, open the **Customize** menu and choose **Plugins**.

## Step 2 — Add the Pitt HS library (first time only)

Choose **Browse plugins**. If you don't see the Pitt HS library yet, add it by its
address:

```
pitt-hs-osc/claude-plugins
```

(Copy that in exactly. You won't be asked to sign in — it's open to the team.)

## Step 3 — Install the tool

Find **pitt-hs-content-ops** in the list and click **Install**. That's it — it's now
part of your Claude.

## Step 4 — Turn on automatic updates (recommended)

Still in **Customize → Plugins**, find the Pitt HS library and switch on
**auto-update**. This way, whenever the tool is improved, you get the new version
automatically — you never have to reinstall.

## How to use it

Start a Claude conversation, attach or drop in a UPMC release (a Word `.docx` file),
and ask for the web version — for example:

> "Here's a UPMC release — give me the web-ready version for the Pitt HS site."

Claude will **show you every change it plans to make and wait for your OK** before
editing, then save a clean, dated copy. Your original file is left untouched.

## If it gets something wrong

Just tell Claude what should have been different (for example, "you removed a link
that should have stayed"). It will note the correction in a small file and tell you
where it is. **Send that file to Nick** — he folds good corrections into the tool so
it improves for everyone. You don't fix anything yourself.

## Need help?

Ask **Nick** (nick@nicholasburcin.com). If a step looks different from what's written
here, the app may have moved a menu — Nick can point you to it.
