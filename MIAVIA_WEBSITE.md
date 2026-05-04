# Miavia — Website Implementation Record

_Last updated: 28 April 2026_

A complete record of the current Miavia website implementation in `index.html`, reflecting every script update, aesthetic refinement, and integration delivered to date.

**Tagline:** Your story, your way.
**Philosophy line:** The Miavia Philosophy · Designing memories for those who expect more.
**Display font:** Playfair Display (free Google Font — closest match to OGG, the paid display face the boss originally specified).

---

## Brand architecture

Three destinations, grouped under one philosophy.

| Destination | Property | Location | Status | Bedrooms · Guests · Bathrooms |
|---|---|---|---|---|
| Var Retreat | Miavia Var | Var, Provence | Available | 5 · 10 · 4 |
| Events & Yacht | Miavia Yacht | Côte d'Azur · Mediterranean Sea | Available | 5 · 10 · 6 |
| Miavia Suite Life | Miavia Suite | Côte d'Azur | **Fully Booked** (burgundy pill) | 1 · 2 · 2 |

Nine experiences, each with its own detail page and members-only booking form.

| Experience | Level / Type | Duration | Location | Guests | Season | Includes |
|---|---|---|---|---|---|---|
| Yoga Class | Mat Pilates · Yoga · Meditation | 90 min | Miavia Var · Miavia Yacht | Private or small group of 6 max | Year-round | Private instructor, mats & props |
| Wine Tasting | Red · White · Champagne | 2h (90 min · Champagne) | Miavia Var · Vineyard · Miavia Yacht | Private or small group of 8 max | Year-round | Private sommelier & small bites |
| Truffle Hunting | No experience required | Half day (3–4 h) | Var Countryside, Haute Provence | Up to 8 guests | November – March | Expert guide & truffle dog |
| Horse Riding | For Beginners | 2–3 h | Var Countryside | Private or Group of 4 | Year-round | Guided ride and all riding equipment |
| Cooking Classes | No experience required | Half day (3–4 h) | Miavia Var · Miavia Yacht | Up to 6 guests | Year-round | Private chef, seasonal ingredients, recipe cards, wine pairing |
| Painting Class | No experience required | 2–3 h | Miavia Var / Var Countryside | Private or small group (up to 4) | Year-round | Full selection of painting materials |
| Paintball | No experience required | 2–3 h | Var Countryside | Group of up to 4 | Year-round | All essential paintball equipment |
| Massage Wellness | In-residence / Onboard / Couples | 60–120 min | Miavia Var · Miavia Yacht · Miavia Suite | Per guest · couples available | Year-round | Licensed therapist, all oils and linens |
| Private Chef | Private dining · tailored menu | Evening (3–4 h) | Miavia Var · Miavia Yacht · Miavia Suite | Up to 10 guests | Year-round | Private chef, curated seasonal menu, wine pairing, full service |

---

## Page-by-page summary

### Home page
- Full-page hero with the Miavia wordmark and `YOUR STORY / YOUR WAY` tagline (white, OGG-style tracked uppercase).
- **Bordeaux intro fade** — page loads with full-screen burgundy overlay, then fades out gradually to reveal the photography. Logo + tagline + nav arrows fade in on top.
- Four directional nav prompts: up `Experiences`, left `About Miavia`, right `Contact`, down `Destinations`.

### About Miavia
- Full-page video hero with white logo, `ABOUT MIAVIA` title, `THE MIAVIA PHILOSOPHY` subtitle, scroll-down cue.
- Body copy: italic Playfair lead paragraph + DM Sans body, two paragraphs from the boss's final script ("Across the most extraordinary places…", "Miavia is for those who choose to shape their own story…").
- Image carousel rotating through real Miavia photography (yacht / Monaco interior / horse riders / wine flight / truffle guide / chefs / outdoor meditation).
- **THE TIME IS NOW** CTA panel — black background, photograph behind at 30% opacity with radial vignette, white logo, white Playfair title (OGG tracking), italic Cormorant tagline, white-outline `BEGIN` button → routes to sign-up.

### Destinations
- Three stacked cards with alternating left/right layout.
  - **Var Retreat** → Miavia Var. _"Untouched, expansive woodland deep in the Var countryside…"_
  - **Events & Yacht** → Miavia Yacht. _"Days at anchor in still coves, evenings where the sky meets the water…"_
  - **Miavia Suite Life** → Miavia Suite — `FULLY BOOKED` burgundy pill in the corner. _"Live and breathe life in a unique coastal enclave on the Côte d'Azur…"_

### Property pages (Miavia Var / Yacht / Suite)
1. Full-page video hero with `[PROPERTY TITLE]` only (the philosophy subtitle was removed at the boss's request — too repetitive).
2. Scroll-revealed description (location eyebrow + italic lead + DM Sans body).
3. Property stats strip — bedrooms · guests · bathrooms only (length / crew / platform / amenities removed).
4. **THE SPACE** eyebrow only — no carousel headline, the eyebrow speaks for itself.
5. Image carousel of the property at 560px height.
6. Experiences Curated For You — `TAILORED FOR YOUR STAY.` headline (uppercase OGG-style tracking).
7. Other Experiences — small `OTHER EXPERIENCES` eyebrow only, then a 620-px tall carousel rotating through curated landscape-only photography from across the experience folders.
8. **BEGIN YOUR STORY** booking form — auth-gated dark aesthetic.

### Experiences index
- `EXPERIENCES` eyebrow only at the top (no headline / italic tagline — too repetitive).
- 3-column grid of nine experience cards: Yoga / Wine / Truffle / Horse / Cooking / Painting / Paintball / Massage Wellness / Private Chef.
- Each card: 4:5 photograph → uppercase Playfair title (OGG tracking) → DM Sans description paragraph → DISCOVER link.

### Individual experience detail pages
1. Full-page video hero → `[EXPERIENCE TITLE]` + `THE MIAVIA PHILOSOPHY / DESIGNING MEMORIES FOR THOSE WHO EXPECT MORE`.
2. Location eyebrow + skeleton intro paragraph.
3. **Side-by-side layout** matching the boss's wireframe: `EXPERIENCE DETAILS` panel (labelled rows: Type / Duration / Location / Guests / Season / Includes) on one side, image carousel on the other.
4. **Yoga and Wine pages have multiple side-by-side blocks** — one per sub-type, alternating sides for editorial rhythm:
   - Yoga: Mat Pilates → Yoga → Meditation
   - Wine: Red Wine → White Wine → Champagne
   Each block has its own subtype-specific Type/Duration/Location/Guests/Season/Includes row.
5. Auth-gated `RESERVE` booking form on the dark aesthetic, with Clerk profile auto-fill.

### Contact page
- Members-only — guests see a "Reach the Miavia Team" blocker with sign-in / become-a-member CTAs.
- Logged-in: light card with Miavia wordmark + `SHARE YOUR STORY` title.
- Fields: *First Name, *Last Name, *Email, Country Code, Phone Number, Topic, additional details textarea, `SEND` button.
- Submissions go to **Formspree** (`formspree.io/f/xdaybonp`) and forward to the `#website-contact` Slack channel via Formspree's native Slack action.

### Sign Up — `REGISTER FOR MEMBERSHIP`
- Full custom form (replaces Clerk's drop-in component) so all seven boss-specified fields can be collected at sign-up:
  1. *First Name (required)
  2. *Last Name (required)
  3. *Email (required)
  4. *Password (required, min 8 chars)
  5. Country Code (dropdown: France / Monaco / Italy / UK / US / Germany / Switzerland / Spain)
  6. Phone Number
  7. Birthday + Language (English / Français / Italiano / Español / Deutsch)
- On submit → Clerk creates the account → 6-digit verification code emailed → user enters code → session active → routed to home.
- Custom fields (countryCode / phone / birthday / language) saved to Clerk's `unsafeMetadata`, auto-pulled into all booking forms going forward.

### Sign In — `WELCOME BACK`
- Clerk's polished `<SignIn />` component on a centered card. Themed to Miavia (cream card, oat borders, Playfair title, burgundy submit button, italic Cormorant footer link).

### Booking flow
- **Begin Your Story** (Property Booking Form) — black aesthetic, white Miavia logo, dark inputs with white labels. Auth-gated. Pre-fills from the signed-in member's Clerk profile. Collects: first/last/email/phone, birthday, language, destination (Miavia Var / Miavia Yacht / Miavia Suite), guests, check-in/check-out, repeating per-experience date/time rows.
- **Reserve** (Experience Booking Form on each detail page) — same dark aesthetic, auth-gated, pre-filled.
- **Booking Confirmation** — `YOUR STORY BEGINS HERE` headline + "Your stay is now confirmed, thoughtfully arranged and ready to unfold. Your confirmation number is MVxxxxxx." + itinerary receipt list.

### Menu (slide-out drawer) — auth-aware
| Signed out | Signed in |
|---|---|
| About Miavia | About Miavia |
| Destinations | Destinations |
| Experiences | Experiences |
| — | Contact |
| Sign Up | My Account |
| Log In | Sign Out |
| Language selector (EN / FR / IT / ES) | Language selector |

Header top-right: Sign In link (signed out) → Clerk avatar dropdown (signed in).

### Footer / meta banner — identical on every page
- Miavia logo (left) · Copyrights & Terms italic Cormorant (centre-bottom) · Instagram | Contact (right). Burgundy background, white wordmark, no link columns.

---

## Authentication (Clerk)

### What's wired
- **Clerk JS SDK** loaded via CDN with the Miavia publishable key (`pk_test_…`). No npm / build step required.
- `useClerkUser()` React hook re-renders any component on auth state changes.
- `AuthGate` component renders the "Members Only" blocker on the Contact page and as a swap-in for the booking forms on every property and experience page.
- `profileFromClerk(user)` helper pulls a normalised profile (firstName / lastName / email / phone / birthday / language) used to auto-fill every form.
- Clerk's `<UserButton />` mounts on the header for signed-in members (avatar with profile + sign-out menu).

### What members can do
- Register with the full 7-field custom form, including Birthday and Language.
- Verify their email via 6-digit code.
- Sign in via Clerk's hosted login (email + password, plus Google / Apple if enabled in Clerk dashboard).
- View / edit their profile via Clerk's `<UserProfile />` (opened from the header's "My Account" link).
- Sign out from the avatar dropdown or the menu.

### Clerk theme
The Clerk modals and the inline sign-in component all wear a Miavia-matched theme:
- Cream card background (`#FAF8F5`) with thin oat border, sharp corners, soft shadow.
- Playfair Display title in OGG tracking.
- Italic Cormorant subtitle.
- DM Sans labels in small caps.
- Burgundy `#7A1F2B` primary button, hovers to `#5E1620`.
- Hidden default Clerk logo (the Miavia logo on the page handles brand).

---

## Contact form & Slack

The Contact page is a real, working pipeline:

```
Member fills form → Formspree (formspree.io/f/xdaybonp)
                       │
                       ├─→ Email to operations@careta.com
                       ├─→ Submission archived in Formspree dashboard
                       └─→ Posted to the #website-contact Slack channel
```

- Free Formspree plan, native Slack integration via the Workflow tab (no Zapier required).
- Honeypot field on the form silently absorbs bot submissions.
- Built-in Formspree spam filtering.
- Configurable via `window.MIAVIA_CONTACT_ENDPOINT` in `index.html`.

Setup walkthrough is in [`CONTACT_FORM_SETUP.md`](./CONTACT_FORM_SETUP.md).

---

## Real photography wired in

All experience photography loads from local folders under `experience_photos/`. No more stock or descriptive labels.

| Folder | Count | Sample files |
|---|---|---|
| `experience_photos/cooking/` | 18 | chefs_team.jpg, pasta_fork.jpg, lively_class.jpg, dough_front.jpg, … |
| `experience_photos/horses/` | 9 | two_riders_river.jpg, brown_hilltop.jpg, horse_pasture_fog.jpg, … |
| `experience_photos/painting/` | 9 | sip_friends.jpg, empty_studio.jpg, wine_painting_session.jpg, … |
| `experience_photos/paintball/` | 2 | camo_aim.jpg, camo_cover.jpg |
| `experience_photos/wellness/` | 10 | face_massage_candles.jpg, hot_stones.jpg, petrissage_hands.jpg, … |
| `experience_photos/truffle/` | 5 | truffle_basket.jpg, truffles_leaves.jpg, dog_foraging.jpg, dog_close.jpg, guide_and_dog.jpg |
| `experience_photos/wine/` | 12 | sommelier_flight.jpg, cellar_pour_red.jpg, wine_cheese_stone.jpg, decanter_pour.jpg, champagne_pour_flute.jpg, … |
| `experience_photos/yoga/` | 9 | meditation_sunset_group.jpg, group_rocks_sunrise.jpg, meditation_circle_window.jpg, downward_dog_close.jpg, … |
| `experience_photos/chef/` | 11 | plating_artistry.jpg, chef_portrait.jpg, tuile_sauce.jpg, salmon_dish.jpg, venison_sauce.jpg, honey_pastry.jpg, … |

Apartment, yachting, and brand assets continue to live at `apartment_photos/`, `yachting_photos/`, and the root logo PNGs.

The "Moments to compose your stay" carousels on every property page were curated to use only landscape-friendly photos (so portrait-oriented shots don't crop awkwardly in the wide rectangular slot).

---

## Aesthetic system

| Token | Value | Used for |
|---|---|---|
| Display font | `Playfair Display` (with Fraunces / Cormorant fallback) | All major titles |
| Body font | `DM Sans` | Form labels, descriptions, UI |
| Italic accent | `Cormorant Garamond` italic | Taglines, italic leads |
| Burgundy primary | `#7A1F2B` | Buttons, accents, fully-booked pill, Clerk primary |
| Burgundy deep | `#5E1620` | Hover state, header background |
| Black | `#0A0A0A` / `#111` | Dark booking forms, body text |
| Cream | `#FAF8F5` | Page background |
| Oat border | `#E8E2D9`, `#D5CFC5` | Card edges, dividers |
| Muted text | `#8F857A`, `#9A9089` | Eyebrows, hints |
| OGG tracking | `letter-spacing: 0.04em` | All major titles |
| Date input accent | `#5E1620` (via CSS `accent-color`) | Browser-native date picker highlight |

Sharp corners (no rounded radii) throughout. Every page transitions are subtle fades / Ken-Burns / scroll-reveals.

---

## Deliverables & files

Everything is in the `MiaVia` folder inside the user's Downloads directory.

| File | Purpose |
|---|---|
| `index.html` | The single-file site — React via Babel standalone, no build step. Open directly in a browser. |
| `experience_photos/` | All curated experience photography, keyed per experience. |
| `apartment_photos/` · `yachting_photos/` | Real Miavia Monaco and Oksanchik yacht shoots. |
| `miavia-deploy/` | A clean copy of the deployable site files (no backend, no docs) — drag-drop to a host. |
| `miavia-deploy-2026-04-28-v15.zip` | Latest deploy bundle (~322 MB). |
| `miavia-github/` · `miavia-github-full/` | Mirrors used to build the GitHub deploy bundles. |
| `backend/` | Optional Node/Express backend (not currently used — the site runs on Formspree + Clerk). |
| `CONTACT_FORM_SETUP.md` | Formspree + Slack integration walkthrough. |
| `MIAVIA_WEBSITE.md` | This document. |

### Deploy guide

`miavia-deploy/DEPLOY.md` covers two paths:
1. **GitHub → Vercel** (recommended) — push to a GitHub repo, import on Vercel, deploy. ~15 minutes.
2. **Vercel CLI** — `npx vercel --prod` from the deploy folder. ~5 minutes, requires Terminal.

---

## Pending / deferred work

Everything still on the road map, with current status:

| Item | Status |
|---|---|
| **Stripe payment integration** | Pending. Boss has chosen Path C (full online payment for fixed-price experiences). To be wired up after current aesthetic round. Custom-built Stripe Checkout via a small serverless function on Vercel will be the cleanest path. |
| **Intro animation multi-stage fade** | Single fade implemented. The 3-stage storyboard (logo on burgundy → logo+slogan → logo+slogan+nav → video) requires the final reel + per-stage stills before we wire it. |
| **Booking form Option 2 — fully automated calendar per item** | Option 1 is live. Option 2 (per-experience inline calendar with availability) requires a backend / scheduling platform. Recommended: Stripe + Cal.com integration if needed. |
| **Subtype-specific hero imagery** for wine Red / White / Champagne | All three currently share the sommelier-flight hero. Splitting requires identifying / shooting hero photography for each variant. |
| **Email verification UX polish** | Working. Could be improved by adding a "change email" flow if a user types the wrong address during sign-up. |

---

## Recent change log (latest sessions)

This is what's been delivered since the last save:

- **Aesthetic polish (boss's modification round 2)**
  - Playfair Display applied across all titles (closest free OGG alternative).
  - Bordeaux intro fade-out on home hero.
  - About description italic-lead + body treatment.
  - About bottom `THE TIME IS NOW` panel: black background, photograph behind at low opacity, white logo, BEGIN button.
  - Date picker accent recolored to bordeaux.
  - Property booking form switched to dark aesthetic.
  - Footer simplified to skeleton's minimal meta-banner.
  - Slide counters (1/4 etc.) removed from every photo carousel.
  - "Other Experiences" carousel made taller and stocked with landscape-only photos.
  - Property pages reduced to first 3 stats only.
  - All carousel titles ("A landscape, composed", "Composed in detail", "M/Y Oksanchik …") removed — `THE SPACE` eyebrow alone.
  - All carousel section headlines ("Tailored for your stay", "Moments to compose your stay") set to OGG-style uppercase.
  - "MOMENTS TO COMPOSE YOUR STAY" headline removed from below `OTHER EXPERIENCES` eyebrow.
  - `THE MIAVIA PHILOSOPHY` subtitle removed from property heroes.
  - Italic taglines removed from each experience hero ("Expression, free from rules…", etc.) and from each card on the experiences index.
  - Experiences index introduction (headline + tagline) removed; only `EXPERIENCES` eyebrow remains.
  - About page carousel filled with seven real Miavia photographs (yacht / residence / landscape / wine / truffle / cuisine / wellness).

- **Experience detail layout (boss's wireframe)**
  - Side-by-side `EXPERIENCE DETAILS` + image carousel layout per the wireframe.
  - Yoga: three stacked side-by-side blocks (Mat Pilates / Yoga / Meditation), alternating sides.
  - Wine: three stacked side-by-side blocks (Red / White / Champagne), alternating sides.
  - Italic descriptions removed from each subtype block.

- **Authentication (Clerk)**
  - Loaded Clerk JS SDK with the Miavia publishable key.
  - Built `useClerkUser` React hook + `AuthGate` blocker component.
  - Replaced legacy `window.miaviaUser` flag everywhere with real Clerk session checks.
  - Fully themed Clerk's modals + inline forms in Miavia aesthetic (cream / oat / burgundy / Playfair / DM Sans).
  - Added Clerk's `<UserButton />` to header for signed-in members.
  - Auth-gated the Contact page and every booking form (property + experience).
  - Built a custom 7-field sign-up form (replaces Clerk's drop-in `<SignUp />`) with email-code verification step.
  - Login still uses Clerk's polished `<SignIn />` component for fast returning-member UX.

- **Contact form**
  - Formspree integration live with native Slack delivery.
  - Honeypot anti-bot field.
  - Loading / error / success states polished.

- **Destinations**
  - Miavia Suite Life marked **Fully Booked** with burgundy pill.

- **Documentation**
  - `CONTACT_FORM_SETUP.md` rewritten Formspree-first.
  - `miavia-deploy/DEPLOY.md` rewritten for Vercel.
  - `STRIPE_SETUP.md` walks through Payment Links per experience.

---

## Booking form rules (boss spec — `MIAVIA WEBSITE BOOKING FORM AND CONTACT RULES.pdf`)

Applied to both `PropertyBookingForm` (property hero pages) and `ExperienceBookingForm` (experience detail pages). The forms are still **members-only**; if a guest visits, they see the dark "Members Only" panel with **Sign In** + **Become a Member** CTAs in the booking-form slot.

### Destinations
- Limited to **Miavia Var (`flyosc`)** and **Miavia Yacht (`yachting`)** — Suite removed (it's marked Fully Booked).
- Property pages preselect their own destination on load.
- Experience-detail forms only show the destination dropdown when the experience is offered at more than one place; if it has only one valid destination, that destination is auto-selected (no dropdown shown).

### Smart destination ↔ experience filtering
Driven by the global `EXP_DESTINATIONS` map in `index.html`:

| Experience  | Var | Yacht |
|-------------|:---:|:---:|
| Yoga        | ✅ | ✅ |
| Wine        | ✅ | ✅ |
| Painting    | ✅ | ✅ |
| Wellness    | ✅ | ✅ |
| Private Chef| ✅ | ✅ |
| Truffle     | ✅ |    |
| Horses      | ✅ |    |
| Cooking     | ✅ |    |
| Paintball   | ✅ |    |

- Picking a destination filters which experiences appear in the picker.
- Picking an experience whose destinations don't include the current selection auto-switches the destination to its first valid one.
- Picking an experience that's only offered at one place auto-locks the destination there.

### Subtypes (`EXP_SUBTYPES`)
- **Yoga** → Yoga · Mat Pilates · Meditation
- **Wine Tasting** → Red Wine · White Wine · Champagne
- All other experiences have no subtype dropdown.

### Date mode toggle
- Two-pill toggle: **One Day** / **Multiple Days**.
- One Day → single date picker.
- Multiple Days → start + end date pickers (and on the experience form, a time field).
- The selected mode is forwarded to Formspree as `stay_type`.

### Guest count
- Free-form `<input type=number min=1>`, no maximum.
- Placeholder: `No fixed limit — events welcome`.

### Per-person pricing display (`EXP_PRICING`)
Each experience shows its current price next to / under the picker:

| Experience | Label |
|---|---|
| Yoga      | €150 / person   |
| Wine      | €200 / person   |
| Truffle   | €450 / group    |
| Horses    | €200 / rider    |
| Cooking   | €280 / person   |
| Painting  | €150 / person   |
| Paintball | €120 / group    |
| Wellness  | €180 / 60 min   |
| Chef      | €600 / evening  |

Price labels are display-only; the actual amount charged is whatever is set on the matching Stripe Payment Link. To change a price: edit the Payment Link in the Stripe dashboard **and** update the label here so they stay in sync.

### Payment redirect
- "Continue to Payment →" submits the form, posts the booking inquiry to Formspree (so the concierge gets it in `#website-contact` even if Stripe isn't yet wired), then redirects to the matching `MIAVIA_STRIPE_LINKS[experienceId]` URL with `client_reference_id=<booking_number>` and `prefilled_email=<member email>`.
- Property booking with no `stay` Payment Link configured falls through to the in-house `#confirmation` page.

### Auth gate (guest fallback)
- Guests visiting any booking form see the dark "MEMBERS ONLY" panel inline (page above is fully browseable).
- Two CTAs: **Sign In** (opens Clerk modal) and **Become a Member** (opens custom 7-field sign-up).
- After successful sign-up, the user lands back on the page they were trying to book from.

### Source-of-truth constants
All four booking-form constants live at the top of `index.html`, grouped right above `PropertyBookingForm`:
- `EXP_LABELS` — display names
- `EXP_PRICING` — `{ amount, perPerson, label }`
- `EXP_DESTINATIONS` — which destinations each experience is offered at
- `EXP_SUBTYPES` — per-experience subtype choices

Mirrored to `miavia-deploy/index.html`, `miavia-github/index.html`, `miavia-github-full/index.html`. Latest deploy bundle: `miavia-deploy-2026-04-28-v21.zip`.

---

## Live deploy: Netlify + miavia.com

### Hosting
- **Host:** Netlify (free plan).
- **Netlify project:** `chimerical-jelly-811a00`
- **Temporary URL:** https://chimerical-jelly-811a00.netlify.app
- **Custom domain:** `miavia.com` (and `www.miavia.com`)
- **Domain registrar:** GoDaddy (renews 24 Dec 2026 — £18.99/yr).

### How the site is deployed
1. Bundle the site folder (`miavia-deploy/`) into a zip.
2. Drag the unzipped folder onto https://app.netlify.com/drop (or onto the existing project's Deploys tab).
3. Netlify hosts everything as static files — `index.html` is the entry point; React + Babel run in the browser via CDN, so there's no build step.

### Compressed bundle for Netlify Drop
Full `miavia-deploy/` is ~313 MB (mostly photos). Netlify Drop has practical upload limits, so the build script for deploys:
- Resizes every photo to 1100 px max (longest side), JPEG quality 55, progressive.
- Drops 26 orphan photos that aren't referenced anywhere in `index.html` (mostly leftover Monaco/test images).
- Strips `.md` documentation (not required for the site to render).
- Recompresses logo PNGs to 480 px max.

Result: **~7.9 MB zip** containing 121 used photos + `index.html` + 3 logos. Visually identical at typical browser sizes.

Latest mini bundle: `miavia-netlify-mini-2026-04-28.zip`.

### Custom domain — how it's wired
1. **Netlify side:** Domain management → added `miavia.com` and `www.miavia.com` → set up Netlify DNS (rather than manual A/CNAME records).
2. **Netlify gave us 4 nameservers:**
   - `dns1.p06.nsone.net`
   - `dns2.p06.nsone.net`
   - `dns3.p06.nsone.net`
   - `dns4.p06.nsone.net`
3. **GoDaddy side:** Domain → DNS → Nameservers → Change Nameservers → "I'll use my own nameservers" → pasted in the four Netlify nameservers → Continue & Verify.
4. **DNS propagation:** typically 1–4 hours, up to 24 hours worst case.
5. **HTTPS:** Netlify auto-provisions a Let's Encrypt cert once DNS verifies.

When complete, both `https://miavia.com` and `https://www.miavia.com` resolve to the Netlify site with a green padlock.

### Things to know about GoDaddy
- GoDaddy's "Website" / "Coming Soon" page is **separate** from Miavia's real site. Don't click "Publish Site" — that would put GoDaddy's AI-generated coming-soon page in front of `miavia.com` instead of the Netlify site. Just leave it alone.
- GoDaddy sometimes adds parking/MX records. After nameserver swap, those records no longer apply because Netlify DNS is authoritative — so they're ignored automatically.

---

## Online payments: deferred

### Why
Toren is registered in Monaco. **Stripe does not support Monaco** as a country for business registration. Andorra, Liechtenstein, San Marino, and Monaco are all excluded from Stripe's supported list. The CAPTCHA error during signup was a separate browser issue, but even past that, Stripe would have rejected the Monaco entity at the activation step.

### Decision (2026-04-28)
Launch the site as **inquiry-only** for now. No bank account is set up yet anyway. Real online payments stay paused until either:
1. Toren registers a French entity (most Monaco luxury businesses also have a French SARL/SAS), and Stripe is set up under that, **or**
2. Toren picks a Monaco-friendly alternative — most likely **PayPal Business** (officially supports Monaco; ~3.4% + €0.35 per transaction; works as a drop-in replacement for our Payment Links pattern), **or**
3. Toren goes through their Monaco bank for a Worldline / CFM / BNP Paribas Monaco / Société Générale Monaco merchant account (the proper concierge-grade option, takes 2–4 weeks to set up).

### What still works without payment
Everything except the actual charge step:
- Members sign up via Clerk's custom 7-field form.
- Logged-in members fill out the booking form on a property page or experience page.
- Form submits → Formspree posts it to email + the `#website-contact` Slack channel with all booking details.
- Member is redirected to the `#confirmation` page.

The concierge then follows up with a manual quote/invoice/payment link until self-serve checkout is wired in.

### How to flip payments back on later
Once a payment processor is chosen and active:
1. Create a Payment Link per experience in Stripe / PayPal / Worldline.
2. Paste each URL into the `MIAVIA_STRIPE_LINKS` config block at the top of `index.html` (or rename to `MIAVIA_PAYMENT_LINKS` if switching processor — code is otherwise the same).
3. Re-deploy.

The redirect logic, `client_reference_id` correlation with the booking number, and Formspree double-write are already in place — just need the URL slots filled in. The full step-by-step is in `STRIPE_SETUP.md`.

---

## Quick reference

| What | Where |
|---|---|
| Live site (temp) | https://chimerical-jelly-811a00.netlify.app |
| Live site (custom domain) | https://miavia.com (after DNS propagates) |
| Netlify dashboard | https://app.netlify.com → `chimerical-jelly-811a00` |
| Domain registrar | GoDaddy → My Products → `miavia.com` |
| Auth (members) | Clerk dashboard with `pk_test_YWxsb3dlZC1iZWFyLTcwLmNsZXJrLmFjY291bnRzLmRldiQ` |
| Form submissions | Formspree `xdaybonp` + Slack `#website-contact` |
| Payments | Paused — see "Online payments: deferred" above |
| Latest full bundle | `miavia-deploy-2026-04-28-v21.zip` (308 MB) |
| Latest Netlify mini | `miavia-netlify-mini-2026-04-28.zip` (7.9 MB) |
| Latest update zip | `miavia-update-2026-04-28.zip` (81 KB — index.html + docs only) |

---

## Mobile responsiveness (added 2026-04-29)

Added a global `<style>` block at the top of `index.html` with `@media (max-width: 768px)` and `@media (max-width: 480px)` rules. Targets the inline-style patterns the site uses (attribute substring selectors `[style*="..."]`) and overrides them with `!important` so phones render correctly.

What flips on mobile (≤768px):
- Header tightens to `22px` horizontal padding so logo + menu fit on a phone.
- All `padding: 120px 40px` (and similar) collapse to `64px 22px` — content uses the full screen width.
- Two-column and three-column grids stack into a single column. The four-column featured-experiences grid becomes two-up.
- The booking form's `1.3fr 1fr 1fr 28px` row stacks vertically.
- Hero `<h1>` clamps tighten so headlines don't overflow.
- Submit buttons stretch to ~320 px wide for friendly tappability.
- The "Scroll" hint indicator hides (saves vertical space).
- Carousels still slide naturally with touch.

The site stays fully desktop-first; mobile is an override layer, not a rebuild. To tweak a specific element, add another rule under that media query.

---

## About-page duplicate-image fix (2026-04-29)

Two changes prevented seeing the same photo twice on the About page:

1. **Carousel slide #1**: was `YACHT.profileSunset` (yacht at sunset). The "THE TIME IS NOW" CTA panel below uses the same photo as a darkened background, so the same image was appearing twice. Changed slide #1 to `YACHT.diningTablescape` (formal yacht dinner). Changed CTA background to `APT.bedroomDark`.

2. **Carousel slide #2**: was `MON_NEW[15]` (a Monaco residence photo from the dynamic `MON_NEW` array). The mini Netlify bundle build script couldn't detect this dynamic path so it dropped the file from the bundle, causing the slide to fall back to a placeholder. Changed to `APT.dining` (Monaco apartment dining), which is in the static `APT` constant and is always shipped in every bundle.

The 7 carousel slides are now all unique photos drawn from different brand pillars (yacht / residence / horses / wine / truffle / cooking / yoga).

---

## Membership approval workflow (added 2026-04-29)

Per the boss's spec, sign-ups are now **manual approval**. New applicants don't get instant member access; the concierge reviews them in the Clerk dashboard before booking unlocks.

### Flow

```
Applicant submits 7-field sign-up form
  → Email verification (6-digit code)
  → Clerk user created with unsafeMetadata.membershipStatus = "pending"
  → User signed out automatically
  → Lands on "Application Received" page (dark aesthetic)
  → Slack alert posted to #website-contact via Formspree
Concierge reviews in https://dashboard.clerk.com → Users
  → Edits unsafeMetadata → sets "membershipStatus": "approved"
(Optional) Make.com webhook fires → automated welcome email
Applicant signs in → site reads metadata → full member access
```

### Code changes
- `useClerkUser()` hook now returns `{ isLoaded, isSignedIn, isApproved, membershipStatus, user }`.
- `membershipStatusOf(user)` helper reads `unsafeMetadata.membershipStatus` (or `publicMetadata.membershipStatus`); defaults to `'pending'` for any user without the flag.
- `CustomSignUpForm.submitCode()` after successful email verification: stamps `membershipStatus: 'pending'` + `appliedAt`, posts the applicant to Formspree (→ Slack), signs the user out, navigates to `pending-review`.
- New page: `PendingReviewPage` — dark, on-brand "Application Received" panel with copy and a Return Home button. Routed at `pending-review`.
- `PropertyBookingForm`, `ExperienceBookingForm`, and `ContactPage` each have a second auth gate: if `isSignedIn && !isApproved`, they show "Application Under Review" instead of the form.

### What the concierge does
1. Open https://dashboard.clerk.com → choose Miavia application → **Users**.
2. Find the applicant by email (newest first).
3. Open profile → scroll to **Unsafe metadata** → click **Edit**.
4. Change `"membershipStatus": "pending"` to `"membershipStatus": "approved"`.
5. (Optional) add `"approvedAt": "<ISO date>"`.
6. Save. The applicant can now sign in and book.

To **reject**: leave them as `pending`, or click **Lock account** / **Delete user**.

### Grandfathering existing members
Anyone who signed up before 2026-04-29 has no `membershipStatus` field, so they'll see "Application Under Review" until manually approved in the Clerk dashboard. Approve yourself + the boss as a one-time backfill.

### Automated approval email (optional follow-up)
Currently the boss/concierge emails the approved member personally. To automate it: set up a Clerk webhook (`user.updated`) → Make.com workflow → Gmail (or Resend). Detailed step-by-step in **`MEMBERSHIP_APPROVAL.md`** Part 3.

### Source-of-truth values
- `'pending'` — applied but not approved. Default for any user without the flag.
- `'approved'` — full member, all features unlocked.
- (Defensive default) — anything else is treated as `'pending'`.

### Files
- `MEMBERSHIP_APPROVAL.md` — full operational guide (how to approve, how to set up email automation, troubleshooting).
- `index.html` — `useClerkUser` hook, `PendingReviewPage`, three approval gates.
- Latest deploy bundle: `miavia-deploy-2026-04-29-v3.zip` (308 MB, full quality, mobile + approval flow).
