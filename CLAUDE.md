# T.W Services company website: notes for Claude

Read this file at the start of every session. Keep it current: whenever a decision changes or a feature ships, update the relevant section in the same change.

## Who this is for

The owner of T.W Services, a small structural steel fabrication and erection company (Central US time). The owner is not a programmer. Explain choices in plain language, keep the site simple, and never assume he can debug code. He approves what goes live.

## What this site is (owner, 2026-11-22)

- A **public company website** for customers (GCs, owners, architects): who T.W Services is, what it does, past projects, and how to get in touch.
- **No logins and no database.** Plain pages only, so it costs almost nothing to run and holds nothing sensitive.
- **Completely separate** from the internal shop/bids/billing app (repository `TylerTW/Shop`, site `twsteel-shop`). Never share code, data, logins or links to internal pages between them.
- Starting point: a draft the owner made on Wix. Use it as a guide for pages, wording and layout; build our own design (don't copy Wix's template).
- **Domain and DNS come later**, after the site is built. Until then it runs on a `*.netlify.app` address.

## Owner decisions (2026-11-22)

- **Pages (7):** Home, General Contractors, Fabrication for Fabricators, Residential & Small Jobs, About, Projects (photo gallery), Contact.
- **Wording:** from the Wix draft (tyler0069.wixsite.com/twfabs), spelling and grammar cleaned up, meaning unchanged. Company facts from it: 1701 CR 3405, Liberty Hill, TX 78642; 512-966-5999; serving Central Texas; started in a 3,000 sq ft shop with a crew of 2, now 24,000 sq ft after 20 years.
- **No email address anywhere on the site** (owner, 2026-11-22, to keep it away from spam harvesters). The top bar and footer say "Send us a message" and link to the contact form. Messages from the form are emailed to the owner's own address, which is set **only in Netlify** (Forms > Notifications), never in the code or these notes. bids@twfabs.com is not a real mailbox; don't use it.
- **Photos:** wait for the owner's own originals; use clearly marked placeholders until then. Don't use the Wix copies, and never use manufacturer/eBay/stock machine pictures.
- Logo: the same T.W Services logo files as the shop app (owner's own artwork).
- **First push straight to `main`** (notes file only) was approved once, to create the branch. Everything after goes through pull requests.

## How the site is laid out

- `site/` is everything that gets published (`netlify.toml`: publish `site`, no build command). This notes file is outside it on purpose, so it is never public.
- One folder per page with an `index.html` (clean addresses like `/about/`): `/`, `/general-contractors/`, `/fabricators/`, `/residential-small-jobs/`, `/projects/`, `/about/`, `/contact/`, plus `/thanks/` (after the form is sent) and `404.html`.
- `site/assets/style.css` is the only stylesheet. **No JavaScript at all**: the phone menu is a `<details>` element; there are two menus (desktop row and phone dropdown) in each page's header. The header and footer are copied into every page, so a change to them must be made in all 9 files.
- Logo files in `site/assets/img/` are copies of the shop app's (`logo-mark.png` in the header, `logo-dark.png` in the footer).
- Photo placeholders are `<div class="photo-slot">what goes here</div>` (shown as "PHOTO COMING"). Replace each with the owner's photo (`<img>` with alt text, shrunk to web size).
- `netlify.toml` sets safety headers (a Content Security Policy that allows no scripts and only our own files). If a script, map embed or outside font is ever added, the policy must be updated or it will be blocked.

## Contact form (checked against Netlify docs 2026-11-22)

- Netlify Forms: `<form name="contact" data-netlify="true" netlify-honeypot="company-website" action="/thanks/">`. **Free and unlimited on credit-based plans.** Spam filtered by Akismet plus our hidden honeypot field.
- Form detection: Manage > Forms > Settings > "Find forms on your pages" (on since 2026-11-22). Netlify's docs still call it "Enable form detection". It only scans at publish time.
- Email notification to the owner's address (set in Netlify only, never in the code): Forms > Notifications. An address outside the Netlify team gets one confirmation email that must be clicked first (or, if that isn't offered yet, the address must be a team member). The `email` field becomes the Reply-to, so replying answers the customer.
- The email subject line is set by the owner in Netlify (Forms > Notifications). Don't add a hidden `subject` field to the form: per Netlify's docs it would override his.
- Fields: name*, company, email*, phone, what do you need (service list), project location, message*. No file uploads (plans are sent by email instead).

## Still to do (owner)

- Netlify: form detection is **on** (owner, 2026-11-22; new UI: Manage > Forms > Settings > "Find forms on your pages"). **Done 2026-11-22:** email notification to the owner's own address (not written here), any form, his own subject line.
- Netlify's new dashboard has its own AI agent ("Ask for a change" box, Publish button, "Add a contact form" suggestions). Owner should not use them: changes go through GitHub pull requests only.
- Send own photos (and which project names may be shown); answer the wording questions ("0 injuries", "century" vs "decades" of experience, press brake 3/16").
- Make the project public when ready; then domain and DNS.

## Tech

- Hosting: Netlify, its own project on the owner's existing **Pro** team. Production deploy = 15 credits; deploy previews are free.
- Plain HTML and CSS, as few tools as possible, so any developer can pick it up later.
- Before choosing any Netlify feature, check the current docs (docs.netlify.com; add `.md` to a page URL for plain text).

## Working rules

- Work on a branch, open a pull request, send the owner the free deploy preview link. **The owner merges = publish.** Never push to `main` directly.
- Shrink photos before adding them (web-sized, about 200-400 KB each).
- No secrets in the code.

## Change log

- 2026-11-22: Repository created by the owner; project notes written; owner's Wix draft read and pages, email and photo decisions recorded.
- 2026-11-22: First version built: 7 pages from the Wix wording (cleaned up), contact form (Netlify Forms), photo placeholders, logo, safety headers. Checked at phone and desktop size (no errors, no sideways scroll, all links work). TylerTW/tw-services-website#1, merged by the owner.
- 2026-11-22: Owner created the Netlify project (Import from GitHub; production branch main). First production deploy of the site (15 credits). New projects start private, so only the owner can view it for now. Form detection and the bids@ email notification not turned on yet.
- 2026-11-22: Owner turned on form detection. This notes-only pull request is merged to trigger the publish that registers the contact form.
- 2026-11-22: Removed bids@twfabs.com from every page (owner doesn't own it and wants no email address on the site); top bar and footer link to the contact form instead. Form messages go to the owner's address, set in Netlify only.
- 2026-11-22: Owner merged TylerTW/tw-services-website#3 (email removed; live) and set up the form's email notification in Netlify. Queued on the branch, not yet in a pull request: removed the form's built-in subject line so the owner's Netlify subject is used.
