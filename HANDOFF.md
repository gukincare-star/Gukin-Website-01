# GUKIN — Developer handoff (Next.js rebuild)

Rebuild in **Next.js + TypeScript + Tailwind + Framer Motion** from this static spec.

## Tokens
- Ground `#F6F5F0` · Surface `#FFFFFF` · Ink `#191817` · Muted `#6E6A63` · Rule `#E4E0D6`
- Sage `#7E9A76` / banner `#456A3E`→`#4B6749` · Sap green `#1E5B4C` / `#3E9C74`
- Plum `#3B2E4A` / `#6E5688` · Cranberry wine `#7C2A3E` / `#9C3A54`
- Barrier section gradient `#2F4A2C → #3A5936 → #456A3E`
- Type: Inter Tight (display + body, headings ≈ -0.04em), IBM Plex Mono (labels, data). Radius 12–24px.

## Signature elements
- **Logo banner**: full-bleed, square corners. Two stacked gradients — a plum wash `rgba(59,46,74,.45)→0` over a vertical sage `#456A3E → #4B6749 → warm-white transparent`, so the green dissolves downward into the page. Logo centered, links left, bag right.
- **Hero**: full-bleed photo, slow Ken-Burns scale (1.05→1.14 / 22s), plum→transparent scrim, "Wellness reinterpreted" pill, word-by-word blur→crisp headline, magnetic CTA, "Watch the film" → inline player.
- **Cart drawer**: quick-add from cards and spotlights, free-shipping progress bar, qty steppers, "Added to your ritual" toast.
- **Texture carousel**: scroll-snap row, hover scale on each tile.
- **Barrier repair**: green gradient section, 3-up imagery + 4 numbered explainers, staggered scroll reveals.
- **Before/After**: pointer + touch draggable divider revealing a full-size before image.

## Components (props-driven)
CinematicHero, Marquee, ScienceAxis, ThreeTheories, Principles (tabbed), ProductGrid/ProductCard (3D tilt + quick-add), ProductSpotlight, IngredientHotspots, HorizontalScience, TextureCarousel, BarrierScience, BeforeAfter, DataCounter, VideoFilm, RitualQuiz, CartDrawer, Testimonials, JournalGrid, Waitlist; PDP: ProductGallery, PurchaseBox, InteractiveScience, Usage, Reviews, FAQ, CompleteTheRitual, sticky mobile CTA. Chrome: ScrollProgress, auto-hide Nav.

## Content architecture
Move all arrays to `data/` or the Shopify Storefront API. Product shape: `id, slug, name, subtitle, description, price, images[], benefits[], ingredients[], usage[], category, goal, rating, reviews, badges[], variants[]`.

## Motion / performance
Framer `whileInView` for reveals (this build uses CSS `animation-timeline: view()`), `useScroll` for the progress bar and horizontal science, pointer transforms for magnetic CTAs, card tilt and before/after. Respect `prefers-reduced-motion` — already handled, swapping cinematic motion for fades.

**Images**: convert everything in `site/media/` to WebP/AVIF at ~1600px and serve through `next/image` with responsive `sizes`. Several source files are 3–7 MB; this is the single biggest performance win available.
