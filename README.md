# oversite-website

Source for `https://oversite.com` — the public landing page, DMG download host, and `/welcome` post-install page that the Oversite app's onboarding wizard auto-opens.

This is a static site: 3 HTML pages, one CSS file, no build step, no npm dependencies. Hosted on Vercel; deploys via `git push` to whichever branch is wired to the Vercel project (typically `main`).

## Layout

- `index.html` — `/` landing page
- `extension.html` — `/extension` Chrome extension explainer (linked from the in-app wizard's "Learn more" button)
- `welcome.html` — `/welcome` post-install page (auto-opened by the wizard after Step 6 completes)
- `style.css` — shared CSS (system font stack, monochrome with single accent on the download button)
- `vercel.json` — `/download/Oversite-latest.dmg` redirect to the GitHub Release + security headers
- `sitemap.xml` / `robots.txt` — discovery
- `assets/hero.png` — single static screenshot used on the landing page
- `assets/favicon.ico`, `assets/apple-touch-icon.png` — icons

## Privacy stance

Zero outbound requests from any page. No Google Fonts, no analytics, no third-party CDN. Mirrors the parent project's CLAUDE.md "no telemetry" invariant — the website is the public face of a privacy-first product, and its absence of telemetry advertises that stance.

## Deploying

Wired to Vercel project `oversite-website`. To deploy a change:

```
git push origin main
```

Vercel builds (no-op for static) and deploys automatically. First-time setup:

1. Import this repo into Vercel via the dashboard.
2. Set Framework Preset = "Other".
3. Set Output Directory = `.` (root).
4. Add domain `oversite.com` (apex) and `www.oversite.com` (subdomain). Set the www entry to redirect to apex via the Domains UI dropdown.

## DMG download URL

`https://oversite.com/download/Oversite-latest.dmg` 302-redirects to `https://github.com/ahmedradwan210-gif/oversite-releases/releases/latest/download/Oversite_aarch64.dmg`. The `Oversite_aarch64.dmg` filename is version-stable by maintainer convention — see `PRJCTOVRSITE/RELEASES.md` for the rename-on-upload step that keeps the redirect target valid across releases.
