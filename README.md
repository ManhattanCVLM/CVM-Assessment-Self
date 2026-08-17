# CVM Self Assessment

The self assessment, on its own. 350 questions across 7 assessment areas, scored 1–8,
offline once installed, and nothing in it refers to the external assessment.

```
https://YOUR-USERNAME.github.io/CVM-Assessment-Self/
```

Hand that URL to your client's own people. It runs in any modern browser, on any device, and can be
installed to a home screen or desktop so it works with no signal and keeps its answers on
that device.

---

## Two things it does

**Answer the self assessment.** The default. There is no Self/External switch to leave
in the wrong position, so a submission cannot arrive filed against the wrong assessment —
the one mistake merging could not detect on its own. Finish, then
**Setup → Export my assessment (JSON)** and send the file back.

**Compare two self assessments.** *Setup → What this copy is doing → Comparing two
self assessments.* Import two finished ones — last year's against this year's — and
every chart, table and figure compares them, **labelled by their own titles**. Scoring
switches off, and the PDF report becomes available, because a comparison is a thing worth
sending to someone. A file from an external assessment is refused rather than loaded under
the wrong name.

---

## What is deliberately absent

The word "external" does not appear in this app. Not hidden — absent:

- no assessment-type switch, and no external option anywhere
- no cross-assessment gap filter or gap jump while scoring
- one score chip per subject, not a pair with a permanent dash
- one score column in the CSV, and no gap column
- one series on the dashboard, no alignment card, no divergence list

If a backup holding both assessments is restored here — the only way external scores can
reach this device — they stay in the file, never appear, and **are dropped from the
export**. Passing them on would have the consolidator merge answers into an assessment
this person was never asked to do, credited to them by name.

Comparison is the exception that proves it: two series, but both are self assessments,
named by their titles.

---

## Layout

```
index.html                the app
sw.js  manifest.webmanifest  icon-*.png      offline install
CVM Self Assessment.html  one-file copy, for email or a laptop
.nojekyll                 tells Pages to serve the files as-is
```

One self-contained HTML file — questions, charts, logo and all. No build step, no
dependencies, no server, no database.

---

## Installing it

It runs in **any modern browser** — Chrome, Edge, Safari, Firefox, on Windows, macOS,
Android, iPhone or iPad. Installing is optional; it gives the app its own icon, its own
window, and makes it work with no network.

| Where | How |
|---|---|
| **Windows / macOS**, Chrome or Edge | The **install icon** at the right-hand end of the address bar, or ⋮ → *Cast, save and share ▸ Install page as app* |
| **Android**, Chrome | ⋮ → **Install app** |
| **iPhone / iPad** | **Safari** → **Share** → **Add to Home Screen** |
| **Firefox** | No install button; it runs as an ordinary page, and still works offline |

The app puts an **Install this app** button in Setup when the browser offers one, so on
Chrome and Edge there is nothing to hunt for.

iPhone and iPad are the one place where the browser matters: **no iOS browser except
Safari can install a web app**. Chrome on iOS is Safari's engine with a different badge
and Apple does not expose the install to it. That restriction is Apple's, and applies
nowhere else.

---

## Who can see it

**A URL on its own shows nothing.** Without a licence key the app shows its logo, its name
and a key field — no questions, no dashboard, no tabs. The 350 questions are the product,
and "nobody knows the URL" is not a control.

**The link you send carries the key**, after the `#` so it never reaches the server or its
logs:

```
https://YOUR-USERNAME.github.io/REPO-NAME/#lic=CVM1.eyJj…
```

They open it and are straight in — nothing to paste. The key is stored on the device and
wiped from the address bar, so it is not left sitting in a screenshot or a shared tab.
A key pasted into the field by hand works exactly the same.

**Somebody whose key has lapsed is never locked out of their own work.** The gate is only
for a device with no licence *and* nothing on it. If there are answers here, they get the
read-only app instead, so they can always reach and export what they did.

This is why the repositories stay public and the URLs stay reachable: that is what lets
everyone get updates. The door is in the app, not in the hosting.

---

## Licensing

The client-facing apps — Self, External and the client app — carry a licence.
The consolidator does not; it is the operator's own tool.

**This app does nothing until it is licensed.** With no key it shows the questions but will
not record a score, and says so: *"This assessment needs a licence — contact Manhattan CVLM
to obtain a licence key."* That is deliberate for the self assessment: a copy that reaches
someone who was never given a key should not quietly work for a year.

**How it works.** You issue a signed key holding the client's name and an end date,
using `CVM Licence Keys (KEEP PRIVATE).html`, which never leaves your machine. They paste
it into **Setup → Licence**. The app verifies the signature against the public key built
into it, and works normally until the date passes.

**What happens at the end.** Scoring switches off. Everything already scored stays visible,
and export and the PDF report still work — nobody's completed assessment is held hostage
over a date. A new key pasted over the old one unlocks it again, with no rebuild and no
reinstall.

**With no key at all**, this app is locked from the first screen — there is no build-date
grace period, because there is nothing here anyone should be doing unlicensed. The External
and client apps take the softer route: they run until the build's own date (`BUILD_EXPIRES`
in `build_editions.py`, currently 31 August 2027) and then go read-only.

**What it does not do.** It cannot *enforce* anything, and no client-side app can. The code
is on their machine and the source is readable, so someone willing to edit the app can
remove the check. What the signing does is make a key impossible to forge or extend — the
private key exists only on your machine, and altering so much as the date inside a key
breaks its signature. The device clock cannot simply be wound back either: the latest date
the app has ever seen is stored, and time never runs backwards from it. Continuing past
expiry takes deliberate tampering, not forgetfulness.

If you ever need real enforcement, that means a server the app checks in with — which also
means it stops working offline, which is currently one of the better things about it.

---

## Turning on GitHub Pages

1. **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: **`/ (root)`** → **Save**

Pages must be switched on per repository; it is off by default on a new one.

---

## How an update reaches people

**The page is fetched from the network first**, with the cached copy as the fallback. So a
reload with any signal at all lands on the current version — one reload, not two — and the
app still opens instantly with no network.

That is a change from how it worked up to build 2.5, which served the cached copy every
time and fetched the new one quietly for next time. The first visit after an update showed
the old app, which reads exactly like the update having failed.

**A release made while somebody has the app open** shows them *"A new version is ready"*
with a Reload now button. Nothing is swapped underneath them mid-question, and their
answers survive either way.

**Installed copies check on every open**, and the worker script itself is exempt from the
browser's HTTP cache (`updateViaCache: "none"`), so a new release cannot sit unnoticed
behind a stale copy of `sw.js`.

**If the site is ever switched off** — Pages turned off, the repository made private on a
free plan, a deploy that fails — an installed copy keeps working from its cache. The worker
treats a 404 or a 500 as a failed fetch, not as the app, so a hosting error never replaces
a working install. New visitors get nothing, of course.

To release: replace `index.html`, **bump `const CACHE` in `sw.js`**, commit. Without the
bump, devices keep the assets they cached — the page will be current but its icons and
manifest will not.

If a device is somehow still stuck: in the browser, clear site data for the URL; on a
home-screen install, delete the icon and add it again. Answers live in the browser's
storage for that origin and survive the first; the second clears them, so export first.

---

## Releasing a change

1. Replace `index.html`
2. **Bump `const CACHE` in `sw.js`** — currently `cvm-self-v15`
3. Commit and push

Without step 2, a device that already installed this keeps serving its cached copy.
Answers already on a device survive an update.

---

## Where the data lives

No server side. Every score and note stays on the device that entered it and is never
transmitted, so publishing this publishes the blank tool, not anyone's results. Nothing is
preloaded — each assessment is a different client.

Deleting the installed app, or clearing site data in the browser, clears the answers. Export at the end of every session.

---

## The other repositories

| Repository | What it holds |
|---|---|
| **CVM-Assessment-Self** | The self assessment |
| **CVM-Assessment-Ext** | The external assessment |
| **CVM-Assessment** | The client app: self against external, and the comparison of two |
| **CVM-Consolidation** | Combining many assessors' submissions into one assessment |

All four sit on the same `github.io` origin but keep separate storage keys and separate
offline caches, so they can all be installed on one device without touching each other's
answers.

---

© Brooklyn Solutions AI / Manhattan CVLM. All rights reserved. Published here for
distribution to named clients; not licensed for reuse or redistribution.
