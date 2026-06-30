# Backend / Platform Backlog — Hirobius

Every core moving piece behind the sites, grouped by domain. Phased so we don't over-build:

- **Phase 0 — Now:** finish Access Tech + the minimum to launch & bill one client.
- **Phase 1 — Next (at 2–3 clients):** templatize + the repeatable production pipeline.
- **Phase 2 — Later (only if/when justified):** CMS/auth, fleet tooling, AI engine.

Status key: ☐ todo · ◐ in progress · ✓ done · ⏸ deferred

---

## 0. Site finishing — Access Tech (Phase 0)
- ☐ Strip to **orange-only** (remove green layout, toggle, dead CSS/JS)
- ☐ Self-host + optimize images (replace the 14 LoremFlickr hot-links)
- ☐ Wire the lead form to a real handler (see Forms)
- ☐ Drop the unused font pair; keep Bricolage + Hanken
- ☐ SEO: `LocalBusiness` JSON-LD, `sitemap.xml`, `robots.txt`, canonical
- ☐ Accessibility pass (`alt` text, focus states, contrast)
- ☐ Fill in `README`
- ☐ Remove `noindex` at launch
- ☐ Land finished site on `main`

## 1. Forms / lead capture (Phase 0)
- ☐ Pick a **host-agnostic** service: **Web3Forms** or **Formspree** (works on any host)
- ☐ Add field `name`s, honeypot, and the service's spam/captcha
- ☐ Route submissions → client's lead email; add a success state/page
- ☐ Decision: do we also store submissions (e.g., a sheet/DB) or email-only? (email-only for now)
- ☐ Standardize a reusable form snippet for the template

## 2. Hosting / deploy (Phase 0 → 1)
- ☐ Choose host: **Cloudflare Pages** (unlimited/free) or **Netlify** / **Vercel**
- ☐ Git-connected auto-deploy (push → build → live)
- ☐ Production vs preview environments; SSL (automatic)
- ☐ Phase 1: per-client projects vs single multi-tenant app — decide at volume
- ☐ Phase 1: build pipeline if/when we adopt an SSG (Astro)

## 3. Domains / DNS (Phase 0)
- ☐ Standard registrar: **Cloudflare** (at-cost domains, central DNS)
- ☐ Register each client domain **in the client's name** (they own it)
- ☐ Track renewal dates (in the client tracker) + reminders
- ☐ Phase 1: `previews.hirobius.com` wildcard for spec-site previews

## 4. Auth (Phase 1 / 2 — only if needed)
- ☐ Decision: needed only for (a) a client-editing CMS, or (b) gating previews
- ☐ Preview gating: `noindex` + obscure URL now; basic-auth / Cloudflare Access later if needed
- ☐ CMS auth (if we add a CMS): GitHub OAuth (Sveltia) — defer until CMS decision

## 5. CMS / client editing (Phase 2 — only if clients self-edit)
- ☐ **Decision point:** request-based AI edits (no CMS) vs client self-edit (needs CMS)
- ☐ If CMS: **Sveltia** (lean, git-based) or **TinaCMS** (visual) — not self-hosted Strapi/Payload
- ☐ Define the content **schema** (the editable fields)
- ☐ Media handling inside the CMS (uploads → repo or object storage)
- ☐ Per-client wiring + a simple client "how to edit" guide
- Note: current default is **request-based + AI**, so this stays deferred unless a client insists

## 6. Image / media management (Phase 0 → 1)
- ☐ Phase 0: self-host + compress real photos in-repo; lazy-load below the fold
- ☐ Collect real Access Tech assets (owner/equipment, before/after pairs, hero)
- ☐ Phase 1: build-time optimization (e.g. `astro:assets`) once templatized
- ☐ Phase 2 (at scale): object storage (Cloudflare R2) + image CDN to avoid git photo-bloat

## 7. Template / fleet management (Phase 1)
- ☐ Extract content → `content.json` per client (the lightweight `ClientConfig`)
- ☐ Formalize per-client theming via the existing CSS tokens (palette/fonts/spacing)
- ☐ Repo strategy: a **template repo** + per-client instances
- ☐ **Snapshot/freeze** each site at handoff (prevent fleet-wide restyle drift)
- ☐ Versioning + a simple "eject to standalone" path
- ☐ Phase 1+: Astro + Content Collections if multi-page sites are needed

## 8. Billing / payments (Phase 0)
- ☐ **Stripe** subscription for the $100/mo retainer
- ☐ Deposit/setup invoice flow ($250 upfront)
- ☐ Failed-payment retries (dunning) + receipts
- ☐ Optional: Stripe customer portal for self-serve

## 9. Analytics / SEO / attribution (Phase 1)
- ☐ Lightweight analytics: **Plausible / Umami** (or GA)
- ☐ Lead attribution: optional **call tracking** (CallRail) per client
- ☐ Google Business Profile link + local SEO basics
- ☐ Per-page meta + OG image standardized in the template

## 10. Client management / ops (Phase 0 — mostly done)
- ✓ Client tracker (CSV)
- ✓ Onboarding checklist
- ✓ Preview / spec-site workflow
- ☐ Move tracker into Notion/Airtable as the live hub
- ☐ Password-manager vaults per client (1Password/Bitwarden)

## 11. Security (Phase 0 — baseline done)
- ✓ Security Baseline doc (vendors + 6 practices)
- ☐ Enforce MFA across all accounts; least-privilege when delegating
- ☐ Cyber liability insurance (once billing)
- ☐ Privacy policy on every client site (forms collect data)

## 12. AI engine (Phase 2 — DEFERRED)
- ⏸ Lead-gen (Google Places puller + qualification)
- ⏸ AI: lead → validated site config (structured output + eval)
- ⏸ Automated preview generation + cold-email pipeline (deliverability is the real constraint)
- Note: prove the manual loop with real paying clients first; build this as the portfolio
  layer on top of real usage.

---

### Critical path to first revenue (do these, in order)
1. Finish Access Tech (Section 0) · 2. Forms (1) · 3. Host + domain (2, 3) ·
4. Stripe (8) · 5. Launch + onboard (Section 10 checklist).
Everything else is Phase 1+/deferred.

---

## Design / QA pass (latest) — Access Tech
**Done**
- ✓ Icons migrated to **Lucide** (48 icons, `data-lucide`), brand marks kept as SVG
- ✓ Contrast fix: green text/eyebrows/labels on light bg now use `--ember-dark` (WCAG AA)
- ✓ Logo `<img>` `max-width` guard + smaller on mobile; fixed-toggle no longer covers footer (mobile body padding); Option 2 hero mobile min-height added
- ✓ Build-anatomy + SOP docs added under `/docs`

**New open items surfaced**
- ☐ Self-host the **gallery before/after + service-area map** images (still hot-link LoremFlickr) — pending Phil's real before/after pairs
- ☐ Add **robots.txt, sitemap.xml, canonical** (need final domain) + a **privacy policy** page
- ☐ Add lightweight **analytics** (Plausible/Umami)
- ☐ **Pin or self-host Lucide** (currently CDN `@latest`) to remove the runtime dependency
- ☐ At launch: strip to one layout + remove the redundant token set (`--ember*` and `--leaf*` are identical greens) and unused font pair

---

## Autonomous rough-edge sweep — done
- ✓ Removed **all external image hot-links** (LoremFlickr) — Option 2 hero now self-hosted photo; gallery before/after + service-area map are clean styled placeholders (await Phil's real pairs); dropped the loremflickr preconnects
- ✓ **SEO**: canonical + `og:url`, `robots.txt`, `sitemap.xml` (on accesstechnw.com)
- ✓ **privacy.html** page (forms collect data) + footer links in both layouts
- ✓ **404.html** branded not-found page
- ✓ **Pinned Lucide** to a fixed version (no more CDN `@latest`)
- ✓ **a11y**: visible `:focus-visible` outlines + "Skip to content" link
- Still pending (need you/external): noindex off, Deployment Protection off, domain/DNS, promote to main, Stripe, real before/after photos, analytics
