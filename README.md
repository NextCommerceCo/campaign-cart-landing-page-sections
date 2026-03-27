# Campaign Cart Landing Page Sections

A library of **74 composable landing page section partials** for building presale landing pages and advertorial presell pages — built on [`next-campaign-page-kit`](https://www.npmjs.com/package/next-campaign-page-kit).

**Live previews:**
- [Landing sections smoke test](https://next-campaign-page-sections.netlify.app/landing/)
- [Presell-1 example](https://next-campaign-page-sections.netlify.app/presell-1/)

---

## In the Campaign Cart ecosystem

```
campaign-cart-landing-page-sections   ← you are here
  └── Section partials (landing + presell)
  └── Compose into pages (landing.html, presell-example.html)
        ↓
campaign-cart-starter-templates
  └── Drop composed pages in as landing or presell pages
  └── Connects to checkout funnel
```

This repo is the **source of sections**. You pick the sections you need, set content variables in frontmatter, and compose a page. That page then drops into [campaign-cart-starter-templates](https://github.com/NextCommerceCo/campaign-cart-starter-templates) as a landing or presell entry point to a checkout funnel.

---

## Getting started

**1 — Clone and install**
```bash
git clone https://github.com/NextCommerceCo/campaign-cart-landing-page-sections
cd campaign-cart-landing-page-sections
npm install
```

**2 — Start the dev server**
```bash
npm run dev
```

Select `landing` or `presell-1` from the list → opens `http://localhost:3000/{slug}/`.

---

## Composing a landing page

Create a new `.html` file inside `src/landing/`. Frontmatter holds all content variables; the body lists which sections to include and in what order.

```html
---
title: "My Landing Page"
page_type: product

headline: "Say Goodbye to Sleepless Nights"
body_text: "Doctor engineered formula designed for results."
cta_text: "Order Now & Save 60%"
cta_url: "checkout.html"

hero_image: "images/hero-1/hero-photo.png"
hero_image_alt: "Product photo"

review_count: "27,517+ 5-Star Reviews"
testimonials_heading: "What Our Customers Are Saying"
---

{% campaign_include 'nav-1.html' %}
{% campaign_include 'hero-1.html' %}
{% campaign_include 'testimonials-1.html' %}
{% campaign_include 'faq-1.html' %}
{% campaign_include 'footer-1.html' %}
```

Sections read variables from the page context directly — no need to pass arguments to each `campaign_include`. See `src/landing/landing.html` for a full smoke test with every section rendered.

### Image paths

All images in `src/landing/` are namespaced by section slug to prevent conflicts:

```yaml
hero_image: "images/hero-1/hero-photo.png"   # not "images/hero-photo.png"
```

### Branding

Override the CSS custom properties in `tokens.css` for your brand colors:

```css
:root {
  --brand-primary:   #your-color;
  --brand-secondary: #your-color;
  --brand-accent:    #your-color;
}
```

---

## Section catalog

| Category | Available sections |
|----------|--------------------|
| Nav | `nav-1`, `nav-2` |
| Hero | `hero-1`, `hero-3`, `hero-4`, `hero-5`, `hero-6` |
| Benefits | `benefits-1` `benefits-2` `benefits-3` `benefits-4` `benefits-5` `benefits-8` |
| Features | `features-2` `features-3` `features-6` `features-7` `features-8` `features-10` `features-11` |
| Before/After | `beforeafter-1`, `beforeafter-2` |
| Problem/Solution | `problemsolution-1` `problemsolution-2` `problemsolution-4` `problemsolution-5` `problemsolution-6` `problemsolution-7` `problemsolution-8` |
| Testimonials | `testimonials-1`, `testimonials-2`, `testimonials-3`, `testimonials-4` |
| Reviews | `reviews-1`, `reviews-2`, `reviews-3`, `reviews-4`, `reviews-5` |
| UGC | `ugc-1`, `ugc-3`, `ugc-5`, `ugc-6` |
| Ingredients | `ingredients-1` `ingredients-2` `ingredients-3` `ingredients-4` `ingredients-5` `ingredients-6` `ingredients-7` |
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

Preview any individual section at `http://localhost:3000/{slug}/` during `npm run dev`.

---

## Presell page

`presell-1` is a standalone advertorial/listicle page template. It is **not** composable — it is a single self-contained page. Preview it at `http://localhost:3000/presell-1/`.

See `src/presell-1/presell-example.html` for a working example.

---

## Interactive sections

All interactive behaviors are handled by a single `assets/js/landing.js` — no section-specific scripts needed:

- **Accordion** — FAQ, ingredients, and benefits sections
- **Swiper sliders** — testimonials, reviews, UGC, before/after, ingredients carousels
- **Countdown timer** — urgency timer with localStorage persistence

All behaviors are driven by `data-*` attributes. See [CLAUDE.md](./CLAUDE.md) for the full attribute reference.

---

## npm scripts

| Script | What it does |
|--------|-------------|
| `npm run dev` | Dev server with interactive campaign picker |
| `npm run build` | Build all campaigns to `_site/` |
| `npm run new <slug> <section>` | Scaffold a new section preview campaign |

---

## Related

- [next-campaign-page-kit](https://www.npmjs.com/package/next-campaign-page-kit) — the framework this builds on
- [campaign-cart-starter-templates](https://github.com/NextCommerceCo/campaign-cart-starter-templates) — checkout funnel templates (the downstream consumer of pages composed here)
