# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a static personal portfolio website for Brian Davis (Senior Data Engineer & Solution Architect), hosted on GitHub Pages at `bdavis9725.github.io`. It is based on the KREO template by Styleshout (CC Attribution 3.0 license). There is no build system, package manager, or test suite — all files are served directly.

## Development

**Preview locally** by opening any HTML file directly in a browser, or serving with any static file server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

There are no build, lint, or compile steps.

## Site Structure

The site has three pages:

- `index.html` — main page with hero slider, About Me, and Architectural Highlights sections
- `cv.html` — resume/CV page with its own standalone stylesheet (`css/cv.css`)
- `portfolio.html` — placeholder page (currently "in progress")

### CSS Architecture

All pages except `cv.html` share three stylesheets loaded in order:

1. `css/base.css` — grid system and foundational layout
2. `css/vendor.min.css` — third-party plugin styles (FlexSlider, Magnific Popup, etc.)
3. `css/main.css` — all site-specific styles, organized by section (header, hero, services, about, footer, etc.). This is the primary file to edit for visual changes.

`cv.html` loads only `css/cv.css`, which is fully self-contained.

Fonts are self-hosted (Raleway, Merriweather) in `fonts/` and referenced via `css/fonts.css`, which is imported at the top of `main.css`. Font Awesome icons are at `css/font-awesome/`.

### JavaScript

`js/main.js` is the only custom JS file. It initialises all interactive behavior on `$(window).load`:

- **Preloader** — fades out `#loader` then `#preloader`
- **FlexSlider** — hero carousel on `#hero-slider` (fade animation, 7 s interval)
- **Waypoints** — highlights the active nav item as sections scroll into view
- **FitText** — scales `#hero-slider h1` responsively
- **Mobile menu** — replaces static anchor mobile buttons with a dynamic toggle
- **Smooth scroll** — animates scrolling for all `.smoothscroll` links
- **Magnific Popup** — modal handler for `.item-wrap a` (used in portfolio)
- **Contact form** — validates `#contactForm` with jQuery Validate and POSTs via AJAX to `inc/sendEmail.php`

All vendor JS lives in `js/` as pre-minified files (jQuery 1.11.3, FlexSlider, Waypoints, Validate, FitText, Placeholder, Magnific Popup, Modernizr).

### Contact Form

`inc/sendEmail.php` handles the contact form server-side. **This does not execute on GitHub Pages** (which only serves static files), so the contact form is currently non-functional in production. If deploying to a PHP-capable host, update `$siteOwnersEmail` in that file.

## Key Conventions

- Navigation on `index.html` uses `href="#section-id"` anchor links with `.smoothscroll` for in-page scrolling; links to other pages (`portfolio.html`, `cv.html`) are standard hrefs.
- Google Analytics (ID: `G-MB4XT6ZJV4`) is included inline in the `<head>` of all three HTML pages.
- The KREO template license requires a credit link to `styleshout.com` to remain in the site footer (or a $10 removal fee paid).
- `portfolio.html` social links are commented out — uncomment and populate when the page is built out.
