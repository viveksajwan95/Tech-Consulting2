# Orium website — deployment

## What to upload

Upload everything in this folder to your web root.

    index.html      the whole site, self-contained (CSS, JS, logo all inlined)
    assets/         logo mark, kept as a separate file for favicons and social cards
    robots.txt      tells crawlers to index the site and where the sitemap is
    sitemap.xml     one entry for the home page
    404.html        optional error page

`index.html` has no external dependencies except two remote resources:

- Google Fonts (Cormorant Garamond, Outfit, JetBrains Mono)
- the hero video, streamed from Pexels

Both load over HTTPS from their own CDNs. Nothing else is fetched.

## Hosting

Any static host works — no server-side runtime, no build step, no database.

- **Netlify / Vercel / Cloudflare Pages** — drag this folder into the dashboard, or connect a repo with this folder as the publish directory.
- **GitHub Pages** — commit the folder contents to the `gh-pages` branch or a `/docs` folder.
- **Traditional hosting (cPanel, S3, nginx, Apache)** — copy the contents into `public_html` / the bucket / the document root.

Serve over HTTPS. Most hosts issue a free certificate automatically.

## Before you go live

1. **Domain** — replace `https://orium.com` in `robots.txt` and `sitemap.xml` with your real domain.
2. **Social preview** — add an `og:image` tag in `<head>`, pointing at a 1200×630 PNG you upload to `assets/`. Without it, links shared on LinkedIn and WhatsApp show no image.
3. **Favicon** — generate icons from `assets/orium-mark.png` and add the usual `<link rel="icon">` tags.
4. **Host the hero video yourself** — the video currently streams from Pexels at 2560×1440. Download it, compress it to roughly 1920×1080 at a few MB, save it as `assets/hero-loop.mp4`, and change the video `src` in `index.html` to `assets/hero-loop.mp4`. The page will load noticeably faster. Credit: Adis Resic, via Pexels.
5. **Search Console** — verify the domain with Google Search Console and submit `sitemap.xml`.
6. **Analytics** — paste your GA4 or Plausible snippet just before `</head>`.

## Editing later

`index.html` is compiled output. To make design changes, edit `Orium v2.dc.html` in the project and export again — editing the compiled file by hand will be overwritten next time.

## What's already handled

- Page title, meta description and keywords
- ProfessionalService and FAQPage structured data (rich results eligible)
- Open Graph title, description and type
- Semantic headings, one `h1`, descriptive `alt` text
- `prefers-reduced-motion` respected across all animation
