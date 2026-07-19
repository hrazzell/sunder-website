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
- The console screenshots in `assets/` are the real `sunder/apps/web` console
  (dark theme) rendered with representative fixture data via mocked API
  responses; the footer discloses this. Regenerate after major console UI
  changes by re-running a similar Playwright harness against `npm run dev`.
- The evidence JSON in the "prove it" section is excerpted from a real bundle
  produced by `sunder/scripts/pilot-happy-path.sh`.
- The "evidence model" section is grounded in the canonical architecture:
  ADR-046/ADR-047 and `sunder/docs/architecture/canonical-sync-implementation-plan.md`
  (merged canonical gates plus pending PR #331). The canonical data plane is
  dormant until the release-wide cutover (`sunder` issue #303), so the section
  says "landing with design-partner pilots" and the trust note discloses this
  explicitly — do not reword it into a shipped claim before the cutover merges.
- The connector grouping mirrors the canonical-v1 producer set from the
  implementation plan (HR CSV/JSON, GitHub, Entra classic certified; other
  sources at varying maturity, moving onto the canonical contract). Update it
  when adapters are certified or the cutover changes the supported set.
- The CLI session, the Slack approval card, and the Data Trust readout are
  illustrative and labeled as such in their captions (Data Trust models the
  pending PR #331 console page; regenerate it as a real screenshot once #331
  merges and the canonical routes go live).
- Pilot stat-strip numbers are the success-criteria targets from the
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
  see/decide/prove acts, evidence model (canonical architecture),
  API/agents + connectors, "what Sunder is not", design-partner program,
  FAQ, final CTA.
- `style.css` — theme tokens are CSS variables at the top (`--accent`, `--bg`,
  …); change those to retheme.
- The apply CTA is a `mailto:` link (three occurrences in `index.html`);
  replace with a form URL (e.g. Tally/Typeform) when one exists.
