# Oasis — Project Summary

## Overview

**Oasis** is a physical female sanctuary space in Heidelberg, Germany. Three independent freelance facilitators offer wellness events and private services under the Oasis concept. Oasis is not a legal entity — each facilitator operates independently and handles their own payments and legal obligations.

- **Domain:** oasiscollective.de
- **Tagline:** celebrating sisterhood
- **Mission:** our female sanctuary is a safe space to rest and realign with yourself
- **Hosting:** Hostinger (manual zip upload to `public_html`)
- **Repo:** github.com/SudoAdeline/Oasis-Waiting-List

---

## Facilitators

| Name | Role | Email |
|------|------|-------|
| Thembelihle Mchunu (Thembe) | Sound · Breathwork · Meditation · Movement | — |
| Elisabeth Bernbeck | Personal Massage · Event Organisation | elisabethbernbeck@gmail.com |
| Stefanie Gann (Steffi) | Inner Compass Guide · Life Coaching · Women's Circles | stefanie.gann@gmx.net |

**Legal entity / copyright holder:** Elisabeth Bernbeck, Heumarkt 11, 69117 Heidelberg

---

## Tech Stack

- Plain HTML / CSS / JS — no build tools, no framework
- Google Fonts: Cormorant Garamond (display) + Jost (body)
- Google Forms for waiting list signups
- Stripe Payment Links for event and service payments (no backend needed)
- EN/DE language toggle with `localStorage` persistence
- Inline JSON data embedded in HTML (no server required to run locally)

---

## Design System

| Token | Value |
|-------|-------|
| Primary colour | Steel blue `#4A6B7A` |
| Text light | `#FAFAF5` |
| Text muted | `rgba(250,250,245,0.7)` |
| Accent | `#8AABB8` |
| Background | Water photo (`bg-water.png`) + dark overlay |
| Display font | Cormorant Garamond |
| Body font | Jost |

**Style:** minimal, feminine, calm — water and botanical aesthetic. Animations include scroll-triggered reveals, ambient drifting orbs, hero entrance stagger, and a breathing glow on the logo.

---

## File Structure

```
index.html                    ← Waiting list / coming soon (LIVE)
home.html                     ← Full website (swap to index.html at launch)
reserve.html                  ← Event reservation / checkout page
style.css                     ← Shared styles across all pages
datenschutz.html              ← Website-level GDPR privacy policy (German)
impressum.html                ← Website-level legal notice

data/
  events.json                 ← Event data reference
  services.json               ← Private services reference

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

## Pages Built

### 1. Waiting List — `index.html` (LIVE at oasiscollective.de)

- Full-screen water background with dark overlay
- Oasis logo + "celebrating sisterhood"
- Intro video (click to play)
- Name + email signup form → Google Forms
- EN/DE language toggle
- Footer: Datenschutz · Impressum · Instagram

### 2. Full Website — `home.html` (local, not yet deployed)

Single-page scrolling site with five sections:

| Section | Content |
|---------|---------|
| **Hero** | Full-screen background, logo, tagline, scroll indicator |
| **Mission** | Intro video, sanctuary description |
| **Calendar** | Monthly events with capacity tracking, expand-on-click details, Reserve buttons |
| **Services** | Private offerings per facilitator with multi-tier pricing |
| **About Us** | Facilitator cards with bios and contact buttons |

**Navigation:** Fixed top bar with logo, section links, DE/EN toggle, and hamburger menu on mobile.

### 3. Reserve Page — `reserve.html`

- Reads event ID from URL (`?event=EVENT_ID`)
- Displays event name, date, time, facilitator, price, spots remaining
- Shows "Sold out" state and hides form when fully booked
- Consent checkbox linking to facilitator-specific legal pages
- "Pay & Reserve" → redirects to Stripe Payment Link

### 4. Facilitator Pages — `facilitators/`

One page per facilitator with:
- Profile header: name, role, bio
- Private services with descriptions, durations, prices
- Book buttons → Stripe Payment Links
- Back link to home

### 5. Legal Pages — `legal/`

Six pages — AGB (Terms & Conditions) + Datenschutz (Privacy Notice) per facilitator. All comply with German law (DDG, DSGVO, MStV).

---

## Events (Placeholder Data)

| Event | Facilitator | Date | Time | Price | Capacity |
|-------|-------------|------|------|-------|----------|
| Opening Ceremony | Thembe | Sat 14 Mar 2026 | 10:00–12:00 | €25 | 20 |
| Sonic Rest & Reset | Thembe | Tue 17 Mar 2026 | 17:00–20:00 | €35 | 15 |
| Sacred Cycle | Steffi | Sat 21 Mar 2026 | 10:00–12:00 | €30 | 12 |
| Tea Lounge | Thembe | Sat 28 Mar 2026 | 10:00–12:00 | €15 | 12 |
| Muse Choir | Thembe | Sat 4 Apr 2026 | 10:00–12:00 | €20 | 20 |

---

## Private Services

### Thembelihle Mchunu

| Service | Duration | Private | Intimate Circle (max 4) | Open Circle (max 10) |
|---------|----------|---------|------------------------|----------------------|
| Reset Ritual | 60 min | €120 | €50 p.p. | €30 p.p. |
| Revive | 30 min | €60 | €30 p.p. | €18 p.p. |
| Guided Meditation | 60 min | €85 | — | €25 p.p. |

### Elisabeth Bernbeck

| Service | Duration | Price |
|---------|----------|-------|
| Gesichtsmassage | 20 min | €15 |
| Nacken / Kopf / Schulter | 30 min | €25 |
| Nacken / Kopf / Schulter | 45 min | €35 |
| Ganzkörpermassage | 60 min | €45 |
| Ganzkörpermassage | 90 min | €65 |
| Deep Relax Psoas | 90 min | €90 |
| Deep Relax Psoas | 120 min | €120 |

### Stefanie Gann

| Service | Duration | Price |
|---------|----------|-------|
| Life Coaching Session | 60 min | €75 |
| Inner Compass Package (4 Sessions) | 4 × 60 min | €260 |

---

## Bilingual Support

All pages support English and German:

- Language toggle on every page (English default)
- `data-en` / `data-de` attributes on all translatable elements
- Language preference saved to `localStorage` (`oasis-lang`)
- Dynamic content (events, services, about) rendered in the active language

---

## Hosting & Deployment

### Current State
- **Waiting list** is live at `oasiscollective.de`
- **Full website** (`home.html`) is built locally — not yet deployed

### Deployment Process
1. Zip the project folder
2. Upload zip to Hostinger File Manager → `public_html`
3. Extract in place
4. At launch: rename `home.html` → `index.html` (replacing the waiting list)

---

## Before Launch — Checklist

- [ ] Replace all placeholder Stripe Payment Links with real ones (events + private services)
- [ ] Add Thembe's email address in services data and legal pages
- [ ] Add Thembe's address in `legal/thembe-datenschutz.html`
- [ ] Add Steffi's address in `legal/steffi-datenschutz.html`
- [ ] Update Instagram URL in footer (currently generic)
- [ ] Update facilitator pages to use inline data (currently use `fetch()`)
- [ ] Confirm actual event capacities with facilitators
- [ ] Add real facilitator photos/portraits
- [ ] Final review of German translations
- [ ] Test all pages on mobile devices
- [ ] Deploy full site and swap `home.html` → `index.html`
