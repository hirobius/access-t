# SOP — Launching a New Client Site (Human Guide)

For a non-developer or junior Hirobius team member. This walks you through taking a new client
from "signed up" to "live website," using the Access Tech site as the template. You don't need to
write code — but you need to know what we collect, where things live, what "good" looks like, and
when to hand off to Adrian or the AI agent.

**The short version:** every Hirobius site is one file (`index.html`) plus a folder of images.
We copy the Access Tech build, swap in the new client's colors, logo, photos, words, and contact
info, point a fresh contact-form key at the client's email, test everything, then point the
domain at it and flip it live. Most of the hands-on building is done by the AI agent — your job is
to gather the right inputs, check the work, and run the launch checklist.

Read the **Glossary** at the bottom first if any term is unfamiliar.

---

## Step 1 — Collect everything from the client

You can't build a good site from a vague brief. Get all of this up front (an intake form or a
quick call). If something's missing, chase it before building starts.

**About the business**
- Business name and a one-line description of what they do
- Their list of services (aim for 6–9), each with a sentence describing it
- The areas/towns they serve
- What makes them trustworthy: licenses, certifications, "X years in business," "free estimates,"
  degrees, etc.
- Phone number(s) — note which number goes with which region if more than one
- **The email address where they want leads to land** (this is important — the contact form sends
  to it)

**Brand and visuals**
- Their logo — ideally a see-through (transparent) PNG. We need a light/white version (for the
  dark top bar) and a full-color version. If they only have one, the agent can make the other.
- Their brand colors (hex codes if they have them; otherwise grab them from the logo)
- Photos: a strong hero shot, a photo of the owner or their equipment, and ideally several
  before/after pairs of real jobs. Real photos massively outperform stock — push for them.

**Domain and ownership**
- The web address (domain) they want, e.g. `theirbusiness.com`
- Important: the domain must be registered **in the client's name** — they own it, not us.

Hand this complete package to the AI agent (which follows `SOP-NEW-SITE-AGENT.md`) to do the build.

---

## Step 2 — Understand where things live

So you can sanity-check the work:

- **`index.html`** — the entire website. All the text, layout, colors, and the contact form are
  in this one file. There is no separate database or CMS.
- **`/images`** folder — every photo and logo lives here. We always store the client's own images
  here (never link to someone else's website for images — those can break or disappear).
- **Colors and fonts** are controlled by a small set of named settings at the top of the file
  (called "design tokens"). Re-coloring a site for a new client is mostly changing those values
  plus the logo and photos. You won't edit these by hand, but it's why turnaround is fast.
- The Access Tech file currently ships **two design options** with a toggle at the bottom. A real
  client site ships only **one** — the agent removes the other and the toggle during the build.

---

## Step 3 — What "good" looks like (review the build)

Once the agent reports a preview is ready, open the preview link and check it like a picky customer:

- **It's clearly the new client**, not Access Tech. No leftover "Access Tech," forestry wording,
  or Idaho/Washington phone numbers anywhere — including the browser tab title and the footer.
- **The logo looks crisp** on the dark top bar (not a white box around it, not blurry).
- **Photos are real and sharp**, load quickly, and none are missing/broken.
- **Colors match the brand** and text is easy to read (no light-gray-on-white, no clashing).
- **The words read well** — services make sense, contact info is correct, no placeholder text like
  "Project Name / Location" left behind.
- **Only one design** shows (no toggle buttons floating at the bottom).

If something's off, send it back to the agent with specifics.

---

## Step 4 — The QA checklist (plain language)

Go through all of these on the preview before you even think about launching. If any fail, it's
not ready.

- **Phones, tablets, and desktops:** resize your browser window from wide to narrow (or open it on
  your phone). The menu should turn into a "hamburger" button on small screens, sections should
  stack neatly, and nothing should run off the side of the screen.
- **Every link works:** clicking the menu items jumps to the right section; clicking a phone number
  offers to call it; the "Free Estimate" buttons jump to the form.
- **The contact form actually works:** fill it in and submit it. You should see a "thanks" message
  appear, AND a test email should arrive in the **client's** inbox (confirm with them or via a
  shared inbox). This is the single most important test — the whole site exists to capture leads.
- **No broken images:** every photo and the logo load; the favicon (little icon in the browser tab)
  shows up.
- **No hidden errors:** if you know how, open the browser's developer console (right-click →
  Inspect → Console) and confirm there are no red error messages. If you're not sure, ask the agent
  to confirm "zero console errors."
- **It's still hidden from Google:** before launch the site should carry a "noindex" tag so Google
  doesn't list a half-finished page. The agent confirms this is present pre-launch and removes it at
  launch.

---

## Step 5 — The launch checklist

Do these in order, only after QA passes and the **client has approved** the preview.

1. **Point the domain at the site.** Add the client's domain to the hosting project (Vercel) and
   set the DNS records it asks for. Wait for the secure padlock (SSL) to turn on — this can take a
   bit. (If DNS is confusing, this is a good escalate-to-Adrian moment.)
2. **Let Google see it.** Remove the "noindex" tag so the site can be found in search.
3. **Make it public.** Turn off **Deployment Protection** so anyone can visit without a special
   link.
4. **Go live.** Promote the approved version to "production" (the main branch). The live domain now
   serves the finished site.
5. **Final live check.** Visit the real web address: confirm the padlock is there, images load,
   and submit **one more** test through the contact form to make sure leads arrive on the live site.

After launch: confirm the client has paid per **their agreement** (check the client tracker — pricing varies per deal until the standard model is set)
in Stripe. (Don't start billing yourself — see escalation.)

---

## When to escalate to Adrian

Loop Adrian in (don't guess) when:
- The domain/DNS step is unclear, or there's any question about **who owns the domain** (it must be
  the client).
- The contact form test email does **not** arrive after a couple of tries.
- The client wants something the template doesn't do (extra pages, online booking, e-commerce, a
  login, a system for them to edit the site themselves).
- Anything touching **money**: invoicing, pricing an edit request, refunds.
- You're unsure whether the site is truly ready to go public.
- Any account access, passwords, or the Web3Forms key need to be stored or shared.

---

## Glossary

- **DNS** — the internet's address book. It's what connects the client's domain name (like
  `theirbusiness.com`) to the actual server hosting the site. Updating DNS is how a new site "goes
  live" on its real address.
- **noindex** — a small instruction in the page that tells Google "don't list this in search
  results yet." We keep it on while building so an unfinished site doesn't show up, and remove it at
  launch.
- **Deployment Protection** — a Vercel setting that keeps preview versions private (you need to be
  logged in or have a special bypass link to view them). Great for client review; we turn it off at
  launch so the public can visit.
- **Web3Forms key** — a free, unique code that connects the site's contact form to an email inbox.
  Every site gets its **own** key pointed at **that client's** lead email. Never reuse another
  client's key.
- **Edits** — changes are requested by the client and handled by us (billed per the client's
  agreement). Edits are request-based and AI-assisted — clients don't log in to change the
  site themselves; they ask us.
- **Preview vs. production** — *preview* is the private draft we review; *production* is the public,
  live site on the real domain. We only promote to production at launch.
- **Hero** — the big banner image and headline at the very top of the page.
- **Design tokens** — the small set of named color/spacing/font settings at the top of the file
  that control the whole site's look, which is why re-theming for a new client is fast.
