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
- **Email shown on the site and for the contact form: bids@twfabs.com** (not the Wix draft's Inquires@).
- **Photos:** wait for the owner's own originals; use clearly marked placeholders until then. Don't use the Wix copies, and never use manufacturer/eBay/stock machine pictures.
- Logo: the same T.W Services logo files as the shop app (owner's own artwork).
- **First push straight to `main`** (notes file only) was approved once, to create the branch. Everything after goes through pull requests.

## Tech

- Hosting: Netlify, its own project on the owner's existing **Pro** team. Production deploy = 15 credits; deploy previews are free.
- Plain HTML and CSS, as few tools as possible, so any developer can pick it up later.
- Before choosing any Netlify feature, check the current docs (docs.netlify.com; add `.md` to a page URL for plain text).

## Working rules

- Work on a branch, open a pull request, send the owner the free deploy preview link. **The owner merges = publish.** Never push to `main` directly.
- Shrink photos before adding them (web-sized, about 200-400 KB each).
- No secrets in the code.

## Change log

- 2026-11-22: Repository created by the owner; project notes written; owner's Wix draft read and pages, email and photo decisions recorded. Nothing built yet.
