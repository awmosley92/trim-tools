# Digital Scribe — Trim Tools

Two offline finish-carpentry calculators, packaged as an installable web app. 100% vibecoded.

- `stool.html` — Sheet S-01, window stool & horn calculator
- `reveal.html` — Sheet S-02, reveal finder for reused trim
- `index.html` — landing page linking both

## Deploy to GitHub Pages

1. Create a public repo (e.g. `trim-tools`).
2. Upload **the contents of this folder** to the repo root — not the folder itself.
   Keep `icons/` as a subfolder. Include the hidden `.nojekyll` file; if the web
   uploader won't take it, create it with **Add file → Create new file**, name it
   `.nojekyll`, leave it empty, commit.
3. Settings → Pages → Build and deployment → Source: **Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. Wait about a minute. Live at `https://<username>.github.io/trim-tools/`.

## Install on the iPhone

Open that URL in **Safari** (Chrome can't install web apps on iOS).
Share → **Add to Home Screen**.

You get an icon that launches full screen with no browser chrome, works with no
signal, and keeps every value you typed.

## Persistence

Each tool saves its inputs to `localStorage` under its own key
(`digital-scribe.stool.v2`, `digital-scribe.reveal.v2`), on every change plus
again when the page is hidden. Switch apps, lock the phone, reboot — the numbers
are still there.

Storage for a home-screen web app is separate from Safari's and is **not** subject
to the 7-day eviction that applies to ordinary Safari browsing. It is cleared if
you delete the home-screen icon, or if you tap **Reset** inside a tool.

Caveat: the two tools do not share values, and there is no multi-window log —
one set of numbers per tool at a time.

## Updating

Edit the file, upload the new version, done — Pages redeploys on every push.

Phones that already installed it hold a cached copy. The service worker refreshes
in the background, so a second launch picks up changes. To force it immediately,
bump `VERSION` at the top of `sw.js`:

```js
const VERSION = 'ds-2026-11-18-a';   // change the date/letter
```

That invalidates the old cache on next load.

## Not in search results

`robots.txt` disallows crawlers and every page carries
`<meta name="robots" content="noindex, nofollow">`. That keeps the site out of
Google. It does **not** make it private — anyone with the URL can still open it.

## Files

```
.nojekyll                  stops Jekyll from processing the site
robots.txt                 keeps crawlers out
index.html                 landing page, registers the service worker
stool.html                 Sheet S-01
reveal.html                Sheet S-02
manifest.webmanifest       app name, icons, standalone display
sw.js                      offline cache
icons/icon-180.png         iOS home screen
icons/icon-192.png         manifest
icons/icon-512.png         manifest
icons/icon-512-maskable.png  Android adaptive
```

No build step, no dependencies, no network calls. Everything renders from the
files in this folder.
