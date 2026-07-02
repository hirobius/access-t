# Access Tech — Website

Custom one-page marketing site for **Access Tech** (forestry mulching, fuel reduction &
land improvement — North Idaho & Eastern Washington). Built and maintained by **Hirobius**.

## Stack
- Static **`index.html`** — self-contained (inline CSS + JS), no build step.
- Real assets self-hosted in **`/images`** (logo, photos, social image).
- Hosted on a managed static host (Vercel today; portable to Netlify/Cloudflare Pages).
- Lead form via **Web3Forms** (host-agnostic) → emails `adrian@hirobius.com`.

## Layout note
The file currently ships **two layouts behind a bottom toggle**:
- **Option 1 ("Full")** — the live design (green, full-featured). *This is the one we ship.*
- **Option 2 ("Condensed")** — an alternate; kept for now, to be removed at launch.

Both are green (matched to Phil's logo). Type: Bricolage Grotesque + Hanken (Option 1),
Cabinet Grotesk + Satoshi (Option 2).

## Assets (`/images`)
- `logo-white.png` — header/footer logo (dark backgrounds)
- `logo-color.png` / `logo-icon.png` — full color + icon (light backgrounds / favicon)
- `mulcher-cleared-area.jpg`, `mulcher-at-work.jpg` — hero + owner
- `forest-cleared-*.jpg` — real job photos (gallery candidates)
- `before-after-promo.jpg` — Phil's branded before/after graphic
- `og-image.jpg` — 1200×630 social share image

## Launch checklist
- [ ] Confirm the form delivers (test submit → email lands)
- [ ] Swap real before/after photos into the gallery (currently placeholder, awaiting Phil)
- [ ] Remove the layout toggle (ship Option 1 only)
- [ ] Point the domain `accesstechnw.com` at the site
- [ ] Remove the pre-launch `<meta name="robots" content="noindex,nofollow">`
- [ ] Turn off Vercel Deployment Protection (or host equivalent)
- [ ] Verify `og:image` / structured-data URLs resolve on the live domain
- [ ] Promote to `main` (production)
- [ ] Collect the $1,500 build fee (edits billed case-by-case; no subscription)

## Docs
- `ARCHITECTURE.md` — repo architecture review + target direction
- `BACKLOG.md` — full backend/platform task list (phased)
