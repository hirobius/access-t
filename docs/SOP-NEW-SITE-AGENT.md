# SOP — Stand Up a New Client Site (AI Agent)

Audience: an AI coding agent with file read/edit + bash + git access.
Goal: produce a new, launch-ready client site from the Access Tech reference build
(`/home/user/access-tech/index.html`) — one static `index.html`, inline CSS+JS, self-hosted
images, working Web3Forms lead form, correct SEO, deployed to Vercel.

This is a **template-by-copy** workflow: the reference build is a single static file driven by
CSS custom properties (design tokens). Re-theming a client ≈ swapping token values + logo +
photos + copy + SEO fields + the Web3Forms key. Do not introduce a build step, a framework, or
external runtime dependencies. Keep it one self-contained `index.html` + `/images`.

Follow the steps in order. Do not skip the QA gate before launch. Do not commit or push unless
explicitly told to in the step.

---

## 0. Inputs to collect / confirm before editing

Refuse to scaffold until you have these. If any are missing, list exactly what is missing and stop.

**Business identity**
- `BUSINESS_NAME` (e.g. "Summit Tree Care")
- `TAGLINE` / one-line value prop
- `SERVICE_LIST` (6–9 services with a one-sentence description each)
- `SERVICE_AREA` (regions/cities, e.g. "North Idaho & Eastern Washington")
- `CREDENTIALS` / trust points (licenses, degrees, "free estimates", "X years", etc.)
- Phone number(s) with state/label, and the destination **lead email**

**Brand / design**
- Logo files: transparent PNG. Need a **white/knockout** version for the dark header/footer
  and a **full-color** version for light backgrounds + a square **icon** for the favicon.
- Brand palette (hex). Map to the token set in §3.
- Photos: hero, owner/equipment, 3+ before/after pairs (or single job photos), any gallery shots.

**Infra**
- `PROD_DOMAIN` (registered in the **client's** name — confirm, do not assume)
- Web3Forms access key generated against the **client's lead email** (see §5). One key per site.
- Confirm host = Vercel (git-connected). Note portability to Netlify/Cloudflare Pages if asked.

Record these in a short config block in your working notes so later steps are mechanical.

---

## 1. Scaffold the new site (copy the template)

The reference build is the source of truth. Copy the whole repo skeleton, not just `index.html`.

```bash
SRC=/home/user/access-tech
DEST=/home/user/<client-slug>          # e.g. /home/user/summit-tree
mkdir -p "$DEST/images" "$DEST/docs"
cp "$SRC/index.html" "$DEST/index.html"
cp "$SRC/README.md" "$DEST/README.md"            # then rewrite for the new client
# Do NOT copy Access Tech's photos/logos; bring the client's own assets into $DEST/images
cd "$DEST" && git init -q
```

Notes:
- Use a lowercase, hyphenated client slug for the directory and (later) the Vercel project name.
- Keep `ARCHITECTURE.md` / `BACKLOG.md` as Hirobius-internal references; they are *not* per-client
  deliverables — do not copy them into the client repo unless asked.

---

## 2. Strip the reference build down to a single layout

The reference `index.html` ships **two layouts** (`#layout-one` orange, `#layout-two` green) behind
a bottom toggle. A client site must ship exactly one. Default to **Option 1 (`#layout-one`)** unless
the brand explicitly suits the condensed green design better.

Remove, in `index.html`:
1. The entire `<div id="layout-two"> … </div>` block (the `#layout-two` opening through
   `</div><!-- /#layout-two -->`).
2. The toggle widget: `<div class="vtoggle" …> … </div>` (after the layouts).
3. The toggle JS in `<script>`: the block under `/* ---- Layout toggle (Option 1 / Option 2) ---- */`
   (the `KEY`, `tBtns`, `setLayout`, `saved`, and its event listeners).
4. The Option-2-only CSS: the `OPTION TWO` style section (the `#layout-two` rules,
   `.v2-*` classes, `--leaf*`/`--mint*` token block if Option 2 is dropped) and the
   `#layout-two{display:none}` / `body.show-v2 …` layout-switching rules.
5. The Option-2 font pair `<link>`s in `<head>` (Fontshare: Cabinet Grotesk + Satoshi) plus the
   `api.fontshare.com` / `cdn.fontshare.com` preconnects. Keep only the kept layout's fonts
   (Option 1 = Bricolage Grotesque + Hanken Grotesk via `fonts.googleapis.com`).
6. The `loremflickr.com` / `live.staticflickr.com` preconnect + dns-prefetch `<link>`s — these
   only existed for placeholder stock and must be gone once images are self-hosted (§4).

Sanity-check after stripping: search the file and confirm **zero** matches for `loremflickr`,
`v2-`, `layout-two`, `show-v2`, `vtoggle`, `fontshare`. The scroll-reveal IntersectionObserver and
the mobile-nav burger JS must remain. The Web3Forms submit JS must remain.

---

## 3. Re-theme via design tokens (`:root` in `<style>`)

All palette/spacing/type live as CSS custom properties in `:root` (around lines 62–87 of the
reference). Re-theme by editing **values only** — never rename tokens, since every rule references
them. Key tokens for Option 1:

- Accent / CTA color (the brand's primary): `--ember` (default `#2f8f4e`), with
  `--ember-dark` (hover) and `--ember-soft` (light-on-dark accent). These drive buttons, links,
  eyebrows, focus rings, badges.
- Dark surfaces (header/footer/dark sections): `--pine-950 / -900 / -800 / -700` and `--forest-600`.
- Light surfaces / paper: `--bone`, `--bone-200`, `--kraft`.
- Ink / text: `--ink`, `--ink-soft`, `--bark`.
- Muted accent text on dark: `--moss-300`, `--moss-500`.
- Fonts: `--font-display` (Bricolage Grotesque) and `--font-sans` (Hanken Grotesk). If you change
  fonts, also update the Google Fonts `<link>` in `<head>` to match.
- Spacing scale `--s1..--s7`, `--section-y`, `--maxw`, `--radius*` — leave as-is unless the brand
  needs tighter/looser rhythm.

Re-theming rule of thumb: set `--ember`/`--ember-dark`/`--ember-soft` to the brand accent and pick
the dark-green/neutral `--pine-*` family to match the brand's dark tone. Verify contrast (accent
text on dark and on light must remain readable).

---

## 4. Add + optimize images (self-host in `/images`)

Never hot-link third-party images. Put every image in `$DEST/images` and reference it as
`/images/<file>.jpg`. Optimize with Python Pillow before committing.

**Targets**
- Hero / full-bleed photos: long edge ~1600–1920px, JPEG quality 82.
- In-content photos (about, gallery): ~1200–1600px long edge, JPEG q82.
- Logos: transparent **PNG** — one full-color, one white/knockout for dark header/footer, one square
  icon (favicon). Do not JPEG a logo (kills transparency).
- Social share: one `og-image.jpg` at exactly **1200×630**.

**Pillow recipe** (run with the client's source files in a `raw/` folder):

```bash
pip install pillow >/dev/null 2>&1
python3 - <<'PY'
from PIL import Image, ImageOps
import pathlib, sys

OUT = pathlib.Path("images"); OUT.mkdir(exist_ok=True)

def jpeg(src, dst, long_edge=1600, q=82):
    im = ImageOps.exif_transpose(Image.open(src)).convert("RGB")
    w, h = im.size
    if max(w, h) > long_edge:
        s = long_edge / max(w, h)
        im = im.resize((round(w*s), round(h*s)), Image.LANCZOS)
    im.save(dst, "JPEG", quality=q, optimize=True, progressive=True)
    print(dst, im.size)

def og(src, dst="images/og-image.jpg"):
    # cover-crop to 1200x630
    im = ImageOps.exif_transpose(Image.open(src)).convert("RGB")
    im = ImageOps.fit(im, (1200, 630), Image.LANCZOS)
    im.save(dst, "JPEG", quality=82, optimize=True)
    print(dst, im.size)

def logo(src, dst, max_w=480):
    # keep transparency; output PNG
    im = ImageOps.exif_transpose(Image.open(src)).convert("RGBA")
    if im.width > max_w:
        s = max_w / im.width
        im = im.resize((max_w, round(im.height*s)), Image.LANCZOS)
    im.save(dst, "PNG", optimize=True)
    print(dst, im.size)

# --- edit the calls below for this client's actual files ---
jpeg("raw/hero.jpg",  "images/hero.jpg", 1920, 82)
jpeg("raw/owner.jpg", "images/owner.jpg", 1400, 82)
og("raw/hero.jpg")                              # or a dedicated branded share image
logo("raw/logo-color.png", "images/logo-color.png")
logo("raw/logo-white.png", "images/logo-white.png")   # white knockout for dark header
logo("raw/logo-icon.png",  "images/logo-icon.png", 128)
PY
```

White knockout: if the client only supplies a color logo, generate a white version (recolor opaque
pixels to white while preserving alpha) for the dark header/footer. Verify it reads on `--pine-950`.

**Wire the images into `index.html`** (these paths exist in the reference — repoint them):
- Favicon: `<link rel="icon" … href="/images/logo-icon.png">`
- Header + footer logo: `<img class="brand-logo" src="/images/logo-white.png" …>` (alt = business name)
- Hero background: `.hero-bg .ph` `background:url("/images/<hero>.jpg")` and the
  `<video … poster="/images/<hero>.jpg">`
- About visual: `.about-visual .ph` `background:…url("/images/<owner>.jpg")`
- Before/after + gallery: replace each placeholder `.ph.before` / `.ph.after` background and the
  `.ph-sub` caption text with real photos. Prefer real `<img>` over CSS backgrounds where you add
  new gallery items so they get `alt` text.
- `og:image`, `twitter:image`, and JSON-LD `image`/`logo` must point to absolute
  `https://<PROD_DOMAIN>/images/...` URLs (§6).

---

## 5. Wire the lead form (Web3Forms — one key per site)

The form posts to `https://api.web3forms.com/submit` and is AJAX-handled in the closing `<script>`
(`#estimate-form` → inline success/error). Do **not** rewrite the JS; just set the hidden fields.

1. Generate a **new** free access key at https://web3forms.com using the **client's lead email** as
   the destination. Each site MUST have its own key — never reuse Access Tech's
   `31719ab4-ebe8-484a-88bc-ed84acbc8b89`.
2. In the `<form id="estimate-form">`, set the hidden inputs:
   - `<input type="hidden" name="access_key" value="<CLIENT_KEY>">`
   - `<input type="hidden" name="subject" value="New estimate request — <BUSINESS_NAME> website">`
   - `<input type="hidden" name="from_name" value="<BUSINESS_NAME> Website">`
3. Keep the honeypot `<input type="checkbox" name="botcheck" … style="display:none">`.
4. Keep field `name` attributes (`name`, `phone`, `email`, `address`, `acreage`, `message`,
   `attachment`) — Web3Forms emails these. Adjust labels/fields to the client's trade (e.g. swap
   "Approximate Acreage" for a relevant select) but every input must keep a `name`.
5. The success copy is set in JS (`#estimate-status`); update the business-specific wording if needed.

You will test actual delivery in QA (§8).

---

## 6. SEO / metadata / structured data (`<head>`)

Edit every one of these for the new client. Do not leave Access Tech strings anywhere.

- `<title>` — `<BUSINESS_NAME> — <Primary Service> | <SERVICE_AREA>`
- `<meta name="description">` — 150–160 chars, services + area + a hook (e.g. "free estimates").
- Open Graph: `og:title`, `og:description`, `og:type` (website), `og:image`
  (`https://<PROD_DOMAIN>/images/og-image.jpg`).
- Twitter: `twitter:card` (summary_large_image), `twitter:title`, `twitter:description`,
  `twitter:image`.
- JSON-LD `<script type="application/ld+json">` `LocalBusiness`: update `name`, `description`,
  `url` (`https://<PROD_DOMAIN>`), `logo`, `image`, `telephone`, `areaServed`, `knowsAbout`
  (the service list), and the `contactPoint[]` array (one per phone/region). Validate it is parseable
  JSON.
- **Leave the pre-launch guard in place during build:**
  `<meta name="robots" content="noindex,nofollow">`. It is removed only at launch (§9).

Also update all visible copy/text: nav labels, hero, about, services cards, before/after captions,
why-us, service-area tags, phone-card numbers (and `tel:` hrefs), final CTA, footer columns, and the
`© <year> <BUSINESS_NAME>` line.

---

## 7. Preview deploy (Vercel)

```bash
cd "$DEST"
git add -A && git commit -q -m "Initial <BUSINESS_NAME> site from Hirobius template"
# Create/link the Vercel project (git-connected auto-deploy). Static — no build command, output = repo root.
```

- Push to a non-production branch so Vercel produces a **preview** deployment (production = `main`,
  promoted only at launch).
- Preview deploys are gated by **Vercel Deployment Protection** — the preview URL requires a logged-in
  viewer or a **bypass link**. Generate the bypass/share link to send for review; do not disable
  protection yet.
- Confirm the deploy succeeded and the preview renders before QA.

---

## 8. QA gate (must pass before launch)

Do not proceed to launch until all pass. Report any failure instead of launching.

**Responsive** — check at widths 1280, 901, 900, 680, 420, and ~360px. Breakpoints in the build are
`900px`, `680px`, `420px`. Verify: nav collapses to the burger overlay ≤680px; service/gallery grids
reflow; hero text stays readable over the photo; no horizontal scroll (`overflow-x` is hidden but
check anyway).

**Links & nav** — every in-page anchor (`#about #services #gallery #why #area #estimate #top`)
scrolls correctly; all `tel:` links use the client's real numbers; footer external link points to
`https://<PROD_DOMAIN>`; burger opens/closes and closes on link click.

**Form** — submit a real test entry; confirm the success state renders inline AND the email lands in
the **client's** inbox. Confirm the honeypot field is hidden. Confirm the failure path (e.g. block
network) shows the inline error copy.

**Images** — all `/images/...` resolve (no 404s, no leftover placeholders, no `loremflickr`); logo
shows correctly on the dark header/footer; favicon loads; `og:image` is 1200×630.

**Console / network** — open DevTools: zero console errors, zero failed requests. Confirm fonts load.

**SEO** — `noindex` STILL present (pre-launch); `<title>`/description correct; JSON-LD validates;
OG/Twitter/JSON-LD image+url use the production domain.

---

## 9. Launch

Only after the QA gate passes and the client has approved the preview.

1. **Domain** — confirm `PROD_DOMAIN` is registered in the **client's** name; add it as a custom
   domain on the Vercel project; set DNS records as Vercel instructs; wait for SSL to provision.
2. **Remove the noindex guard** — delete `<meta name="robots" content="noindex,nofollow">` from
   `<head>` (and its `PRE-LAUNCH` comment).
3. **Turn off Vercel Deployment Protection** for production so the live site is publicly viewable
   without a bypass link.
4. **Promote to production** — merge/push the reviewed branch to `main`; confirm Vercel deploys
   `main` to the production domain.
5. **Verify live** — load `https://<PROD_DOMAIN>`: confirm SSL padlock, no `noindex`, all
   `/images/...` and JSON-LD/OG URLs resolve on the real domain, and run one more live form test to
   the client's inbox.

---

## 10. Hand back to the human (Adrian)

Return a concise report containing:
- Client repo path + Vercel project name + production domain.
- Preview URL (with bypass link) and live URL.
- Confirmation: single layout shipped, images self-hosted/optimized, form tested end-to-end (with the
  test email screenshot/landing confirmation), noindex removed, protection off, on `main`.
- The Web3Forms access key used (note it routes to the client's lead email) for the password vault.
- Any open items requiring a human (e.g. awaiting real before/after photos, domain transfer in the
  client's name, billing: $1,500 upfront build fee; edits billed case-by-case — invoice status).
- Anything you could not verify and why.

Do not start Stripe billing or transfer domain ownership yourself — flag these for Adrian.
