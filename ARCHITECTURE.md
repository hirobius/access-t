# Architecture — Access Tech site / Hirobius template

An architectural read of this repo: what it is today, the issues, and where it should go
to become the reusable foundation for the agency. Two lenses throughout: **(A)** this site
as the Access Tech deliverable, and **(B)** this repo as the seed of a repeatable template.

## Current state (snapshot)
- Single `index.html` (~1,160 lines / ~77 KB). Pure static, **no build step, no config**.
- **Ships two layouts** (orange + green) + a bottom toggle, plus the dead CSS/JS of whichever
  is unused — i.e. a *pitch/preview artifact*, not a finished product.
- **14 hot-linked LoremFlickr images**; loads **two** font pairs (Bricolage/Hanken +
  Cabinet/Satoshi) via render-blocking external CSS.
- **Form is non-functional** (preview `alert()`, no field `name`s, no handler).
- `noindex` still present; `README` empty.

## Bright spot (real asset)
The **design-token system** — palette, spacing, and type are CSS custom properties
(`--leaf`, `--ember`, `--s*`, `--font-*`). Re-theming per client is mostly variable swaps,
so the eventual template refactor is already half-built. Also: self-contained,
zero-dependency, trivially hostable and portable.

## Issues by severity

### High — fix before launch
1. **Hot-linked images (×14).** Third-party URLs can rotate/rate-limit/vanish and are
   unoptimized — the #1 production-fragility risk. Self-host + optimize real photos.
2. **Form doesn't work.** The site's core job is lead capture; the form only `alert()`s.
   Wire to a host-agnostic service (Web3Forms/Formspree) with field `name`s + honeypot.
3. **Two layouts + toggle still shipped.** Doubles the code and ships dead CSS/JS. Pick one
   (orange) and strip the rest.

### Medium
4. **Content welded to markup.** All copy/services/contact is hardcoded inline — the thing
   blocking reuse, per-client theming, a CMS, and the config/AI direction. Fix = extract
   content → data (the seed `ClientConfig`).
5. **Font bloat.** Loads both font pairs; after picking orange, drop the green pair.
6. **No SEO scaffolding.** No `LocalBusiness` JSON-LD, no sitemap/robots; `noindex` still on.

### Low / housekeeping
7. Empty README (no handoff docs).
8. Accessibility: images are CSS backgrounds (no `alt`) — use `<img>` for real photos.
9. Land the finished product cleanly on `main` (main currently mirrors the dual-layout preview).

## Target architecture (agency template — not today)
- **Content as data:** one `content.json` per client = a lightweight `ClientConfig`; the
  template renders from it. Unlocks reuse + theming + future CMS/AI.
- **Theme via the existing tokens:** formalize the CSS-variable set as the per-client theme.
- **One template, per-client instances:** each client = content + theme + images, rendered by
  a shared template and **snapshot-frozen at handoff** (prevents fleet-wide restyle drift).
- **Light SSG (Astro) only once templatized** — not needed for a single static site.
- Self-hosted/optimized images · host-agnostic forms · managed static host.

## Recommended sequence
- **Now (ship Access Tech, ~1 session):** strip to orange-only → self-host images → wire form
  → drop unused fonts → add JSON-LD + robots/sitemap → README → remove `noindex` at launch.
- **Later (only at 2–3 clients):** extract content → `content.json`, formalize theme tokens,
  decide template/fleet repo strategy.

**Guardrail:** don't templatize now — premature optimization. Ship the clean single static
site for Access Tech; the token system means the template refactor is already half-done.

See `BACKLOG.md` for the full task list across forms, hosting, auth, CMS, images, templates,
billing, and the rest of the platform.
