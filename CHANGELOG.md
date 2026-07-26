# Changelog

All notable changes to the Rooftop / Skyline landing page.

## 2026-07-01

### Fixed
- **Hero background not displaying.** The live deployment had been built with Vercel's
  zero-config pipeline, which compiled the site into serverless functions and never served
  the `/assets/` folder — so `hero-skyline.jpg` and `hero-reveal.mp4` returned **404** and the
  hero fell back to the flat `--sky` blue color. Added `vercel.json`
  (`@vercel/static`, `src: "**/*"`) to force static hosting of every file and redeployed.
  Assets now return **200** on `skyline-omega.vercel.app`.
- **Hero CTA buttons had mismatched heights.** The white "See example issues" button was ~10px
  shorter than the dark "Start writing free" button, because the dark button contains the
  arrow-icon box (28px tall) which made its content taller than the white button's plain text.
  Changed `.hero__cta` from `align-items: center` to `align-items: stretch` so the shorter
  button matches the taller one automatically (no hardcoded height). Verified pixel-identical
  (both 56px border-box, matching top/bottom edges and drop shadow). The `2px` border/stroke is
  identical on both buttons and was not the cause.

### Added
- **Hover micro-interactions on all non-hero sections** (Features, Writers, Pricing, Footer),
  extending the site's existing "brutalist lift" idiom (nudge toward top-left + grow the hard
  offset shadow):
  - Features — cards lift, illustration eases in, corner arrow darts up-right.
  - Writers — feature quote lifts; testimonial rows slide in and their avatar lights up yellow.
  - Pricing — plans lift (featured plan slightly more); check marks rotate-and-pop.
  - Footer — column links slide right; the subscribe box lifts on focus.
  - All new animations are guarded by `@media (prefers-reduced-motion: reduce)`.
- **`.vercelignore`** to stop deploying dev/internal files publicly (`.claude/`, `server.js`,
  `.env.local`, `vercel.json`, `node_modules/`, `design-import/`). Confirmed
  `/.claude/settings.local.json` and `/server.js` now return **404** on the live site.
- **`README.md`** documenting structure, local dev, deploy flow, and deployment gotchas.

### Notes
- Deploys are manual CLI uploads (`vercel --prod`); the repo is not connected to GitHub.
- Production is served from the `skyline-omega.vercel.app` alias; hashed deployment URLs are
  SSO-protected and frozen per build.
