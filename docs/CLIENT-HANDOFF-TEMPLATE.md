# Client Handoff Template

Reusable handoff for a finished client site. Two parts:

- **Part A** is client-facing. Paste it into the handoff email or a one-pager and fill the `[brackets]`.
- **Part B** is your internal delivery cheat sheet. **Do not send it to the client.**

Style note: no em dashes anywhere (house style). Keep it plain and friendly.

---

## Part A — Send to the client

**Your site is live at [domain]. Here is everything you need to know to run it.**

### Making changes
- Text or email me any change request. There is no login for you to manage. You tell me what you want, I make it happen.
- Small tweaks (copy, phone numbers, swapping a photo) are quick. Larger additions (new sections or pages) I will quote before starting.

### Your leads
- Every request from the site lands in your inbox as an email. **Those emails are your record, so keep them.**
- The form service also keeps a backup copy on their side for about 30 days on the free plan. If you want a permanent, searchable list of every lead (a spreadsheet or simple CRM), I can set that up. Just ask.
- Spam protection is on. If junk ever starts getting through, tell me and I will tighten it.

### What you own
- The domain and your email are yours and were left untouched during launch.
- Keep **auto-renew on** for [domain] so the site and your email never lapse. A lapsed domain takes both offline.

### Going live and getting found
- The site is live now, but Google takes a few weeks to fully index a new site, so search traffic builds over time.
- The single biggest local-search boost is your **Google Business Profile**. If you have not claimed it, I can set it up for you.

### If something ever looks wrong
- Text me. The site is backed up and version-controlled, so I can roll it back fast.

### What is included
- The build is a one-time fee. Ongoing changes are handled per request. There is no monthly charge unless we agree on a care plan.
- *(If a care plan applies: "Your $[MONTHLY]/mo plan covers hosting, monitoring, domain oversight, and up to [X] of edits per month.")*

---

## Part B — Internal delivery cheat sheet (do NOT send)

### Hosting and recurring cost, the real picture
- **Hosting is effectively free** at one-page-local-business scale (Vercel free tier covers it with room to spare).
- **Caveat:** Vercel's free (Hobby) plan is technically non-commercial per their terms. Fine for one small site. To be clean or to scale, either budget ~$20/mo for Vercel Pro **or** use **Cloudflare Pages, which is genuinely free and commercial-OK.**
- **The only real recurring cost is the domain (~$15 to $20/yr)**, and it renews on the client's own registrar account since they own it. **Do not put the client's card on file for hosting.**
- If you want recurring revenue, make it an explicit **care plan** (flat monthly = hosting + monitoring + a small edit allowance + domain oversight), not a hosting passthrough.

### Web3Forms notes
- The leads ARE the emails in the client's inbox. Those do not expire. Web3Forms PRO's storage is a redundant backup, not the source of truth, so do not scare the client with "go PRO or lose leads."
- Free tier: 250 submissions/month, honeypot spam guard. Enough for a local business.
- One access key per client, tied to the client's email. Optionally CC yourself.
- Honest upsell: "want a permanent list of leads?" then pipe the form to a Google Sheet or CRM (paid setup).

### Upsell menu (keep in your back pocket)
- **Care plan / retainer** (the recurring one, biggest lever)
- Lead automation: form to Google Sheet / CRM / instant text-to-owner
- Analytics plus a simple monthly traffic and leads report
- Google Business Profile setup and ongoing posts/reviews
- Hero video loop (if they have a clip)
- Ongoing before/after photo refreshes to keep the gallery alive
- Extra pages later: service detail pages, seasonal landing pages, financing, a reviews section once they have testimonials
- Brand extensions: business cards, vehicle decals, print matching the site

### Pre-handoff checklist (do all before giving the keys)
- [ ] Payment collected (build fee), invoice sent with client's business address
- [ ] Domain pointed and resolving over HTTPS; email (MX) records confirmed intact
- [ ] Form delivering to the client's inbox (tested end to end); noindex removed
- [ ] Google Business Profile: claimed or offered
- [ ] **Credentials hygiene:** client keeps their own registrar/email logins; you hold only the access you need; **rotate any password the client shared with you** and store it in your vault, never a text thread
- [ ] Auto-renew ON for the domain; renewal date logged in the client tracker
- [ ] Client tracker updated: domain, live date, renewal date, form key location, links
- [ ] Scope and turnaround stated in writing (what is included vs billable; small edits within 1 to 2 business days)
- [ ] Light service agreement / terms sent (what you are and are not responsible for: not liable for client content accuracy, their email, or third-party downtime like the host or form service)
- [ ] Repo snapshot/tag at launch so future template changes cannot drift this live site
