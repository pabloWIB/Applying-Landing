# Applyiing

A single-screen typographic piece built around one argument: knowledge only counts once it is applied.

## Description

One page, one statement, one link. There is no product to sell, no form to fill and no navigation to follow, so the whole design problem is typographic: set the argument so it reads, and give it a single graphic idea to sit in.

That graphic idea is a ring of seven hairline circles drawn entirely in CSS. Six of them drift inward toward a still centre over a fourteen-second cycle and drift back out, which is where the piece gets its only movement. There are no images in the project — the ring, the favicon and the arrow in the button are all vector marks generated in the source.

The page ships **no JavaScript at all**. Layout, animation, focus handling, responsive behaviour and reduced-motion support are all CSS. Nothing is requested from a third-party origin: the two typefaces are served from this repository, and there is no analytics, no CDN and no tracking of any kind.

## Tech stack

| Layer | Technology | Detail |
|---|---|---|
| Markup | HTML5 | Two static pages, `index.html` and `404.html` |
| Styling | CSS3 | Custom properties, CSS Grid, `clamp()` fluid type, three files |
| Display type | Cinzel | Variable font, weight axis 400–900, one file |
| Script type | Dancing Script | Regular, used for the wordmark only |
| Body type | System UI stack | No download; Cinzel has no true lowercase and is unfit for running text |
| Scripting | None | The project contains no JavaScript files |
| Build | None | No bundler, no preprocessor, no `package.json` |

## Measurements

Verified on a local HTTP server and by opening the files directly.

| Metric | Value |
|---|---|
| First-load weight | 217 KB, of which 201 KB is the two fonts |
| HTTP requests on first load | 7 — the page, three stylesheets, two fonts, one icon |
| JavaScript shipped | 0 bytes |
| Third-party requests | 0 |
| Console errors and warnings | 0 on both pages |
| Text contrast | 21:1 primary, 8.63:1 secondary |
| Horizontal overflow | None at 360, 480, 768, 1024 or 1440 px |
| Minimum touch target | 44 px on every standalone control |

## Project structure

```
.
├── index.html                       # The piece: statement, argument, one link
├── 404.html                         # Same shell, returns to the home page
├── robots.txt                       # Allows everything, points at the sitemap
├── sitemap.xml                      # One URL — the site is one page
├── .gitignore
├── assets/
│   ├── css/
│   │   ├── base.css                 # Custom properties, reset, typography, utilities
│   │   ├── layout.css               # Page grid, header, hero, footer, media queries
│   │   └── components.css           # The animated ring, buttons, links, 404 block
│   ├── fonts/
│   │   ├── cinzel-variable.ttf      # Display face, weight axis 400–900
│   │   ├── dancing-script-regular.ttf   # Wordmark
│   │   └── ofl.txt                  # SIL Open Font License, covers both families
│   └── img/
│       └── favicon.svg              # Hand-written SVG, 284 bytes
└── docs/
    ├── auditoria.md                 # Inventory and findings before the rewrite
    └── cambios.md                   # What changed, grouped by phase
```

## Running it locally

The project is static and has no dependencies, so opening the file works:

```bash
open index.html
```

To serve it over HTTP instead — which is how the fonts and the canonical URL behave in production:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`. Any static server does the same job; nothing needs to be installed or built first.

## Customising the type

Both `@font-face` rules live at the top of `assets/css/base.css`. Cinzel is supplied as a variable font, so the whole 400–900 range comes from one file and one request:

```css
@font-face {
  font-family: "Cinzel";
  src: url("../fonts/cinzel-variable.ttf") format("truetype-variations");
  font-weight: 400 900;
  font-display: swap;
}
```

Colour, spacing, type scale and motion are all declared as custom properties in the `:root` block of the same file. Changing the palette or the spacing rhythm means editing that block and nothing else.

## Accessibility

- One `<h1>` per page and a heading order with no skipped levels.
- A skip link as the first focusable element.
- A visible focus ring on every interactive element, set globally through `:focus-visible`.
- Contrast measured at 21:1 for primary text and 8.63:1 for secondary, against a 4.5:1 requirement.
- Pinch zoom left enabled; the viewport meta sets no scale limits.
- `prefers-reduced-motion` stops the ring animation.
- Standalone controls are at least 44 px on their short edge.

## Fonts and licensing

Cinzel and Dancing Script are both licensed under the SIL Open Font License. `assets/fonts/ofl.txt` is the licence text as distributed and must travel with the font files if they are redistributed.

## Deployment

Deployed as a static site at [applyiing.wib.digital](https://applyiing.wib.digital). There is no build step: upload the repository root as-is, with no build command and no output directory. Point the host's 404 handler at `404.html`.

If the site is served from a different domain, three values need updating: the `<link rel="canonical">` and `og:url` tags in `index.html`, and the `Sitemap:` line in `robots.txt` together with the `<loc>` in `sitemap.xml`.

## Author

**Pablo Nieto Pérez** — [wib.digital](https://wib.digital)
GitHub: [@pabloWIB](https://github.com/pabloWIB)

## Hire me

I build **custom internal tools, CRMs and dashboards** for small teams, and
**conversion-focused websites** for businesses.

- [Custom internal tool, CRM or dashboard](https://www.fiverr.com/pablonietop/build-a-custom-internal-app-for-your-business) — from $45
- [Conversion-focused website](https://www.fiverr.com/pablonietop/convert-your-landing-page-design-to-code) — from $80
- [All my services on Fiverr](https://www.fiverr.com/pablonietop)
- [wib.digital](https://wib.digital)
