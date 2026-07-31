# devinharold.com — portfolio site

Static single-page portfolio for Devin Harold, deployed on **GitHub Pages** at
https://devinharold.com (canonical) and https://www.devinharold.com (redirects to apex).

Originally designed in Claude Design ("Devin Harold portfolio redesign" project) and
exported/baked into plain static HTML — no build step, no framework, no runtime dependencies.

## Structure

```
index.html                  the whole site (styles inline in <head>, small vanilla JS at the end)
404.html                    styled not-found page
assets/
  *.webp                    portrait (2 sizes) + 6 client logos
  og-image.png              Open Graph / Twitter share image (1200x630)
  fonts/                    self-hosted Merriweather (SIL OFL)
favicon.ico, favicon-32.png, apple-touch-icon.png
CNAME                       custom domain for GitHub Pages (devinharold.com)
.nojekyll                   disables Jekyll processing
robots.txt, sitemap.xml
```

## Fonts

- **Nohemi** (display/text) — loaded from jsDelivr CDN, pinned to `@tamagui/font-nohemi@2.5.1`.
  Nohemi is free for commercial use, but explicit webfont self-hosting rights weren't
  documented, so the CDN reference used by the original design was kept.
- **Merriweather** (body serif) — self-hosted in `assets/fonts/` (SIL Open Font License).

## How to update the site

1. Edit `index.html` directly (everything is in this one file), or re-export from
   Claude Design and re-run the bake process.
2. Commit and push to `main`:
   ```
   git add -A && git commit -m "Describe the change" && git push
   ```
3. GitHub Pages redeploys automatically in ~1 minute (watch the "pages build and
   deployment" workflow in the Actions tab).

## Interactive behavior (vanilla JS at the bottom of index.html)

- Scroll-spy nav highlighting (IntersectionObserver, same tuning as the original design)
- Mobile menu (open/close, Escape, focus trap, body scroll lock)
- Footer copyright year

The "atmosphere" glow treatment from the design's Tweaks panel is baked in as ON.

## DNS (GoDaddy)

- Apex `devinharold.com`: 4 × A records → GitHub Pages IPs, plus AAAA records (IPv6).
  Always use the current IPs from GitHub's docs: "Managing a custom domain for your
  GitHub Pages site".
- `www` CNAME → `<username>.github.io`
- MX/TXT (email) records untouched.
- Rollback: restore the saved pre-cutover zone (see `dns-rollback.txt` in the repo /
  final report) — the old Webflow site remains available until cancelled.
