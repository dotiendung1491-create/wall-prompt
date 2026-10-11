# Wall Reinforcement Prompt Generator – hosting guide

Static site (no backend). Hosted on **GitHub Pages**, deployed automatically by `.github/workflows/pages.yml` on every push to `main`.

| File | Purpose |
|---|---|
| `index.html` | The tool (your original + manifest link + service-worker registration) |
| `wall-prompt-generator.html` | Untouched original, standalone local backup |
| `manifest.webmanifest`, `sw.js`, `icons/` | Installable app + offline support |
| `.github/workflows/pages.yml` | Publishes the site on push |

## One-time setup (about 5 minutes)
1. Install Git: https://git-scm.com/download/win
2. Create a GitHub account if needed, then a new **public** repo, e.g. `wall-prompt` (no README/license).
3. In this folder, in PowerShell:
   ```
   git init -b main
   git add .
   git commit -m "Initial version"
   git remote add origin https://github.com/<your-user>/wall-prompt.git
   git push -u origin main
   ```
4. On GitHub: repo → **Settings → Pages → Build and deployment → Source: GitHub Actions**. Then repo → **Actions** → re-run "Deploy to GitHub Pages" if it already failed once.
5. Your permanent URL: `https://<your-user>.github.io/wall-prompt/`

## Updating later
Edit `index.html` (and copy it to `wall-prompt-generator.html` if you want the backup refreshed), then:
```
git add . ; git commit -m "Update" ; git push
```
Every PC gets the new version on its next online load (the service worker is network-first, so no stale cache).

## Use on any PC
- Open the URL in Chrome/Edge. Nothing to install.
- **Bookmark:** Ctrl+D (show bookmarks bar with Ctrl+Shift+B).
- **Install as app (recommended):** Edge: ⋯ → Apps → *Install this site as an app*. Chrome: ⋮ → Cast, save and share → *Install page as app* (or the install icon in the address bar). Then right-click the app in Start/taskbar → **Pin to taskbar**.
- **Desktop shortcut:** Chrome: ⋮ → Cast, save and share → *Create shortcut…* (tick *Open as window*). Edge: ⋯ → More tools → *Pin to taskbar* / *Pin to Start*. Or right-click Desktop → New → Shortcut → `https://<your-user>.github.io/wall-prompt/`.
- **Offline:** after one online visit the page loads without internet.

## Local backup
Keep `wall-prompt-generator.html` on each PC (or a USB/OneDrive folder) and double-click it. It works with no internet; copy falls back to a legacy method on `file://`.

## Privacy
- All prompt generation runs in the browser. There are no analytics, API calls, keys or tokens; form values are never stored or sent.
- A public GitHub Pages site means **the tool's code (HTML/JS, your prompt template and default values) is readable by anyone with the URL**. It contains no project data. Don't commit real project parameters or drawings to the repo.
- If the tool itself must be private: GitHub Pages access control needs GitHub Enterprise Cloud. Alternative: Cloudflare Pages + Cloudflare Access (free for up to 50 users, email login) – same files, no code changes.
