# Foxxy Studio Landing Page

Production-ready Vite + React port of the Foxxy Studio landing page, ready to deploy to Vercel.

## Local development

```bash
npm install
npm run dev
```

Opens at `http://localhost:5173`.

## Build

```bash
npm run build      # outputs to dist/
npm run preview    # preview production build
```

## Deploy to Vercel

### Option 1 — Vercel CLI (fastest)

```bash
npm install -g vercel
vercel              # follow prompts; deploys a preview
vercel --prod       # promote to production
```

### Option 2 — Git integration

1. Push this folder to a Git repo (GitHub / GitLab / Bitbucket).
2. In Vercel dashboard → **Add New → Project** → import the repo.
3. Vercel auto-detects Vite; just hit **Deploy**. No env vars needed.

The included `vercel.json` rewrites all routes to `/index.html` so client-side hash anchors (#work, #pricing, #book, etc.) work on any path.

## File layout

```
vercel-app/
├── index.html              # Vite entry (Google Fonts preload + #root)
├── package.json
├── vite.config.js
├── vercel.json             # Vercel build config + SPA rewrites
└── src/
    ├── main.jsx            # React DOM root
    ├── App.jsx             # Section composition + Tweaks panel
    ├── styles.css          # All design styles (copied 1:1 from source)
    ├── assets/             # Work images + Clutch logo (imported by components)
    ├── hooks/
    │   ├── useReveal.js    # IntersectionObserver scroll-reveal
    │   └── useGoldShimmer.js  # Gold shimmer text effect
    ├── tweaks/
    │   ├── useTweaks.js    # Tweak state hook
    │   └── TweaksPanel.jsx # Floating settings panel + controls
    └── components/         # One file per section (Hero, Pricing, FAQ, etc.)
```

## Notes

- All design CSS lives in `src/styles.css` and is imported by `main.jsx`. The design is byte-for-byte identical to the source.
- Image assets are imported as ES modules so Vite hashes and fingerprints them in production.
- The Tweaks panel (palette + pricing) now persists per-session in React state. The host postMessage protocol used by the design environment was stripped — this is a normal web app, not an embedded design preview.
- To wire up the real Calendly embed, find the `// ── Calendly embed slot` comment in `src/components/BookCall.jsx` and replace the placeholder `<div className="embed-placeholder">…</div>` block.

## Custom domain

After deploy, add your domain in Vercel → Project → Settings → Domains. Vercel handles SSL automatically.
