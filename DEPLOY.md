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
- **Every push publishes immediately.** There is no staging environment.

---

## Editing copy: the EN/HU language system

The site is bilingual from a single file. **Any text you add needs both languages**, or
it will silently show English to Hungarian readers.

### How it works

Text lives in *pairs* of elements, and one CSS rule hides whichever doesn't match:

```css
html[data-site-lang="en"] [data-lang="hu"],
html[data-site-lang="hu"] [data-lang="en"] { display: none !important; }
```

The rule **only ever hides**. The visible side is matched by no rule at all, so it keeps
whatever `display` Tailwind gave it. That is what makes the pattern safe to use anywhere.

### Adding a line of text

Inline, inside a paragraph:

```html
<p><span data-lang="en">Premiere</span><span data-lang="hu">Bemutató</span></p>
```

A whole paragraph:

```html
<p data-lang="en">English sentence.</p>
<p data-lang="hu">Magyar mondat.</p>
```

### The one trap: `space-y-*`

Tailwind's `space-y-4` puts a top margin on every child *after the first*. With paired
language blocks the hidden one still counts as a sibling, so the visible block inherits a
stray margin. For multi-paragraph blocks, give **each language its own wrapper** carrying
the spacing, and remove it from the parent:

```html
<div class="max-w-xl text-sm leading-relaxed">
  <div data-lang="en" class="space-y-4"> …paragraphs… </div>
  <div data-lang="hu" class="space-y-4"> …bekezdések… </div>
</div>
```

### Things CSS can't reach

`<title>`, meta/OG tags and `aria-label`/`title` attributes are swapped in JavaScript.
See `I18N_META` and `I18N_ARIA` near the top of the script block. Elements opt in with
`data-i18n-aria="menu"` (the key looks up `I18N_ARIA`).

### What is deliberately *not* translated

Work titles, personal names, ensemble and institution names, and credit lists. Hungarian
personal names flip to Hungarian order in the HU text (*Fazekas Ábel*, *Pándi Balázs*);
non-Hungarian names never do.

### Checking your work

Open the page, switch to HU, and run this in the browser console. It should print two
equal numbers, `0` nested, and an empty list:

```js
console.log({
  en: document.querySelectorAll('[data-lang="en"]').length,
  hu: document.querySelectorAll('[data-lang="hu"]').length,
  nested: document.querySelectorAll('[data-lang] [data-lang]').length,
  unpaired: [...document.querySelectorAll('[data-lang="en"]')]
    .filter(el => !el.parentElement.querySelector(':scope > [data-lang="hu"]'))
    .map(el => el.textContent.trim().slice(0, 40))
});
```

Language is resolved before first paint by an inline script in `<head>`, reading
`?lang=hu` first, then `localStorage`, defaulting to English. `https://www.abelfazekas.com/?lang=hu`
is a shareable Hungarian link.

## After push

- Builds usually finish in under a minute. Check **Settings → Pages** for status.
- Visit https://abelfazekas.com (and https://www.abelfazekas.com if you use www). If the domain doesn’t resolve yet, wait for DNS (up to 48 hours, often less).
