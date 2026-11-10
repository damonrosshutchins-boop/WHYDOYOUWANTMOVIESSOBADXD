# GitHub Pages deploy

Files (keep them together in the same folder, at the repo root):

- `index.html`  – the loader page (same code as `index.svg`, converted so Pages serves it as the default document)
- `updater.js`  – the service worker; must live next to `index.html`
- `index.svg`   – original wrapper, unchanged (optional; `index.html` replaces it)
- `.nojekyll`   – tells Pages to skip Jekyll processing

## Steps
1. Create a repo and upload all four files to the root of the default branch.
2. Repo **Settings → Pages → Build and deployment → Deploy from a branch** → pick `main` and `/ (root)` → Save.
3. Open `https://<username>.github.io/<repo>/` after the build finishes (about a minute).
4. First visit installs the service worker, downloads the site, then reloads itself once. Later visits load from cache.

## Troubleshooting
- Stuck on the spinner or odd state: open the page with `?reset` on the end to clear the worker and cache, then reload.
- `?0` on the end skips the service worker and loads the remote copy in an iframe instead.
- Pages is HTTPS-only, which service workers require. Opening `index.html` from disk (file://) will not register the worker.
- Project sites live under `/<repo>/`; the worker's scope is taken from where it is served, so no path edits are needed.
