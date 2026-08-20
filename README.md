# GUKIN — website

Functional longevity, built from the gut out. A twelve-page static site: two compiled application pages plus ten hand-written content pages.

**Contact:** info@gukinwell.com

## Contents

```
netlify.toml            Netlify config — publish dir, caching, headers
README.md               this file
DEPLOY.md               full GitHub + Netlify deployment walkthrough
FILES.md                complete manifest — every file, what it's for
HANDOFF.md              Next.js rebuild spec for a developer
SHOPIFY-AND-TODO.md     Storefront API query + what's still to wire up
.gitignore
site/                   ← the deployed folder
```

## The pages

| Page | Type | Notes |
| --- | --- | --- |
| `index.html` | React, ~1.1 MB | Homepage — hero through FAQ, cart drawer, welcome popup |
| `product.html` | React, ~872 KB | Product detail page |
| `shop.html` | Static, ~20 KB | Nine formulations by concern, PKR pricing |
| `about.html` | Static | Brand story and formulation principles |
| `blog.html` | Static | Journal index |
| `journal-*.html` (×4) | Static | Long-form science articles |
| `shipping-returns.html` | Static | Delivery, returns, refunds |
| `terms.html` | Static | Terms of service |
| `privacy.html` | Static | Privacy policy |

The content pages carry no framework by design — a policy page has no reason to ship a megabyte of React. They load in well under a second.

## Deploy (GitHub → Netlify)

Static site, **no build step**. **Full walkthrough: `DEPLOY.md`.**

1. Create a new repository on github.com.
2. Upload **everything inside this folder** — not the folder itself. `netlify.toml` must sit at the repo root.
3. Netlify → **Add new site → Import an existing project** → pick the repo.
4. `netlify.toml` sets publish directory `site`, no build command. Deploy.

Every push to the default branch redeploys automatically.

## Pricing

All prices in PKR, 2,500–6,000, set by formulation cost:

| Product | Price |
| --- | --- |
| Revive. — NMN 7 Longevity Complex | PKR 6,000 |
| Energize. — NAD+ Next | PKR 5,600 |
| Collagen + PDRN Renewal | PKR 5,200 |
| Gut Restore Synbiotic | PKR 4,200 |
| Vitality. — Liver & Antioxidant | PKR 3,600 |
| Recover. — Sleep & Muscle | PKR 3,200 |
| Fortify. — Bone & Cellular | PKR 2,900 |
| Biotin Gummies | PKR 2,800 |
| BIOME CLEANSE | PKR 2,500 |

Free delivery over PKR 6,000 (Pakistan) and AED 150 (UAE). The cart drawer, subtotal and free-delivery progress bar all read in rupees.

## Performance

- Twenty below-fold sections use `content-visibility`, so the browser skips their layout until they approach the viewport
- Hero image marked `fetchpriority="high"`; every other image lazy-loads
- Cart drawer, FAQ modal and welcome popup are `visibility:hidden` when closed, so they cost nothing idle
- The auto-scrolling science rail stops when off-screen
- `media/` cached for a year, immutable; HTML revalidated on every request
- Content pages ship no JavaScript at all

**Still outstanding:** several photos in `site/media/` are 3–7 MB. Compress them in squoosh.app before launch — see `DEPLOY.md` Part 6. This is the largest remaining win by a wide margin.

## SEO

- Unique `<title>`, meta description, canonical URL and Open Graph tags on all twelve pages
- FAQPage schema on the homepage covering the ten highest-value questions
- Article schema on each of the four journal pieces
- All 37 FAQ answers sit in the homepage HTML whether the modal is open or not, so they are fully crawlable
- Copy targets Pakistan and UAE search intent while the brand voice stays global

## Editing

Text and photos: see `DEPLOY.md` Part 4. The static content pages are straightforward to edit directly on GitHub. `index.html` and `product.html` are compiled — search for the visible text and change only that.

## Not yet connected

- Checkout — the cart is a working front end; no payment processor attached
- The waitlist and welcome-popup forms validate but don't submit anywhere
- Product pages beyond `product.html` — every shop card currently links to it

See `SHOPIFY-AND-TODO.md`.
