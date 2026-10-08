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
- Positioning (2026-10-08): identity governance for agent-first companies,
  led by "who owns each AI agent, what it can actually reach, and proof that a
  human approved it". Only list a connector or feature under "Available
  today" once it ships; everything else goes in the "On the roadmap" group.
- The site deliberately targets design-partner recruitment, not broad launch,
  per the roadmap's explicit not-now list.
- The console screenshots in `assets/` (`console-overview.webp`,
  `console-findings.webp`, `console-inbox.webp`) are real captures of the
  current `sunder/apps/web` Console (dark theme, 1280x788 at 2x, resized to
  2200px wide), running against a local `sunder-api` on PostgreSQL seeded
  through the API with the synthetic Northstar fixtures (HR import, the mock
  GitHub and Entra providers, a leaver, and one access review). Home and My
  work are shown as reviewer Priya Shah, Findings as administrator Elena
  García. The footer discloses that they show fixture data. Regenerate after
  major Console UI changes the same way.
- The evidence JSON in the "prove it" section is an illustrative excerpt in
  the current sealed campaign evidence format (`campaign.json`, see
  `sunder/src/campaign_evidence_rendition.rs`) with synthetic values, and is
  labelled as such.
- The `sunderctl` session is a real run of `sunder/scripts/sunderctl` against
  the same synthetic Northstar lab, with IDs shortened and output trimmed.
- The Slack approval card is illustrative and labelled as roadmap.
- `og-image.png` (1200x630) is rendered from a simple HTML card with
  Playwright using the page headline and the `style.css` colours.
- Pilot stat-strip numbers are target success criteria, agreed per pilot, from the
  design-partner launch assets — keep them in sync with that doc.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Hosting (GitHub Pages)

One-time setup:

1. **Settings → General → Default branch**: switch the default branch to
   `main` (the repo started empty, so the first pushed feature branch became
   the default).
2. **Settings → Pages** → Source: **Deploy from a branch**; branch `main`,
   folder `/ (root)`.
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
