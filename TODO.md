# abelfazekas.com — TODO

**Status:** live at https://www.abelfazekas.com — bilingual EN/HU since 16 Aug 2026.

---

## For the second pass

### 1. Proofread the Hungarian

The whole site was translated in one sitting and has not been read in context. The
register matters most on **About** (the four bio variants) and the **Works**
descriptions. Specific choices worth a decision:

- [ ] **`Szerz.`** — the Composition tag on Works, short for *szerzemény*. Uncertain
      whether it reads clearly at 9px uppercase. Alternatives: `Zene.`, or leave `Comp.`
- [ ] **`Estét betöltő mű`** for "concert-length work" (*I am the Father and Tomb of the
      Sky*). Literal-ish; *egész estés* is more standard but implies theatre/film.
- [ ] **`Program`** for Agenda, **`Bázis`** for "Based in", **`Művek`** for Works.
- [ ] **`foglaltház`** — applied, but check it reads right in all four bio variants.
- [ ] **Name order.** Hungarian names flip in HU (*Pándi Balázs*, *Babinchak Ivan*,
      *Lázár Helga*); non-Hungarian names never do. Check the mixed list in the long
      bio paragraph 3, where the two conventions sit side by side.
- [ ] **Institution names** stay in the original with Hungarian grammar around them
      (*"a Royal Conservatory of The Hague-en"*). The alternative is translating them
      (*"a hágai Királyi Konzervatóriumban"*). Currently: keep original.

### 2. Verify on the live domain

Could not be tested locally — the preview loads the file as a `data:` URL, which
blocks embeds, forms and relative images.

- [ ] YouTube embeds, **especially the *find you in the night* EP embed** (its video ID
      was changed to `uM2V6bAU7RM`)
- [ ] Bandcamp embed on *Organo Trio*
- [ ] Contact form actually delivers (posts to Formspree `maqdarey`)
- [ ] Hero image loads

### 3. Open content items

- [ ] **Contact has no visible email address** — only the form. Some people won't use a
      form. `hello@abelfazekas.com` is still unset; the email-obfuscation JS in
      `index.html` is written and waiting for a `[data-email-local]` element, currently
      dead code.
- [ ] **No `og:image`** — every shared link previews as a bare text box. Worth fixing
      before promoting the site.
- [ ] ***Studies for Qayin*** still says "Recording forthcoming" / "A felvétel hamarosan"
      — supply the audio or drop the box.
- [ ] **MU Színház production** — confirm the final title and add a link once MU
      publishes it. Add as a Works entry after the November premiere, at which point the
      Works subtitle needs to become *(2017–2026)*.
- [ ] **Tailwind CDN** (deliberately deferred) — `cdn.tailwindcss.com` is a dev-mode
      build: it compiles in the browser on every load, causing a brief flash, and it's a
      third-party request on a site that advertises collecting no data.

### 4. Older items, still open

- [ ] BIO namedropping on/off toggle (the third axis the About page was designed for)
- [ ] CV download link
- [ ] Score previews for selected works
- [ ] *Cinnabar* — media to be checked

---

## Done

- [x] Site built, deployed, custom domain (`www.abelfazekas.com`)
- [x] EN/HU toggle and full translation
- [x] Home "Currently" block refreshed after the 2026 break
- [x] Agenda: LA premiere moved to past, MU Színház added as upcoming
- [x] Long education block now follows the voice toggle (was stuck in first person)
- [x] Education blocks constrained to the bio's measure
- [x] `.gitignore` added; `.DS_Store` files untracked
