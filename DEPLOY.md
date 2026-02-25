# abelfazekas.com — GitHub Pages

## What’s set up

- **Entry point:** `index.html`. GitHub Pages serves it at the root, so https://abelfazekas.com loads the site.
- **Custom domain:** `CNAME` in the repo root contains `abelfazekas.com`. In GitHub: **Settings → Pages → Custom domain** set to `abelfazekas.com` (and “Enforce HTTPS” when available).
- **Static only:** `.nojekyll` in root so GitHub doesn’t run Jekyll (no special processing).

## GitHub Pages settings

1. **Settings → Pages**
2. **Source:** Deploy from a branch
3. **Branch:** `main` — **Folder:** `/ (root)`
4. **Custom domain:** `abelfazekas.com` (save, then enable “Enforce HTTPS” after DNS propagates)

## DNS (at your registrar)

- **A records** for `@` and `www`: point to GitHub’s IPs (e.g. `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`), or  
- **CNAME** for `www`: `your-username.github.io` (or `fazekasabel-code.github.io`).  
See [GitHub’s custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Updating the site

- Edit **`index.html`** (single source), then commit and push. For major redesigns you can create a working file (e.g. `site_v8.html`), then replace `index.html` when ready.

## After push

- Builds usually finish in under a minute. Check **Settings → Pages** for status.
- Visit https://abelfazekas.com (and https://www.abelfazekas.com if you use www). If the domain doesn’t resolve yet, wait for DNS (up to 48 hours, often less).
