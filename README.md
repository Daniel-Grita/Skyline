# Rooftop — Skyline Landing Page

A single-page marketing site for **Rooftop**, a distraction-free newsletter platform.
Pixel/retro art direction with a cinematic intro reveal over a city-skyline hero.

**Live:** https://skyline-omega.vercel.app

## Structure

```
index.html          Entire site — markup, inline CSS, and inline JS in one file
assets/
  hero-skyline.jpg  Static hero background (also the video poster / fallback)
  hero-reveal.mp4   Intro reveal video that plays once, then fades to the still
server.js           Tiny static file server for local dev (port 8123)
vercel.json         Forces Vercel to serve everything as static files
.vercelignore       Keeps dev-only files out of the deployed build
```

## Run locally

```bash
node server.js
# → http://localhost:8123
```

`server.js` is a dependency-free static server (no `npm install` needed). It is **local-only**
and is excluded from deploys via `.vercelignore`.

## Deploy

Deploys go to Vercel via **CLI upload** (this repo is not connected to GitHub, so `git push`
alone does **not** update the site):

```bash
vercel --prod        # build + promote to production
```

### Deployment notes / gotchas

- **Use the alias, not the hash URL.** Share and test on **`skyline-omega.vercel.app`**.
  Hashed deployment URLs (e.g. `skyline-<hash>-danielgrita-projects.vercel.app`) are frozen
  snapshots of a single build *and* are gated behind Vercel Authentication (they 302 to SSO) —
  they never update and aren't publicly viewable.
- **`vercel.json` matters.** Without it, Vercel's zero-config build turned the site into
  serverless functions and never served `/assets/`, so the hero background 404'd. The
  `@vercel/static` build forces plain static hosting of every file.
- **`.vercelignore`** prevents dev/internal files (`.claude/`, `server.js`, `.env.local`,
  `vercel.json`, etc.) from being published to the public site.

## Accessibility

All motion (intro reveal + section hover animations) is wrapped in
`@media (prefers-reduced-motion: reduce)` and falls back to a static layout.
