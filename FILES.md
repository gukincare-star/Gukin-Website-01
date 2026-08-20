# FILES.md — complete repository manifest

Every file that goes into the GitHub repository, in the structure it must keep.
**Twelve HTML pages, 55 images, seven root files — 74 files total.**

---

## Root structure

Upload the **contents** of `gukin-final`, not the folder itself. `netlify.toml` must sit at the top level of the repository.

```
<your-repo-root>/
├── .gitignore
├── netlify.toml
├── README.md
├── DEPLOY.md
├── FILES.md
├── HANDOFF.md
├── SHOPIFY-AND-TODO.md
└── site/
    ├── index.html                                  Homepage
    ├── product.html                                Product detail page
    ├── shop.html                                   Shop / all products
    ├── about.html                                  About us
    ├── blog.html                                   Journal index
    ├── journal-gut-longevity-axis.html             Article
    ├── journal-nad-depletion-aging.html            Article
    ├── journal-pdrn-peptides.html                  Article
    ├── journal-collagen-zinc-performance.html      Article
    ├── shipping-returns.html                       Shipping & returns policy
    ├── terms.html                                  Terms of service
    ├── privacy.html                                Privacy policy
    └── media/                                      55 images
```

Two rules for the whole process:

1. **`netlify.toml` at the repository root.** Inside a subfolder, Netlify won't find it and every page 404s.
2. **Never rename `site/` or `site/media/`.** Every image is referenced as `media/filename`.

---

## Root files

| File | Required? | What it does |
| --- | --- | --- |
| `netlify.toml` | **Yes** | Publish directory `site`, no build command, one-year immutable cache on `media/`, revalidate on HTML, security headers, 404 fallback. |
| `.gitignore` | Optional | Keeps `.DS_Store` and `Thumbs.db` out of the repo. |
| `README.md` | Optional | Project overview and editing notes. |
| `DEPLOY.md` | Optional | Step-by-step GitHub + Netlify walkthrough. |
| `FILES.md` | Optional | This manifest. |
| `HANDOFF.md` | Optional | Next.js rebuild spec — tokens, components, motion. |
| `SHOPIFY-AND-TODO.md` | Optional | Storefront API query and field mapping. |

The five `.md` files are documentation. Deleting them changes nothing on the live site — keep them so future you, or a developer, has the context.

---

## The twelve pages

### Application pages (React, self-contained)

| Page | Size | What it holds |
| --- | --- | --- |
| `index.html` | ~1.1 MB | Homepage. Video-poster hero, GUKIN axis with hover reveals, three theories, the new luxury, six core principles, concern tiles, the full range, cleanser and gummy spotlights, ingredient hotspots, the auto-scrolling eight-panel science rail, actives, textures, barrier repair, before/after slider, data counters, testimonials, Find Your Ritual quiz, journal, waitlist, FAQ rail + 37-question modal, cart drawer, welcome popup. |
| `product.html` | ~872 KB | Product detail page. Gallery with thumbnails, subscribe/one-time purchase box, quantity stepper, interactive actives, usage timeline, reviews, FAQs, complete-the-ritual, sticky mobile CTA. |

Both are fully self-contained apart from the photos — all CSS, JavaScript, fonts and the logo are inlined. Nothing to install, nothing to build.

### Content pages (static HTML, ~14–30 KB each)

| Page | What it holds |
| --- | --- |
| `shop.html` | All nine formulations grouped by concern — gut, skin, longevity, strength — with PKR prices and jump links. |
| `about.html` | Why GUKIN exists, what functional longevity means, the six formulation principles, where we operate, what we won't claim. |
| `blog.html` | Journal index — featured article plus three cards. |
| `journal-gut-longevity-axis.html` | The gut–longevity axis. Intestinal permeability, LPS, chronic inflammation, what repairs the barrier. |
| `journal-nad-depletion-aging.html` | NAD+ depletion. What the coenzyme does, sirtuins and PARPs, whether NMN is worth it. |
| `journal-pdrn-peptides.html` | PDRN and peptides. Hydration versus signalling, fibroblast activation, realistic timelines. |
| `journal-collagen-zinc-performance.html` | Sleep, magnesium and the repair window. Why Gulf and South Asian climates make recovery harder. |
| `shipping-returns.html` | Processing, delivery times per city tier, charges, cash on delivery, tracking, damage, returns, refunds, hot-climate packing. |
| `terms.html` | Twenty-one section terms of service, governed by Pakistani law, with UAE consumer rights preserved. |
| `privacy.html` | What we collect, how we use it, who we share it with, cookies, retention, security, minors, your rights. |

These are deliberately **plain HTML with no React and no build step** — a privacy policy has no reason to ship a megabyte of framework. Each loads in well under a second. Every one carries its own `<title>`, meta description, canonical URL and Open Graph tags; the four articles also carry Article schema.

---

## `site/media/` — 55 images

Referenced as `media/FILENAME`, relative to the HTML. **Do not rename the folder or any file** unless you also change the `src`.

### Brand

| File | Used for |
| --- | --- |
| `gukin-logo-white.png` | Logo — banner and footer on all ten content pages |

### Hero and lifestyle

| File | Used for |
| --- | --- |
| `lifestyle-bath.jpg` | Homepage hero, Ken-Burns zoom (loads first, high priority) |
| `lux-estate.jpg` | The new luxury — the range, closing row; About page |
| `lux-martini.jpg` | The new luxury — "Out late, still yourself" |
| `lux-suit.jpg` | The new luxury — "The considered daily" |
| `lux-candlelit.jpg` | The new luxury — "Dinner, unhurried" |
| `lux-rain.png` | Spare |

### GUKIN axis — hover reveals

`ax-gut.jpg` (Gut, plus `pr-gut.jpg` as its second reveal) · `ax-microbiome.jpg` · `ax-inflammation.jpg` · `ax-cell.jpg` · `skin-glow.jpg` (Skin) · `ax-skin.jpg` (spare)

### Concern tiles and principles

`pr-gut.jpg` · `pr-skin.jpg` · `pr-longevity.jpg` (spare) · `pr-strength.jpg` · `pr-barrier.jpg` · `pr-antiaging.jpg`

### Products

| File | Product |
| --- | --- |
| `gummies.png` | Biotin Gummies — PKR 2,800 |
| `cleanser.png` | BIOME CLEANSE — product page |
| `cleanser-flatlay.jpg` | BIOME CLEANSE spotlight — PKR 2,500 |
| `p-vitality.jpg` | Vitality. — PKR 3,600 |
| `p-recover.jpg` | Recover. — PKR 3,200 |
| `p-fortify.jpg` | Fortify. — PKR 2,900 |
| `p-energize.png` | Energize. — PKR 5,600 |
| `p-revive.jpg` | Revive. — PKR 6,000 |
| `p-renew.png` | Spare |

### Ingredient science

`lab-zinc.jpg` (Zinc L-Carnosine) · `lab-theanine.jpg` (L-Theanine) · `lab-nad.jpg` (NMN → NAD+, also the Functional Longevity principle and the NAD+ article) · `lab-resveratrol.jpg` (Trans-Resveratrol)

### Textures

`tex-gel-clear.jpg` · `tex-gel-pink.jpg` · `tex-green-oil.jpg` · `tex-cream-gold.jpg` · `tex-sage-cream.jpg` · `tex-serum-drop.jpg` (carousel) · `tex-cells-green.jpg` · `tex-aloe.jpg` · `tex-leaf-drops.png` · `tex-petri-green.png` · `emboss-sage.png` · `emboss-white.png` · `tex-cream-white.jpg` (spare)

### Skin and journal

`skin-drops.jpg` / `skin-glow.jpg` (before/after slider) · `skin-cream-face.jpg` (PDRN article) · `skin-freckles.jpg` · `journal-gut.png` (featured article)

### Spares — safe to delete

`ax-skin.jpg` · `cleanser-box.jpg` · `cleanser-hero.jpg` · `gummies-clean.png` · `gummies-model.jpg` · `gummies-splash.jpg` · `lux-rain.png` · `molecule-red.png` · `p-renew.png` · `pr-longevity.jpg` · `tex-cream-white.jpg`

`molecule-red.png` is the molecule reference photograph — the site draws those glyphs as vectors, so it isn't used.

---

## Upload checklist

- [ ] `netlify.toml` visible in the repository **root** file list
- [ ] `site/` exists at the root
- [ ] All **twelve** `.html` files present in `site/`
- [ ] `site/media/` contains **55 files** (44 if you drop the spares)
- [ ] Nothing renamed
- [ ] GitHub's "Add a README" checkbox was left unticked

74 files fits inside GitHub's 100-file-per-commit web limit, so one drag-and-drop does it — but the media folder is large, so expect a few minutes.

---

## What is *not* in the repository

No `node_modules/`, no `package.json`, no lockfile, no build output folder — `site/` **is** the output. No `.env`; if you add a Shopify token later it belongs in Netlify's environment variables, never in the repo.

## Every internal link resolves

All twelve pages cross-link and every internal link was checked against the file list. There are no 404s.

The earlier `theory-*.html` and `collection-*.html` links are gone — theory links now point at the matching journal article, collection links at the relevant `shop.html` section.
