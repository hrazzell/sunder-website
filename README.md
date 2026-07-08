# sunder-website

Public design-partner landing page for [Sunder](https://github.com/hrazzell/sunder).

Plain static HTML/CSS — no build step, no JavaScript, no external assets
(fonts, scripts, and icons are all local/system), so the page is fast and has
nothing to break.

## Content rules

- Copy is sourced from the approved landing-page/one-pager/FAQ language in
  `sunder-business/zoe-sunder/111_design_partner_launch_assets.md`. Keep claims
  aligned with `sunder-business/product-roadmap.md` ("claims require proof") —
  update this page when connector maturity or pilot claims change.
- The site deliberately targets design-partner recruitment, not broad launch,
  per the roadmap's explicit not-now list.
- The CLI session in the hero is illustrative and labeled as such.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Hosting (GitHub Pages)

This repo started empty, so its default branch is currently
`claude/sunder-website-design-87brgq`. Recommended one-time setup:

1. **Settings → Branches** (or **Settings → General → Default branch**):
   rename the default branch to `main`. GitHub redirects the old name
   automatically.
2. **Settings → Pages** → Source: **Deploy from a branch**; branch `main`
   (or the current default branch if you skip step 1), folder `/ (root)`.
3. The site publishes at `https://hrazzell.github.io/sunder-website/`.

The absolute URLs in `index.html` (`canonical`, `og:url`, `og:image`,
`twitter:image`) assume that Pages URL — update them if you later serve the
site from a custom domain or a different host.

The `.nojekyll` file tells Pages to serve files as-is (no Jekyll build).

Note: GitHub Pages on a **private** repo requires a paid plan; alternatively
make this repo public (it contains only the public marketing page) or host the
same static files on Cloudflare Pages/Netlify for free.

### Custom domain (when ready)

1. Add the domain under **Settings → Pages → Custom domain** (this commits a
   `CNAME` file).
2. At your DNS provider, point the domain at Pages (`CNAME` to
   `hrazzell.github.io` for a subdomain like `www`, or the four Pages A/AAAA
   records for an apex domain).
3. Enable **Enforce HTTPS** once the certificate provisions.

## Editing

- `index.html` — all page content, in section order: hero, problem,
  how-it-works loop, API/agents + connectors, "what Sunder is not",
  design-partner program, FAQ, final CTA.
- `style.css` — theme tokens are CSS variables at the top (`--accent`, `--bg`,
  …); change those to retheme.
- The apply CTA is a `mailto:` link (three occurrences in `index.html`);
  replace with a form URL (e.g. Tally/Typeform) when one exists.
