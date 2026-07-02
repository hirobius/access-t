# Agency Template — Full Inventory & Burndown (Hirobius)

The master list of every moving piece needed to mass-produce client sites, tracked against
the **Access Tech reference build**. This is the superset; `BACKLOG.md` is the phased backend
slice and `CLIENT-BUILD-ANATOMY.md` is the deep teardown.

**Status:** ✓ done & reusable · ◐ built in reference, needs parameterizing/cleanup · ☐ todo · ⏸ deferred
**Phase:** P0 = ship/bill first client · P1 = templatize (2–3 clients) · P2 = later/scale
**Owner:** A = agent/code · H = Adrian (decision/dashboard) · X = external (client/DNS/3rd-party)

## Progress at a glance
- **Page template (sections):** mostly ✓ built; before/after + service-area imagery ◐ placeholder.
- **Functional core (form, SEO, assets, icons):** ✓ working on the reference.
- **Templatization (config, fleet, repo strategy):** ☐ not started (P1).
- **Ops/business (billing, CRM hub, MFA, privacy):** ☐ mostly open.
- **AI engine:** ⏸ deferred until manual loop is proven.

---

## A. Page template — sections / components
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Top utility bar (phones + area) | ✓ | P0 | A | parameterize phones/area |
| Sticky nav + mobile overlay menu | ✓ | P0 | A | logo + menu links per client |
| Hero (eyebrow/headline/sub/CTAs/bg) | ✓ | P0 | A | copy + hero image per client |
| Trust band (4 badges) | ✓ | P0 | A | per-client trust points |
| About (lead/body/credentials/portrait/badge) | ✓ | P0 | A | |
| Services grid (icon+title+desc) | ✓ | P0 | A | services list per client |
| Before/After gallery | ◐ | P0 | A/X | images are LoremFlickr placeholders; needs Phil's real pairs |
| Why-us (4 points) | ✓ | P0 | A | |
| Service area (copy + tags + map) | ◐ | P0 | A | map slot still placeholder |
| Estimate form (fields + phone cards) | ✓ | P0 | A | wired (Web3Forms) |
| Final CTA band | ✓ | P0 | A | |
| Footer (brand/links/contact/legal) | ✓ | P0 | A | |
| Layout toggle (Option 1/2) | ◐ | P0 | A | temporary; remove at launch |
| Second layout (Option 2 "Condensed") | ◐ | P0 | H | decide keep-as-variant vs drop |
| 404 page | ☐ | P1 | A | not built |
| Thank-you state after form | ✓ | P0 | A | inline success exists (no separate page) |

## B. Design system / theming
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Color tokens (palette) | ✓ | P0 | A | |
| Spacing scale (`--s1..s7`) | ◐ | P1 | A | ~half of component padding is hardcoded rem |
| Type ramp + font loading | ◐ | P0 | A | dedupe to one font pair per client |
| Radius / shadow tokens | ✓ | P0 | A | |
| Button styles | ✓ | P0 | A | |
| Token redundancy cleanup (`--ember*` == `--leaf*`) | ☐ | P0 | A | collapse to one set when stripping to one layout |
| Per-client theme mechanism (swap token values) | ◐ | P1 | A | tokens exist; no formal config yet |

## C. Content & configuration (the templatization core)
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| `ClientConfig` schema (content-as-data) | ☐ | P1 | A | proposed shape in anatomy doc |
| `content.json` per client | ☐ | P1 | A | |
| Full copy extraction from markup | ☐ | P1 | A | |

## D. Assets & media
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Logo variants (white/color/icon) | ✓ | P0 | A | processed for reference |
| Photo optimization pipeline (Pillow) | ✓ | P0 | A | recipe documented in SOP |
| OG image (1200×630) generation | ✓ | P0 | A | |
| Favicon | ✓ | P0 | A | green icon PNG |
| Image self-hosting | ◐ | P0 | A/X | gallery + map still hot-link LoremFlickr |
| Lazy-load below-the-fold images | ☐ | P1 | A | quick win |
| Object storage / image CDN at scale | ⏸ | P2 | A | avoid git photo-bloat |

## E. Integrations
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Lead form (Web3Forms) | ✓ | P0 | A/X | new access key per client |
| Spam protection (honeypot) | ✓ | P0 | A | captcha optional |
| Submission storage beyond email | ☐ | P1 | H | decide (sheet/DB) — email-only for now |
| Fonts (Google + Fontshare) | ✓ | P0 | A | self-host/subset later |
| Icons (Lucide) | ◐ | P0 | A | currently CDN `@latest`; pin or self-host |
| Analytics (Plausible/Umami) | ☐ | P1 | A | |
| Call tracking (CallRail) | ⏸ | P2 | H | optional lead attribution |
| Real embedded service-area map | ☐ | P1 | A | optional |

## F. SEO & metadata
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Title + meta description | ✓ | P0 | A | per client |
| OpenGraph / Twitter cards | ✓ | P0 | A | per client (domain) |
| LocalBusiness JSON-LD | ✓ | P0 | A | per-client data |
| robots.txt | ☐ | P0 | A | needs final domain |
| sitemap.xml | ☐ | P0 | A | needs final domain |
| Canonical URL | ☐ | P0 | A | needs final domain |
| Remove pre-launch `noindex` | ☐ | P0 | A | at launch |
| Accessibility (alt/focus/contrast) | ◐ | P0 | A | contrast ✓; alt text + focus pass remaining |

## G. Hosting / deploy / infra
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Host choice (Vercel now) | ◐ | P0 | H | CF Pages/Netlify portable |
| Git auto-deploy | ✓ | P0 | A | |
| Preview vs production envs | ✓ | P0 | A | |
| SSL | ✓ | P0 | X | automatic |
| Preview gating (Deployment Protection) | ✓ | P0 | H | on now; off at launch |
| Domain registration (client's name) | ☐ | P0 | X/H | per client |
| DNS pointing | ☐ | P0 | H/X | at launch |
| Preview subdomain scheme (`previews.hirobius.com`) | ☐ | P1 | H | for spec-site outreach |

## H. Templatization / fleet management
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Template repo + per-client instances | ☐ | P1 | H/A | |
| Snapshot/freeze on handoff (anti-drift) | ☐ | P1 | A | |
| Eject-to-standalone path | ☐ | P1 | A | |
| Template versioning | ☐ | P1 | A | |
| SSG (Astro) for multi-page | ⏸ | P1+ | A | only if needed |

## I. Client ops / CRM
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Proposal template + filled proposal | ✓ | P0 | A | delivered as files |
| Client tracker (CSV) | ✓ | P0 | A | move to Notion/Airtable hub |
| Onboarding checklist | ✓ | P0 | A | file |
| Preview / spec-site workflow | ✓ | P0 | A | file |
| Consolidate ops docs into repo/ops space | ☐ | P1 | A/H | several live only as downloads |
| Password-manager vaults per client | ☐ | P0 | H | |
| Client intake form (collect inputs) | ☐ | P1 | A | |

## J. Billing / payments
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Edits billed case-by-case (no subscription) | ✓ | P0 | H | pricing locked: $1500 build + per-request edits |
| Build invoice ($1,500 upfront) | ☐ | P0 | H | |
| Dunning / receipts | ☐ | P1 | H | |
| Customer portal | ⏸ | P2 | H | optional |

## K. Security & compliance
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Security baseline doc | ✓ | P0 | A | file |
| MFA across all accounts | ☐ | P0 | H | |
| Least-privilege / delegation | ☐ | P1 | H | when hiring |
| Cyber liability insurance | ☐ | P1 | H | once billing |
| Privacy policy page (forms collect data) | ☐ | P0 | A | per client |
| Service agreement / terms | ☐ | P0 | H | |

## L. Documentation / SOPs
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| ARCHITECTURE.md | ✓ | — | A | in repo |
| BACKLOG.md | ✓ | — | A | in repo |
| README.md | ✓ | — | A | in repo |
| CLIENT-BUILD-ANATOMY.md | ✓ | — | A | in repo |
| SOP-NEW-SITE-AGENT.md | ✓ | — | A | in repo |
| SOP-NEW-SITE-HUMAN.md | ✓ | — | A | in repo |
| AGENCY-TEMPLATE-INVENTORY.md (this) | ✓ | — | A | in repo |

## M. AI engine (deferred — P2)
| Item | Status | Phase | Owner | Notes |
|---|---|---|---|---|
| Lead-gen (Google Places puller) | ⏸ | P2 | A | |
| Lead → `ClientConfig` agent | ⏸ | P2 | A | builds on the schema |
| Eval / quality loop | ⏸ | P2 | A | |
| Auto preview + cold-email pipeline | ⏸ | P2 | A | deliverability is the real constraint |

---

## N. Per-client launch checklist (repeat every site)
1. ☐ Collect assets + content (logo, photos, copy, lead email, domain)
2. ☐ Build from template (tokens, copy, images, services)
3. ☐ Get a Web3Forms key for the client's email + wire it
4. ☐ SEO (title/meta/JSON-LD/og) + favicon
5. ☐ QA gate (breakpoints 900/680/420, links, end-to-end form test, console)
6. ☐ Register domain in client's name + point DNS
7. ☐ Remove `noindex` + turn off Deployment Protection
8. ☐ Promote to production
9. ☐ Start Stripe (setup + monthly)
10. ☐ Handoff note + add to tracker

---

## Next 5 (critical path — Access Tech to live + billing)
1. **Invoice + collect the $1,500 build fee.** Edits are billed case-by-case (no subscription). *(H)*
2. **Domain**: point `accesstechnw.com` (DNS). *(H/X)*
3. **Launch flips**: remove `noindex`, turn off Deployment Protection, promote to `main`. *(A + H)*
4. **Real before/after photos** from Phil → swap gallery off placeholders. *(X → A)*
5. **robots.txt + sitemap.xml + canonical + privacy policy** (once domain is set). *(A)*

Everything below the line (templatization core, fleet tooling, AI engine) is **P1+** — do it
after this site is live, billed, and you've felt the manual process once or twice.
