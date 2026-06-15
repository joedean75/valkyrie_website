# Corvus Industries — Marketing Website

A self-contained static marketing site for **Corvus Industries** (products: **Muninn**, civil; and
**Huginn**, defense), in a dark, mission-first register modeled on defense-tech leaders (Anduril,
Shield AI) — adapted for a **dual-use** company that leads with the civil/SAR mission near-term and
the defense thrust long-term.

## Files
| File | Purpose |
|------|---------|
| `index.html` | Single-page site (hero, mission, platform, capabilities, dual mission, compliance, company, contact) |
| `styles.css` | Design system — dark theme, "Corvus gold" accent, responsive, reduced-motion aware |
| `main.js` | Vanilla JS — sticky nav, mobile menu, scroll reveal, stat counters, cursor-tracking hero glow (no dependencies) |
| `netlify.toml` | Zero-build host config + security/cache headers (for the dedicated repo) |

No build step and no trackers. Fonts load from Google Fonts (Space Grotesk / Inter / JetBrains Mono)
with system-font fallbacks, so it degrades gracefully offline. Deploys anywhere static.

## Preview locally
```bash
cd website
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy

### Recommended: dedicated public repo + Netlify/Cloudflare (keeps `valkyrie` private)
The `valkyrie` repo is **private** (holds business/defense docs), and GitHub Pages from a private repo
needs a paid plan. So publish the site from its **own public repo** — these files are civil/EAR-safe
public marketing, safe to be public. A `netlify.toml` is included here (security headers + zero-build
config), so once the repo exists, Netlify/Cloudflare is a 2-click connect.

**1) Stand up the repo (run on your machine, from a `valkyrie` checkout):**
```bash
cd website
git init -b main
git add .
git commit -m "Corvus Industries marketing site"
# with GitHub CLI:
gh repo create auriga-website --public --source=. --remote=origin --push
# …or create 'auriga-website' in the GitHub UI, then:
# git remote add origin https://github.com/joedean75/auriga-website.git && git push -u origin main
```

**2) Connect a host (free, deploys on every push):**
- **Netlify:** Add new site → Import from Git → pick `auriga-website` → build command *(none)*, publish dir `.` → Deploy. (`netlify.toml` already sets this.)
- **Cloudflare Pages:** Create application → Pages → Connect to Git → `auriga-website` → Framework preset *None*, build output dir `/` → Save & Deploy.
- **GitHub Pages (now also free, since this repo is public):** Settings → Pages → Source: *Deploy from a branch* → `main` / root.

*Custom domain later:* add it in the host's dashboard (Netlify/Cloudflare), or a `CNAME` file for Pages.

### Alternative: GitHub Pages from `valkyrie` (needs paid plan)
A workflow is included in the parent repo at `.github/workflows/deploy-pages.yml` (Settings → Pages →
Source: "GitHub Actions"). This only publishes if `valkyrie` is on a plan that allows Pages from a
**private** repo — otherwise use the dedicated-repo route above.

## Customize before publishing
- **Imagery:** the platform art is a lightweight inline SVG placeholder. Swap in a real render/photo
  once hardware exists (keep file sizes small; add `loading="lazy"`).
- **Domain + email:** update the `mailto:` and contact (currently `CorvusIndustries@outlook.com`) once
  a branded domain/email is set up.
- **Analytics:** none included by design; add privacy-respecting analytics if desired.
- **Open Graph image:** add an `og:image` once you have artwork (improves link previews).

## ⚠️ Content & compliance guardrails (read before going live)
- **Export control:** this is the **civil / EAR-safe** public face. Keep messaging at the mission level
  for defense (ISR, persistent surveillance). **Do not** publish ITAR-sensitive specs, performance
  envelopes for restricted use, or anything that pre-empts a commodity-jurisdiction determination
  (`valkyrie/01_Business_Plan.md` §7.2).
- **No overclaiming:** the platform is **software-validated in simulation, pre-hardware.** The site
  says "built and validated in simulation" — keep it that way until flight test. Don't imply a fielded
  or flying aircraft.
- **Spec accuracy:** figures (endurance, AO, etc.) mirror `valkyrie/08_Spec_Sheet_COMMERCIAL.md` — keep
  them in sync and labeled as targets where appropriate.
- **Safety claim:** the "sensing only, no weaponization" line is load-bearing — keep it on the page.

See [`../valkyrie/Marketing_Campaign.md`](../valkyrie/Marketing_Campaign.md) for positioning, messaging
pillars, audiences, channels, and the launch plan this site anchors.
