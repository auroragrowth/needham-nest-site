# The Needham Nest — website

Static site for The Needham Nest café, Needham Market. Plain HTML — no build step.

## Files
- `index.html` — main website (menu, hours, gallery, allergens, socials, Smash Burger Night banner).
- `smash-burger-night.html` — event ordering + booking page. Card payment via SumUp Hosted Checkout; bookings saved to Supabase. Served at `/smash-burger-night`.
- `assets/` — logo, photos and the food-hygiene badge (pulled out of the HTML so pages stay small).
- `needham-nest-allergens.pdf` — **add this file yourself** (your allergen matrix). Pages link to `/needham-nest-allergens.pdf`.
- `vercel.json` — clean URLs (harmless on other hosts; Cloudflare Pages does clean URLs automatically).

## Hosting (Cloudflare Pages)
Connect this repo in Cloudflare → Workers & Pages → Create → Pages. Framework preset: None. Build command: (empty). Output directory: `/`. Every push to `main` redeploys.

## Domain
Serve on **needhamnest.uk**. SumUp payment return URLs are tied to the domain, not the host, so bookings and payments keep working after the move. When pointing DNS, leave the email **MX** records alone so `info@needhamnest.uk` keeps working, and don't cancel SiteGround until email is confirmed.

## Backend
Bookings/orders live in Supabase (project `ocjdwtbvdqedpeheiwfc`, table `event_bookings`). Payment is handled by two Supabase Edge Functions: `smash-burger-checkout` and `smash-burger-verify`. The SumUp API key lives in Supabase secrets — never in this repo.
