# WEBSITE MASTER FILE
## Ábel Fazekas — Professional Site

**Motto:** Spirit as Sound as Matter  
**Vibe:** Simple, lo-fi, almost goofy  
**Status:** Planning / Pre-build

---

## 1. DESIGN PRINCIPLES

### Aesthetic Direction
- **Lo-fi but deliberate** — not "undesigned," just unpretentious
- **Goofy undertone** — humor lives in the details, not the structure
- **Readability over style** — content is dense; don't fight it
- **No stock-art polish** — if it looks like a Squarespace template, it's wrong

### Visual Language
- Monospace or near-monospace typography (?)
- Minimal color palette — black/white/one accent? or full grayscale?
- Generous whitespace
- Media (video, audio, images) should feel embedded, not showcased
- Consider: deliberate "roughness" — visible grid lines? ASCII elements? hand-drawn touches?

### Interaction
- No unnecessary animations
- Page transitions: instant or near-instant
- Hover states: subtle, functional
- Mobile: works, doesn't need to be fancy

### Anti-patterns (avoid)
- Hamburger menus (if avoidable)
- Hero images
- "Featured work" carousels
- Testimonials
- Newsletter signup popups
- Cookie banners (unless legally required)

---

## 2. SITE ARCHITECTURE

```
/
├── index.html          [Home]
├── about.html          [About]
├── works.html          [Works — filterable list of all creative work]
├── hangzavart.html     [Hangzavart!?]
├── agenda.html         [Agenda — timeline]
└── contact.html        [Contact]
```

### Navigation
- Persistent nav on all pages
- Format: horizontal list, top of page
- Order: Home | About | Works | Hangzavart!? | Agenda | Contact
- Current page indicator: underline? bold? different color?

---

## 3. PAGE SPECIFICATIONS

### 3.1 HOME

**Purpose:** Landing, identity, first impression

**Content:**
- Name: Ábel Fazekas (or stylized variant?)
- Motto: "Spirit as Sound as Matter"
- Navigation
- Nothing else? Or minimal additional context?

**Questions to resolve:**
- [ ] Background: solid color, texture, subtle pattern, or image?
- [ ] Typography treatment for the motto — display font, or same as body?
- [ ] Should there be any dynamic element (audio snippet, subtle animation)?
- [ ] Link to most recent work / upcoming event?

**Draft layout:**
```
+------------------------------------------+
|  Home  About  Composition  Misc...       |
+------------------------------------------+
|                                          |
|           Ábel Fazekas                   |
|                                          |
|      Spirit as Sound as Matter           |
|                                          |
|                                          |
+------------------------------------------+
```

---

### 3.2 ABOUT

**Purpose:** Bio, background, positioning

**Interactive features:**
1. **Voice toggle:** First person ↔ Third person
2. **Name-dropping toggle:** On ↔ Off (shows/hides institutional affiliations, collaborator names)
3. **Length toggle:** Short ↔ Long

**Implementation notes:**
- 2³ = 8 possible combinations
- Consider: write 2 versions (short/long) with conditional spans for the other toggles
- Or: generate all 8 permutations statically, swap with JS
- Toggle UI: radio buttons? switches? text links?

**Content status:**
- [x] Short bio, first person, with names ✓
- [ ] Short bio, first person, without names
- [ ] Short bio, third person, with names
- [ ] Short bio, third person, without names
- [x] Long bio, first person, with names ✓
- [ ] Long bio, first person, without names
- [ ] Long bio, third person, with names
- [ ] Long bio, third person, without names

**Additional content:**
- [ ] Photo? (if yes, what kind — formal, candid, intentionally lo-fi?)
- [ ] CV download link?
- [ ] Current affiliations list?

---

#### SHORT BIO (first person, names on)

I usually do music; composing, performing, organizing. 
Other times film, theater, philosophy, or whatever the good life demands.

Recent works include the slowest metal music you ever heard, an apophatic oratory, and a horror-documentary about suffering as a mode of attention.

Committed to breaking institutional boundaries, I founded a non-academic music academy and, before that, established some strangely academic squats. Somehow the two aren't unrelated.

BA in Composition from The Royal Conservatory of The Hague. 
MA in Composition from Musikakademie Basel. 

Currently based in Budapest and Basel.

---

#### LONG BIO (first person, names on)

I usually do music; composing, performing, organizing. 
Other times film, theater, philosophy, or whatever the good life demands.

Most of the work sits at the intersection of music, philosophy, and mathematics, often via tuning systems and feedback. Recent works include the slowest metal music you ever heard, an apophatic oratory, and five dimensional piece for five pianos.

As a performer, I play clarinets (though at this point, more research into extended techniques than standard repertoire) and I also improvise, having shared stages with Han Bennink, Fred Frith, John Duncan, Ingebrigt Håker Flaten, Jasper Stadhouders, Balázs Pándi, among others. 

Beyond composition: I recently produced a horror-documentary about suffering as a mode of attention, led an artistic research series called Research Concert Cycle at Studio Loos Den Haag, contributed to a pop-science book on prime numbers, and host thematic dinner party performances. I also run somewhat notorious workshops around consensual pain, called Violence Club.

Committed to breaking institutional dichotomies, I founded Hangzavart!? in 2021 — a non-academic music academy. Think Darmstadt meets Burning Man: intensive artistic exploration, summer camp for thoughtful rebels, Erasmus+ funded. High art. Barefoot. Before that, I ran strangely academic squats with art and music students in The Hague.

BA in Composition from the Royal Conservatory of The Hague, studying with Martijn Padding, Yannis Kyriakides, Cornelis de Bondt, and Raviv Ganchrow. During those years, I also attended courses at the Institute of Sonology, the ArtScience faculty of the Royal Academy of Arts, and Leiden University. MA in Composition from Musikakademie Basel with Johannes Kreidler and Johannes Caspar Walter. Visiting student at Schola Cantorum Basel, studying with Johannes Menke and Johannes Keller. Over the years, I attended masterclasses with Helmut Lachenmann, Georg Friedrich Haas, Giorgio Netti, Jennifer Walshe, Peter Ablinger, Nicolas Collins, and Marc Sabat.

Currently based in Budapest and Basel.

---

### 3.3 WORKS

**Purpose:** Single filterable portfolio of all creative work

**Structure:** Reverse chronological list (most recent first), filterable by category

**Filter categories (checkboxes):**
- [ ] Composition (concert works, chamber music, solo pieces)
- [ ] Theater (music theater, performance)
- [ ] Film (scores, production)
- [ ] Improvisation (recordings, live)

**Filter behavior:**
- No boxes checked → show all
- Any boxes checked → show only matching (OR logic: if "Composition" + "Theater" checked, show works tagged with either)
- Each work can have multiple tags

**Implementation:**
```html
<!-- Each work item -->
<article class="work" data-tags="composition,theater">
  ...
</article>

<!-- Filter UI -->
<fieldset class="filters">
  <label><input type="checkbox" value="composition"> Composition</label>
  <label><input type="checkbox" value="theater"> Theater</label>
  <label><input type="checkbox" value="film"> Film</label>
  <label><input type="checkbox" value="improvisation"> Improvisation</label>
</fieldset>
```

```javascript
// ~15 lines of JS
const checkboxes = document.querySelectorAll('.filters input');
const works = document.querySelectorAll('.work');

function filterWorks() {
  const checked = [...checkboxes].filter(cb => cb.checked).map(cb => cb.value);
  works.forEach(work => {
    const tags = work.dataset.tags.split(',');
    const show = checked.length === 0 || checked.some(c => tags.includes(c));
    work.style.display = show ? '' : 'none';
  });
}

checkboxes.forEach(cb => cb.addEventListener('change', filterWorks));
```

**Per-work information:**
- Title (styled: italics or quotes?)
- Instrumentation / forces
- Duration (if relevant)
- Year
- Tags (for filtering)
- Media: video embed, audio player, image gallery, or external link
- Brief description (optional)

**All works with tags:**

| Title | Year | Tags | Media | Status |
|-------|------|------|-------|--------|
| THOU | 2025– | composition | Audio | [x] |
| I am the Father and Tomb of the Sky | 2025 | composition, improvisation | Video + EP | [x] |
| The Gift of Pain | 2025 | film | Trailer + Links | [x] |
| Egy tökéletes nap | 2024 | theater | External link | [x] |
| The True Life is Absent | 2023 | composition | Video | [x] |
| a responsible man... | 2023 | composition | Audio | [x] |
| Thanatos | 2022 | theater | Pictures | [x] |
| Francesco d'Assis | 2022 | theater | Pictures | [x] |
| Studies for Qayin | 2022 | composition | Audio | [x] |
| Cinnabar | 2021 | composition | TBD | [ ] |
| Over Against Other | 2020 | composition | Video + Score | [x] |
| for the Royal Trash Ensemble | 2018 | theater | Video | [x] |
| Organo Trio | 2018 | improvisation | Bandcamp | [x] |
| 651237284 | 2018 | composition | Video | [x] |
| please, come onto the stage... | 2018 | composition, theater | Video | [x] |
| Vocal Project | 2017 | composition | Video | [x] |

**→ DETAILED DESCRIPTIONS: See "DETAILED WORK DESCRIPTIONS" section below**
**Progress:** 16 works complete ✓

**Questions to resolve:**
- [ ] Expand on click, or all visible?
- [ ] Filter UI styling (minimal, fits lo-fi aesthetic)

**Layout:** List format with expandable details

---

#### DETAILED WORK DESCRIPTIONS

##### THOU

*for three sopranos, two clarinets, percussion, viola, cello, and double bass — 90' — 2025–*

**Conductor:** Giorgi Shekiladze

**Ensemble:**
- Alena Verin-Galitskaya, soprano
- Anna Juniki, soprano
- Charis Orfanidou, soprano
- Benjamin Pallagi, clarinets
- Nina Pavšek, clarinets
- Dániel Láposi, percussion
- Anna Jurriaanse, viola
- James Morley, cello
- Pietro Elia Barcellona, double bass

**Partial premiere:** June 2025, Basel

**Short description (for list view):**
An apophatic oratory for three sopranos and chamber ensemble. 90 minutes of microtonal music exploring the impossible address — the Self reaching toward an Other that cannot be named.

**Expanded description (for detail view):**
*THOU* is an apophatic oratory for three sopranos, two clarinets, percussion, viola, cello, and double bass. The work draws on the apophatic theological tradition — the via negativa — in which the divine (or the Other) can only be approached through negation, through saying what it is not.

The music is microtonal throughout. The libretto is an original text based on cut-ups of Pseudo-Dionysius, Meister Eckhart, Levinas, Bataille, and Rimbaud.

90 minutes. Work in progress. Partially premiered June 2025, Basel.

Supported by Ernst Göhner Stiftung.

**Media:**
- [x] Recording of first movement: https://youtu.be/QIXdTnK47QI

---

##### I am the Father and Tomb of the Sky

*for voice, electric guitar, fretless bass, and drums — open form, 60'+ — 2025*

**Ensemble:** [Lithopaedion](https://lithopaedion.com)
- Ábel Fazekas, voice
- Mikael Szafirowski, guitar
- Clemens Schumacher, bass
- Ivan Liuzzo, drums

**Premiere:** December 2025, Basel

**Short description (for list view):**
A concert-length work for metal band and cut-up Bataille. Walls of noise, extended silences, controlled feedback chains, microtonal systems under heavy distortion.

**Expanded description (for detail view):**
*I am the Father and Tomb of the Sky* is a concert-length composition written for Lithopaedion, a Swiss ensemble formed specifically for this project. The title comes from Georges Bataille's poem "The Archangelical," and the libretto is a loose cut-up of his poetry throughout.

The piece sits at the intersection of experimental metal and contemporary composition — not as stylistic quotation but as genuine synthesis. The instrumentation resembles a standard metal band, but all four musicians are active in the international new-music scene as both performers and composers. The result: walls of noise interrupted by extended silences, tightly controlled but chaotic feedback chains, and intricate microtonal systems subjected to heavy distortion.

Open form. No fixed duration. The December 2025 premiere ran over 60 minutes.

*I am the Son and the Tomb of the Sky* is an EP composed of two fragments from the full composition:
- "and the white drool in my mouth": https://youtu.be/l79FXhDocsU
- "find you in the night": https://youtu.be/NOoF7TzSF38

**Media:**
- [ ] Video (uploading to Drive)
- [x] Demo recording (December 2025, two excerpts)
- [x] EP: *I am the Son and the Tomb of the Sky* (two fragments)

---

##### The True Life is Absent

*for mezzo-soprano, clarinet/bass clarinet, and bass clarinet — 13' — 2023*

**Performers:**
- Xenia Lemberski, voice
- Martijn Susla, clarinet / bass clarinet
- Ábel Fazekas, bass clarinet

**Premiere:** June 2023, Basel

**Libretto:** Aisha Pagnes

**Short description (for list view):**
Medieval counterpoint meets microtonality meets extended techniques. The voice embodies the immediate realm of the I; the clarinets, those parts of the self not yet recollected or recognized. The piece unfolds this drama.

**Expanded description (for detail view):**
*The True Life is Absent* is scored for mezzo-soprano and two bass clarinets (one doubling clarinet). The title comes from Rimbaud — "La vraie vie est absente" — a line Levinas also quotes. The libretto, written by Aisha Pagnes, draws on Levinas's 1948 essay "Reality and its Shadow."

Musically, the piece braids medieval counterpoint, microtonality, and extended techniques. The voice represents the immediate, present self — the I in the moment of its own speaking. The two clarinets figure as the unrecognized or unrecollected parts of the self, the shadow-regions that accompany but never fully appear to consciousness. The work is the unfolding encounter between these.

A technical note: the clarinet's harmonic spectrum naturally lacks the octave. Here, this absence becomes structural — the octave is treated as a false unity, a threat within the harmonic universe rather than a resolution.

**Media:**
- [x] Video: https://youtu.be/k-zVOjYn8rA

---

##### a responsible man limits himself to five dimensions

*for five pianos in custom tuning — 14' — 2023*

**Premiere:** November 2023, Musikakademie Basel (fixed media playback, all parts performed by Jacob Mason)

**Short description (for list view):**
What if harmony could be imagined in spatial terms? Five pianos explore a five-dimensional hypercube — impractical, but not *unreasonably* so.

**Expanded description (for detail view):**
Leonhard Euler's 1739 treatise proposed modeling harmony as a six-dimensional hypercube. A responsible person recognizes this as one dimension too many. Here, five pianos in custom tuning navigate a merely five-dimensional pitch space — still speculative, still impractical, but within the bounds of decency. Mathematical and musical terms collapse into one another: inversion is inversion, rotation is rotation. The composition is made entirely in geometric terms.

**Media:**
- [x] Audio recording (surround mixed to stereo)

---

##### Thanatos

*performance — 20' — 2022*

**Performers:**
- Alice von Sinnen
- Janis

**Music:** Ábel Fazekas

**Premiere:** October 2022, Theater Basel

**Media:**
- [x] Pictures (in Drive)

---

##### Francesco d'Assis

*music theater — 20' — 2022*

A music theater dedicated to Charity.

**Performers:**
- Ailen Monti, lute & voice
- Carolina Bermejo †, voice
- Aurore Gontard, voice

**Music:** Ábel Fazekas

**Premiere:** October 2022, Theater Basel

**Media:**
- [x] Pictures (in Drive)

---

##### Studies for Qayin

*for voice, two prepared pianos, and experimentalorgel — 2022*

**Premiere:** 2022, St. Martin Church, Kassel

**Short description (for list view):**
Short studies for a larger chamber work, made during a residency exploring the experimentalorgel at St. Martin, Kassel.

**Expanded description (for detail view):**
*Studies for Qayin* is a set of short pieces composed during a residency at St. Martin Church in Kassel, exploring the possibilities of their recently built experimentalorgel. The studies serve as preparation for a longer chamber work, *Qayin*, yet to be realized.

**Media:**
- [x] Audio recording (Study No. 3)

---

##### Cinnabar

*for voice, two intonarumori, and two percussion — 5' — 2021*

**Premiere:** 2021, Tinguely Museum, Basel

**Media:**
- [ ] TBD (may have audio/video/pictures — to check)

---

##### Over Against Other

*for flute and percussion — 20' — 2020*

**Commissioned by:** Dániel Láposi and Kristóf Siklósi

**Premiere:** 2020, Amadinda Studio

**Media:**
- [x] Video
- [x] Score preview

---

##### for the Royal Trash Ensemble

*music theater — 18' — 2018*

**Media:**
- [x] Video: https://youtu.be/6HoFvDvCBgw

---

##### Organo Trio

*free improvisation — 2018*

**Released:** December 18, 2018

**Personnel:**
- Aurélie Nyirabikali Lierman, OrganoVoice
- Ábel Fazekas, bass clarinet
- Riccardo Marogna, bass clarinet

Recording, Mixing, Mastering: Madhav Agarwal
Cover Photo: Riccardo Marogna

**Description:**
We first started playing together sometime in early 2017 when we met as students at The Royal Conservatory of The Hague. The three of us share a long history in both improvisation and composition, and it's the combination of these two approaches to music-making that continues to serve us as a basis for all our musical ideas. In our self-titled debut album *Organo* we didn't use pre-agreed forms or musical material, but nevertheless our improvisation cannot be said to be totally free either. Through constant reflection and discussion when rehearsing, we 'composed' a quite strict and distinct musical universe within which we could improvise 'freely'. *Organo* is an edited and mixed version of our very first studio recording session.

**Media:**
- [x] Bandcamp: https://organo.bandcamp.com/album/organo

---

##### 651237284

*fixed media — 10' — 2018*

**Performers:**
- Robert Landfermann, double bass
- Cody Takacs, double bass

**Media:**
- [x] Video: https://youtu.be/mkWIL4o5Bcc

---

##### please, come onto the stage and save me

*text score — 2018*

**Media:**
- [x] Video: https://youtu.be/Z58JYKSNioc

---

##### Vocal Project

*graphic score + live electronics — 7' — 2017*

**Performers:**
- Rutger de Groot, voice
- Ábel Fazekas, composition & electronics

**Premiere:** February 2017, Royal Conservatory of The Hague, Arnold Schoenbergzaal

**Media:**
- [x] Video: https://youtu.be/SOqeHpl0oB4

---

##### Egy tökéletes nap

*theater music — 2024*

Music for *Egy tökéletes nap* (*A Perfect Day*), a theater production directed by Szenteczki Zita at 6SZÍN, Budapest. Premiered June 14, 2024. 150 minutes.

The play documents the final years of Karsai Dániel (1977–2024), a constitutional lawyer diagnosed with ALS who publicly fought for end-of-life autonomy in Hungary, taking his case to the European Court of Human Rights. He co-wrote the play about his own life and death with dramaturg Bíró Bence and director Szenteczki Zita. Movement and choreography (Kovács Domokos) are central — the physical vocabulary of jiu-jitsu, which Karsai practiced, becomes a language for the body's struggle against its own collapse.

Karsai died in September 2024.

**Credits:**
- Writers: Karsai Dániel, Szenteczki Zita, Bíró Bence
- Director: Szenteczki Zita
- Music: Ábel Fazekas
- Choreography: Kovács Domokos
- Set design: Lázár Helga

**Link:** [6szin.hu](https://6szin.hu/repertoar/karsai_daniel__szenteczki_zita__biro_bencebregy_tokeletes_nap)

---

##### The Gift of Pain

*film — horror/documentary — 69 min — 2025*

A Swiss horror-documentary directed by Ivan and Atanáz Babinchak. Through self-inflicted acts and wordless rituals, the film observes how suffering, stripped of meaning or justification, becomes a way of seeing. Episodic in structure, devoid of dialogue, it stands between documentation and performance art. The camera's clinical yet compassionate gaze reveals pain not as spectacle or confession, but as a mode of attention. A dark hedonism runs beneath: the will to experience life in its entirety — even beyond one's own limit.

Shot in Basel (Neues Kino, Dome Tattoo, Riverside Boxing). Festival premiere at LUFF – Lausanne Underground Film Festival, October 2025.

**Ábel's roles:** Producer, co-writer, art direction, music, cast

**Credits:**
- Directors: Ivan Babinchak, Atanáz Babinchak
- Producers: Ábel Fazekas, Anouk Neyens
- Screenplay: Ivan Babinchak, Sanna Bo, John Duncan, Ábel Fazekas, Alice Von Sinnen, Anouk Neyens, Dániel Láposi
- Music: Ábel Fazekas, C.P.E. Bach
- Sound Design: Emcsi
- Cast: Ivan Babinchak, Sanna Bo, John Duncan, Ábel Fazekas, Alice Von Sinnen, Anouk Neyens, Dániel Láposi, Emcsi, Atanáz Babinchak

**Links:**
- [Trailer](https://youtu.be/CtR6r9WN-EE)
- [IMDB](https://www.imdb.com/title/tt36016563/)
- [Letterboxd](https://letterboxd.com/film/the-gift-of-pain/)

---

**Other potential items (TBD):**
- Musica Ficta | Cybernetics Through Time (Basel project)
- Feedback Unbound

---

### 3.4 HANGZAVART!?

**Purpose:** Dedicated section for the music academy Ábel founded

**What it is:**  
Hangzavart!? is a non-academic music academy — "a laboratory for music education" — founded by Ábel in 2021. It brings together musicians from all backgrounds to challenge norms, dissolve hierarchies, and explore new ways of learning and creating. The tagline: "High art. Barefoot."

Think Darmstadt Summer Course meets Burning Man: intensive artistic exploration within a community that feels like summer camp for thoughtful rebels. The network has grown through Erasmus+ partnerships across Europe.

**External site:** https://hangzavart.com

**Content for this page:**
- [ ] Brief description (can pull from above)
- [ ] Link to hangzavart.com for full info
- [ ] Possibly: selected images from retreats
- [ ] Role clarification: "Founded by Ábel Fazekas in 2021"

**Questions:**
- [ ] Does this need its own subpages, or just a single page with link-out?
- [ ] Different visual treatment than rest of site? (probably not — keep consistent)
- [ ] Pull in testimonials or keep it minimal?

---

### 3.5 AGENDA

**Purpose:** Past and upcoming events

**Format:** Vertical timeline, reverse chronological (upcoming first, then past)

**Scope:** 2025 onwards only

**Implementation notes:**
- "Present" marker should be date-aware (current date: February 18, 2026)
- Past events: visually distinct (grayed out or lighter)
- Links where available

---

#### EVENTS

**UPCOMING**

**March 2026** (TBA)
*The Gift of Pain* — US Premiere
Los Angeles, US
[Experimental Forum](https://www.experimentalforum.org/2026)

---

── PRESENT ──

---

**PAST**

**November 29, 2025**
Interdiszciplináris Metal Konferencia — Conference Presentation
ELTE Esztétika Tanszék, Budapest, HU
[Event info](https://www.elte.hu/content/i-interdiszciplinaris-metal-konferencia.e.19195)

**November 17–18, 2025**
*The Gift of Pain* — Premiere
Lausanne Underground Film Festival, Lausanne, CH
[LUFF 2025](https://2025.luff.ch/en/programme/film/documentaires/the-gift-of-pain/)

**June 14, 2025**
*THOU* — First Movement
Kartäuserkirche, Basel, CH

---

### 3.6 CONTACT

**Purpose:** How to reach you

**Content:**
- Email (obfuscated or not?)
- Social links? (which platforms?)
- Physical address? (probably not)
- Contact form? (probably unnecessary)

**Draft:**
```
Email: [email]

[optional social icons or text links]
```

---

## 4. TECHNICAL DECISIONS

### Stack options

| Option | Pros | Cons |
|--------|------|------|
| **Static HTML/CSS** | Total control, lo-fi authentic, fast | Manual updates, no templating |
| **11ty / Hugo** | Templating, markdown content, fast builds | Build step, slight learning curve |
| **Single HTML file** | Maximum simplicity, goofy energy | Unwieldy if content grows |

**Recommendation:** Static site generator (11ty?) for maintainability, but keep output minimal

### Hosting
- Netlify / Vercel / GitHub Pages (all free, fast, simple)
- **Domain:** abelfazekas.com ✓ (already purchased)

### Media hosting
- Self-hosted: images, audio
- External embeds: YouTube/Vimeo for video (unless self-hosting matters)
- Consider: bandwidth, loading speed, control

### Google Drive Resources
- **Website assets folder:** https://drive.google.com/drive/folders/1zp3lZvUKztYUa4yPG9_mMT0mvWh07Osx
- **Media folder (most recent):** https://drive.google.com/drive/folders/1HsC_LxvIlsCqyMuNkX2tn2QK2BWb3MQT
- **Website planning folder:** https://drive.google.com/drive/folders/1PawdjKH9knpniAeqphM7vUoCeKwl-y3F

---

## 5. CONTENT INVENTORY

### Text content needed
- [ ] Bio (2/8 versions done — short+long first person with names)
- [x] ~~Work descriptions (per piece)~~ → Done (16 works total)
- [ ] Event descriptions (optional)
- [x] ~~Hangzavart!? explanation~~ → Done

### Media assets needed
| Asset | Type | Source | Status |
|-------|------|--------|--------|
| THOU audio | Audio embed | https://youtu.be/QIXdTnK47QI | [x] have |
| Father and Tomb video | Video embed | Uploading to Drive | [ ] pending |
| Father and Tomb EP | Audio | YouTube (2 tracks) | [x] have |
| responsible man audio | Audio embed | Surround→stereo mix | [x] have |
| Studies for Qayin audio | Audio embed | Study No. 3 recording | [x] have |
| Cinnabar media | TBD | To check | [ ] TBD |
| Over Against Other video | Video embed | Available | [x] have |
| Over Against Other score | Score preview | Available | [x] have |
| True Life video | Video embed | https://youtu.be/k-zVOjYn8rA | [x] have |
| Thanatos pictures | Image gallery | Google Drive | [x] have |
| Francesco pictures | Image gallery | Google Drive | [x] have |
| for the Royal Trash Ensemble | Video embed | https://youtu.be/6HoFvDvCBgw | [x] have |
| Organo Trio | Bandcamp embed | https://organo.bandcamp.com/album/organo | [x] have |
| 651237284 | Video embed | https://youtu.be/mkWIL4o5Bcc | [x] have |
| please, come onto the stage... | Video embed | https://youtu.be/Z58JYKSNioc | [x] have |
| Vocal Project | Video embed | https://youtu.be/SOqeHpl0oB4 | [x] have |
| Egy tökéletes nap | External link | 6szin.hu | [x] have |
| Gift of Pain trailer | Video embed | YouTube | [x] have |
| Headshot/photo | Image | Google Drive | [x] selected |
| Favicon | Image | Create | [ ] |

**Note:** Photos and media available in Google Drive — need to select/curate for site.

---

## 6. OPEN QUESTIONS

### High priority
- [x] ~~Domain name?~~ → abelfazekas.com
- [x] ~~What is Hangzavart!?~~ → Non-academic music academy, founded 2021
- [x] ~~Photo selection~~ → Done
- [x] ~~Cinnabar details?~~ → Done
- [x] ~~Over Against Other details?~~ → Done

### Medium priority
- [ ] Color palette decision
- [ ] Typography selection
- [ ] About page toggle UI design
- [ ] CV: include as download?

### Low priority / later
- [ ] Analytics: yes/no? (if yes, privacy-respecting option like Plausible)
- [ ] Multilingual? (EN / FR / HU?)
- [ ] Dark mode toggle?

---

## 7. REFERENCES / INSPIRATION

*Add links to sites with energy you like*

- [ ] ...
- [ ] ...
- [ ] ...

---

## 8. TIMELINE / MILESTONES

| Phase | Tasks | Target |
|-------|-------|--------|
| **1. Content** | Write all bio versions, gather media | [ ] |
| **2. Design** | Finalize visual direction, mockups | [ ] |
| **3. Build** | Code site, test | [ ] |
| **4. Launch** | Deploy, domain setup | [ ] |

---

## CHANGELOG

- **[date]** — Initial master file created

