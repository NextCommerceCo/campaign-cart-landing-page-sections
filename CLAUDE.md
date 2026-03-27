# Repo Memory — campaign-cart-landing-page-partials

## Repo Overview

A library of **74 composable landing page section partials** built on [`next-campaign-page-kit`](https://www.npmjs.com/package/next-campaign-page-kit). Sections are debranded (ready for any brand via CSS token overrides) and can be composed into any landing page layout.

One standalone page not intended for composition:
- `presell-1` — self-contained presell/advertorial page

---

## Repository Structure

```
_data/
  campaigns.json              ← all campaign entries (one per src/ folder)
src/
  landing/                    ← the composable campaign — edit partials here
    _includes/                ← all 74 partials (images namespaced by section)
    _layouts/base.html        ← Swiper CDN + Tailwind + fonts + landing.js
    assets/
      css/tokens.css          ← shared design tokens (CSS custom properties)
      js/landing.js           ← unified JS: accordion + Swiper + countdown
      images/{section}/       ← per-section image dirs
    index.html                ← example composed landing page
  {section-slug}/             ← reference only — original exports, do not edit
  presell-1/                  ← standalone, not composable
```

---

## Workflows

### Composing a landing page
Work entirely in `src/landing/`. Add a new `.html` page, list sections via `campaign_include`, set content in frontmatter. Run `npm run dev` → pick `landing`.

### Checking how a section should look
Open `src/{slug}/` — these are the original individual section exports with their own preview pages. Use as visual reference when debugging display issues in the composed landing.

---

## npm Scripts

| Script | Purpose |
|--------|---------|
| `npm run dev` | Interactive campaign picker + dev server |
| `npm run build` | Build all campaigns to `_site/` |
| `npm run new <slug> <section>` | Scaffold a new section preview campaign |

---

## How to Compose a Landing Page

Create a new `.html` file inside `src/landing/`. Frontmatter holds all content variables; body lists sections in order:

```html
---
title: "My Landing Page"
page_type: product

headline: "Say Goodbye to Sleepless Nights"
body_text: "..."
cta_text: "Order Now & Save 60%"
cta_url: "checkout.html"
hero_image: "images/hero-1/hero-photo.png"
hero_image_alt: "Product photo"
---

{% campaign_include 'nav-1.html' %}
{% campaign_include 'hero-1.html' %}
{% campaign_include 'testimonials-1.html' %}
{% campaign_include 'faq-1.html' %}
{% campaign_include 'footer-1.html' %}
```

Sections read variables directly from the page context via `{{ variable_name | default: "..." }}` — no need to pass args explicitly.

**Variable naming:** most variable names are unique across section types (e.g. `headline` is hero-specific, `benefit_1` is benefits-specific). If you use two sections of the same type on one page, they'll share the same variable — use different section slugs in that case.

---

## Image Paths in `src/landing/`

All image paths are namespaced by section slug to avoid conflicts:

```
src/landing/assets/images/hero-1/hero-photo.png
src/landing/assets/images/testimonials-1/avatar-1.jpg
```

Partials reference them as `{{ 'images/hero-1/hero-photo.png' | campaign_asset }}`.

When setting image variables in frontmatter, use the namespaced path:

```yaml
hero_image: "images/hero-1/hero-photo.png"
```

---

## `landing.js` — Unified Behaviors

One file covers all interactive sections. All config lives in HTML data attributes — no section-specific JS.

### Accordion
```
[data-accordion]               wrapper; data-allow-multiple="true|false"
[data-accordion-item]          each row; data-open="true|false"
[data-accordion-toggle]        clickable button
[data-accordion-panel]         collapsible content
[data-accordion-icon]          optional chevron (gets rotate-180 class)
```

### Swiper Sliders
Root element uses `[data-swiper-root]` with config as data attributes:
```
data-slides          slidesPerView mobile    (default: 1)
data-slides-md       slidesPerView 768px+    (default: data-slides)
data-slides-lg       slidesPerView 1024px+   (default: data-slides-md)
data-gap             spaceBetween mobile px   (default: 16)
data-gap-md          spaceBetween 768px+
data-gap-lg          spaceBetween 1024px+
data-loop            loop mobile             (default: false)
data-loop-md         loop 768px+             (default: data-loop)
data-loop-lg         loop 1024px+            (default: data-loop-md)
data-centered        centeredSlides mobile   (default: false)
data-watch-overflow  hide controls when locked (default: false)
```

Children: `[data-swiper]` (the .swiper el), `[data-swiper-prev]`, `[data-swiper-next]`, `[data-swiper-controls]` (hides when locked), `.swiper-pagination`

### Countdown Timer
```
[data-countdown]               wrapper
  data-duration-minutes        timer length (default: 15)
  data-storage-key             localStorage key (default: "landing-countdown")
[data-countdown-hrs]           hours display
[data-countdown-min]           minutes display
[data-countdown-sec]           seconds display
```

---

## Design Tokens (CSS Custom Properties)

Defined in `assets/css/tokens.css` and loaded via `base.html`. Section partials reference them as:

```css
color: var(--text-primary);
background: var(--brand-primary);
```

| Token | Default |
|-------|---------|
| `--brand-primary` | `#0f75ff` |
| `--brand-secondary` | `#edf2ff` |
| `--brand-accent` | `#22c55e` |
| `--surface-bg` | `#ffffff` |
| `--surface-card` | `#f8faff` |
| `--surface-alt` | `#f1f5ff` |
| `--text-primary` | `#020b1e` |
| `--text-secondary` | `#4a5568` |
| `--text-inverse` | `#ffffff` |

Override these in a campaign-specific CSS file for branding.

---

## Section Catalog

| Category | Slugs |
|----------|-------|
| Nav | `nav-1`, `nav-2` |
| Hero | `hero-1`, `hero-3`, `hero-4`, `hero-5`, `hero-6` |
| Benefits | `benefits-1`, `benefits-2`, `benefits-3`, `benefits-4`, `benefits-5`, `benefits-8` |
| Features | `features-2`, `features-3`, `features-6`, `features-7`, `features-8`, `features-10`, `features-11` |
| Before/After | `beforeafter-1`, `beforeafter-2` |
| Problem/Solution | `problemsolution-1`, `problemsolution-2`, `problemsolution-4`, `problemsolution-5`, `problemsolution-6`, `problemsolution-7`, `problemsolution-8` |
| Testimonials | `testimonials-1`, `testimonials-2`, `testimonials-3`, `testimonials-4` |
| Reviews | `reviews-1`, `reviews-2`, `reviews-3`, `reviews-4`, `reviews-5` |
| UGC | `ugc-1`, `ugc-3`, `ugc-5`, `ugc-6` |
| Ingredients | `ingredients-1`, `ingredients-2`, `ingredients-3`, `ingredients-4`, `ingredients-5`, `ingredients-6`, `ingredients-7` |
| How-To | `how-to-1`, `how-to-2`, `how-to-3` |
| Compare | `compare-1`, `compare-4`, `compare-5` |
| Icons | `icons-1`, `icons-2`, `icons-3`, `icons-4`, `icons-5` |
| Results | `results-1`, `results-3`, `results-4`, `results-5`, `results-7` |
| Science | `science-1` |
| Media | `media-1`, `media-2` |
| FAQ | `faq-1`, `faq-2` |
| Guarantee | `guarantee-1`, `guarantee-2` |
| CTA | `cta-1`, `bottomcta-1`, `bottomcta-2` |
| Footer | `footer-1` |
| Standalone | `presell-1` (not composable) |

---

## Liquid Filters

| Filter | Example | Output |
|--------|---------|--------|
| `campaign_asset` | `{{ 'images/logo.png' \| campaign_asset }}` | `/landing/images/logo.png` |
| `campaign_link` | `{{ 'checkout.html' \| campaign_link }}` | `/landing/checkout/` |
| `campaign_include` | `{% campaign_include 'hero-1.html' %}` | renders the partial |

`campaign_include` resolves relative to the campaign's own `_includes/` folder.

---

## Key Rules

1. **Edit partials in `src/landing/_includes/`** — that is the canonical source. The `src/{slug}/` directories are reference only.
2. **Image paths are namespaced** — frontmatter image vars must use `images/{section}/filename`.
3. **`presell-1` is standalone** — do not include it in composed pages.
4. **`landing.js` covers all JS** — no section-specific scripts are needed in `src/landing/`.
5. **Tokens are shared** — `src/landing/assets/css/tokens.css` is the single source of truth for design tokens.
