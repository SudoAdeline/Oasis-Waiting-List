# Oasis Website — Full Session Notes

## Project Overview

**Oasis** is a female sanctuary space in Heidelberg, Germany. Three freelance facilitators offer wellness events and private services. Oasis is **not a company** — it's the name of the concept. Each facilitator is legally independent; events and payments are tied to individuals.

**Domain:** oasiscollective.de
**Hosting:** Hostinger (manual zip upload to `public_html`)
**Repo:** github.com/SudoAdeline/Oasis-Waiting-List (public)

---

## Facilitators

| Name | Role | Email |
|------|------|-------|
| Thembelihle Mchunu (Thembe) | Sound · Breathwork · Meditation · Movement | *TODO* |
| Elisabeth Bernbeck | Personal Massage · Event Organisation | elisabethbernbeck@gmail.com |
| Stefanie Gann (Steffi) | Inner Compass Guide (Life Coaching · Women's Circles) | stefanie.gann@gmx.net |

**Legal entity / copyright holder:** Elisabeth Bernbeck, Heumarkt 11, 69117 Heidelberg

---

## File Structure

```
index.html                    ← Waiting list / coming soon (LIVE at oasiscollective.de)
home.html                     ← Full website (swap to index.html at launch)
reserve.html                  ← Reservation / checkout page
style.css                     ← Shared styles across all pages
datenschutz.html              ← Website-level GDPR privacy policy (German)
impressum.html                ← Website-level legal notice (Elisabeth Bernbeck)

data/
  events.json                 ← Event data (also inlined in home.html)
  services.json               ← Private services per facilitator (also inlined in home.html)

facilitators/
  thembe.html                 ← Thembe's profile + private services
  elisabeth.html              ← Elisabeth's profile + private services
  steffi.html                 ← Steffi's profile + private services

legal/
  thembe-agb.html             ← Thembe's Terms & Conditions
  thembe-datenschutz.html     ← Thembe's Privacy Notice
  elisabeth-agb.html          ← Elisabeth's Terms & Conditions
  elisabeth-datenschutz.html  ← Elisabeth's Privacy Notice
  steffi-agb.html             ← Steffi's Terms & Conditions
  steffi-datenschutz.html     ← Steffi's Privacy Notice

assets/
  logo.png
  bg-water.png
  OASIS_INTRO_VIDEO.mp4
```

---

## Tech Stack

- Plain HTML / CSS / JS (no build tools, no framework)
- Google Forms for waiting list signups (hidden iframe submission)
- Stripe Payment Links for event/service payments (no backend needed)
- Client-side EN/DE language toggle with `localStorage` persistence
- Inline JSON data in `home.html` (because `fetch()` doesn't work on `file://`)

---

## Design System

- **Fonts:** Cormorant Garamond (display/headings), Jost (body)
- **Primary color:** Steel blue `#4A6B7A`
- **Text:** `#FAFAF5` (light), `rgba(250,250,245,0.7)` (muted)
- **Accent:** `#8AABB8`
- **Background:** Water image (`bg-water.png`) with dark overlay
- **Style:** Minimal, feminine, calm — water/botanical aesthetic

---

## What Was Built

### Phase 1 — Waiting List (LIVE)

**File:** `index.html`

- Full-screen water background with dark overlay
- Oasis logo + "celebrating sisterhood"
- Intro video (click to play — autoplay with sound is blocked by browsers)
- Oasis description (bilingual)
- Name + email signup form → Google Forms
- Datenschutz + Impressum links in footer
- EN/DE language toggle (English default)

**Google Forms integration:**
- Action URL: `https://docs.google.com/forms/d/e/1FAIpQLSeufxtRSt-exz1xaeb_qMT-ZYPXfEtREQE66vGAR3hrWesylA/formResponse`
- Name field: `entry.803396824`
- Email field: `entry.1589229907`
- Submissions visible at: Google Forms → Responses tab (or linked Google Sheet)

### Phase 2 — Full Website (LOCAL, not deployed yet)

**File:** `home.html`

Single-page scrolling site with sections:

1. **Hero** — Full-screen water background, logo, "celebrating sisterhood", scroll indicator
2. **Mission** — Intro video, sanctuary description, link to services
3. **Calendar** — 5 placeholder events rendered from inline JSON. Hover/tap reveals description, facilitator, price, and "Reserve" button
4. **Services** — 3 columns (Thembe, Elisabeth, Steffi) with private services, prices, Book buttons (→ Stripe), View Profile links
5. **About Us** — 3 cards with names, roles, bios, "Get in Touch" buttons
6. **Footer** — Individual legal links per facilitator, Impressum, Datenschutz, Instagram, copyright

**Navigation:** Fixed top nav with logo (left), section links + DE|EN toggle (right). Background appears on scroll.

### Phase 3 — Reserve Page

**File:** `reserve.html`

- Reads event ID from URL params (`?event=EVENT_ID`)
- Pre-fills event name, date, time, facilitator, price
- Form: name, email
- Consent checkbox linking to facilitator-specific legal pages
- "Pay & Reserve" → redirects to facilitator's Stripe Payment Link
- ⚠️ Still uses `fetch('data/events.json')` — needs inline data update

### Phase 4 — Facilitator Pages

**Files:** `facilitators/thembe.html`, `facilitators/elisabeth.html`, `facilitators/steffi.html`

- Profile header with name, role, bio
- Private services with descriptions, durations, prices
- Book buttons → Stripe Payment Links
- Back link to home
- ⚠️ Still use `fetch('../data/services.json')` — need inline data update

### Phase 5 — Legal Pages

**6 legal pages** (AGB + Datenschutz per facilitator):

| Facilitator | T&Cs | Privacy Notice |
|---|---|---|
| Thembe | `legal/thembe-agb.html` | `legal/thembe-datenschutz.html` |
| Elisabeth | `legal/elisabeth-agb.html` | `legal/elisabeth-datenschutz.html` |
| Steffi | `legal/steffi-agb.html` | `legal/steffi-datenschutz.html` |

All comply with German law (DDG, DSGVO, MStV). Styled consistently with the site.

### Phase 6 — Bilingual EN/DE

- Language toggle on all pages (English default)
- `data-en` / `data-de` attributes on translatable elements
- `localStorage` key: `oasis-lang`
- JS renders dynamic content (events, services, about) in the active language

---

## Placeholder Events (in `home.html`)

| Event | Facilitator | Date | Time | Price |
|-------|-------------|------|------|-------|
| Opening Ceremony | Thembe | 2026-03-14 (Sat) | 10:00–12:00 | €25 |
| Sonic Rest & Reset | Thembe | 2026-03-17 (Tue) | 17:00–20:00 | €35 |
| Sacred Cycle | Steffi | 2026-03-21 (Sat) | 10:00–12:00 | €30 |
| Tea Lounge | Thembe | 2026-03-28 (Sat) | 10:00–12:00 | €15 |
| Muse Choir | Thembe | 2026-04-04 (Sat) | 10:00–12:00 | €20 |

All events have placeholder Stripe links (`https://buy.stripe.com/PLACEHOLDER`).

---

## Placeholder Private Services

**Thembe:**
- Private Sound Bath — 60 min — €80
- Private Breathwork Session — 60 min — €70

**Elisabeth:**
- Relaxation Massage — 60 min — €70
- Deep Tissue Massage — 75 min — €90

**Steffi:**
- Life Coaching Session — 60 min — €75
- Inner Compass Package (4 Sessions) — 4×60 min — €260

All services have placeholder Stripe links.

---

## Hosting & Deployment

### Current Setup
- **Waiting list** is live at `oasiscollective.de` (uploaded as zip to Hostinger `public_html`)
- **Full website** (`home.html`) is local only — will replace `index.html` at launch

### Deployment Process
1. Zip the project files
2. Upload zip to Hostinger File Manager → `public_html`
3. Extract in place
4. At launch: rename `home.html` → `index.html` (replacing the waiting list)

### Past Hosting Issues (Resolved)
- Git auto-deploy failed (private repo, SSH key issues)
- Subdomain files nested incorrectly (zip extracted into subfolder)
- 404 with trailing slash — was browser cache from old `.htaccess` redirect
- Fixed by clearing cache / testing in incognito

---

## Known Issues & TODOs

### Must Fix Before Launch
- [ ] Replace all placeholder Stripe Payment Links with real ones
- [ ] Update `reserve.html` to use inline data (currently uses `fetch()`)
- [ ] Update facilitator pages to use inline data (currently use `fetch()`)
- [ ] Add Thembe's address + email in `legal/thembe-datenschutz.html`
- [ ] Add Steffi's address in `legal/steffi-datenschutz.html`
- [ ] Replace Thembe's placeholder email (`PLACEHOLDER@email.com`) in services data
- [ ] Update Instagram URL in footer (currently generic `instagram.com`)

### Nice to Have
- [ ] Add actual photos/portraits of facilitators
- [ ] Add more decorative elements (botanical SVGs, water accents)
- [ ] Test all pages on mobile devices
- [ ] Final bilingual review (German text accuracy)

---

## Key Decisions Made

1. **Oasis is not a company** — copyright goes to Elisabeth Bernbeck, not "Oasis Collective"
2. **Each facilitator is legally independent** — separate AGB + Datenschutz per person
3. **Stripe Payment Links** — no backend needed, each facilitator manages their own
4. **English is the default language** — DE toggle available
5. **Inline JSON data** — `fetch()` doesn't work on `file://`, so data is inlined in `home.html`
6. **Waiting list gates the site** — `index.html` is the gate, `home.html` is the real site
7. **Click-to-play video** — browser policies block autoplay with sound
8. **Manual hosting** — Git auto-deploy was too error-prone on Hostinger; manual zip upload works

---

## CSS Changes (Latest Session)

Added `.nav-lang` styles for the language toggle integrated into the nav bar:
- Inline-flex layout with vertical separator (`border-left`)
- Responsive breakpoints at 768px and 480px
- Replaced the old fixed-position `.lang-toggle` approach on `home.html`
- Old `.lang-toggle` CSS kept for `index.html` (waiting list) which still uses it
