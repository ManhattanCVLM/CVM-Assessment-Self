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

## Turning on GitHub Pages

1. **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: **`/ (root)`** → **Save**

Pages must be switched on per repository; it is off by default on a new one.

---

## Releasing a change

1. Replace `index.html`
2. **Bump `const CACHE` in `sw.js`** — currently `cvm-self-v9`
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
