# Backend / Platform Backlog — Hirobius

Every core moving piece behind the sites, grouped by domain and phased so we don't over-build.
Reconciled to actual state (see git history for the work log).

- **Phase 0 — Now:** finish Access Tech + the minimum to launch & bill one client.
- **Phase 1 — Next (at 2–3 clients):** templatize + the repeatable production pipeline.
- **Phase 2 — Later (only if/when justified):** CMS/auth, fleet tooling, AI engine.

Status key: ☐ todo · ◐ in progress · ✓ done · ⏸ deferred (on purpose)

---

## 0. Site — Access Tech (Phase 0)
- ✓ Green brand recolor (full layout), real logo (header/footer) + favicon
- ✓ Real photos self-hosted + optimized (hero/about in WebP, preloaded hero)
- ✓ Lead form wired (Web3Forms → adrian@hirobius.com) — **tested end-to-end, delivers**
- ✓ Icons migrated to Lucide (pinned version); brand marks kept as SVG
- ✓ SEO: title/meta, OG/Twitter + real og-image, LocalBusiness JSON-LD, canonical + og:url, robots.txt, sitemap.xml
- ✓ privacy.html + 404.html; privacy linked in footer
- ✓ Accessibility: WCAG-AA contrast fix, :focus-visible outlines, skip link
- ✓ Layout toggle removed (CSS/HTML/JS); full layout only
- ✓ README, ARCHITECTURE, build-anatomy + SOP docs, template inventory
- ✓ LAUNCHED: live on accesstechnw.com (production public + indexable)
- ◐ Before/After gallery + service-area map — styled placeholders, **awaiting Phil's real pairs**
- ⏸ Delete parked Option 2 markup + collapse duplicate tokens (`--ember*`/`--leaf*`) + Bricolage-only fonts — parked per Adrian
- ☐ Privacy policy copy once-over before launch (template text is generic)

## 1. Launch (Phase 0 — the critical path)
- ☐ Invoice + collect the $1,500 build fee from Phil (Owner: Adrian)
- ✓ Access Tech deal (one-off): $1,500 build + case-by-case edits — **not the standard model**
- ✓ Pointed accesstechnw.com at Vercel (A @ + www CNAME on Squarespace; email/MX untouched)
- ✓ Vercel Deployment Protection OFF (site public)
- ✓ Removed pre-launch noindex and pushed (site indexable)
- ◐ Post-launch verify: confirm live padlock + form-from-live-domain (form still delivers to Adrian until key swap)
- ☐ Submit sitemap to Google Search Console + link Google Business Profile (Owner: Adrian)

## 2. Content from client (blocked on Phil)
- ☐ Real before/after photo pairs → swap into gallery
- ☐ (Optional) service-area map image or keep styled placeholder
- ☐ Final copy/phone/credentials sign-off

## 3. Post-launch polish (small, agent-ownable)
- ☐ Analytics: Plausible or Umami (needs account tied to domain)
- ☐ Self-host fonts + Lucide (blocked in this sandbox; do from local machine)
- ☐ Minify HTML/CSS/JS (optional, minor)
- ☐ Lazy-load below-the-fold background images (minor)

## 4. Ops / business (Phase 0 → 1, Owner: Adrian)
- ✓ Proposal template + filled Access Tech proposal (update to $1,500 + case-by-case for future sends)
- ✓ Client tracker (CSV), onboarding checklist, preview/spec-site workflow, security baseline
- ☐ MFA on all accounts (registrar, host, email, Stripe, vault)
- ☐ Password-manager vaults per client (1Password/Bitwarden)
- ☐ Move tracker into Notion/Airtable as the live hub
- ☐ Service agreement / terms doc
- ☐ Cyber liability insurance (once billing)
- ☐ Domain renewal tracking + reminders (registrar: Cloudflare standard; register in client's name)

## 5. Templatization (Phase 1 — start after Phil is live & billing)
- ☐ Extract content → `content.json` per client (the lightweight ClientConfig; shape drafted in docs/CLIENT-BUILD-ANATOMY.md)
- ☐ Formalize per-client theming via the existing CSS tokens
- ☐ Template repo + per-client instances; snapshot/freeze at handoff (anti-drift)
- ☐ Versioning + eject-to-standalone path
- ☐ Standardized reusable form snippet (new Web3Forms key per client)
- ☐ Client intake form (collect all per-client inputs in one shot)
- ☐ `previews.hirobius.com` wildcard scheme for spec-site outreach
- ☐ Decide: per-client host projects vs multi-tenant (at volume)
- ⏸ Astro + Content Collections — only if/when multi-page sites are needed

## 6. Deferred (Phase 2 — do not build yet)
- ⏸ CMS / client self-editing (Sveltia/Tina) — request-based AI edits are the default
- ⏸ Auth (only if CMS or gated previews demand it)
- ⏸ Object storage + image CDN (R2) at scale
- ⏸ Call tracking (CallRail) per client
- ⏸ AI engine: lead-gen puller → lead-to-config agent → eval → auto-preview + cold-email pipeline
  (prove the manual loop with paying clients first; deliverability is the real constraint)

---

### Critical path (in order)
1. Collect $1,500 → 2. Domain/DNS → 3. Launch flips (protection off, noindex out) →
4. Post-launch verify + Search Console → 5. Phil's before/afters → 6. Phase 1 templatization.
