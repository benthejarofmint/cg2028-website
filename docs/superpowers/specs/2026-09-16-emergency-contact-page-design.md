# Emergency Contact Page — Design Spec

Date: 2026-09-16

## Background

This is a companion website for a CG2028 lab project: an elderly wearable
built on the STM32 B-L4S5I-IOT01A board that detects falls. When a fall is
detected, the board's NFC tag can be scanned by anyone nearby, opening this
website. The site's job is to give that bystander everything they need to
help immediately — who the person is, what's medically relevant, and how to
reach emergency services or family.

The site is published on GitHub Pages under the user's personal free GitHub
account. All personal data on the page is fictional, invented for this demo.

## Scope

A single static HTML page. No backend, no build step, no external API keys.
Out of scope: any other page (about the project, team, hardware) — this is
purely the emergency contact page reached via NFC scan.

## Content (fictional profile)

**Elderly resident**
- Name: Mr. Tan Boon Huat
- Age: 78
- Address: Blk 456 Ang Mo Kio Ave 10, #08-123, Singapore 560456
- Device: STM32 B-L4S5I-IOT01A wearable, Unit ID #A7-042

**Medical info**
- Conditions: Hypertension, Type 2 Diabetes, Mild Osteoarthritis
- Allergies: Penicillin
- Blood type: O+
- Current medications: Metformin, Amlodipine

**Next of kin**
- Primary: Ms. Tan Mei Ling (Daughter) — +65 9123 4567
- Secondary: Mr. Tan Wei Jie (Son) — +65 8234 5678

All phone numbers are fictional Singapore-format mobile numbers and are not
real, working numbers.

## Layout (single page, mobile-first)

Order top to bottom:

1. **Alert banner** (sticky top) — "⚠ Fall Detected" with a static demo
   timestamp and a short instruction line ("Please check on them and use the
   buttons below if needed"). Red/orange, high contrast.
2. **Identity card** — illustrated avatar (CSS/SVG, no real photo), name,
   age, device/unit ID.
3. **Call-to-action row** — two large tap-friendly buttons:
   - "Call 995" — `tel:995` link, most visually prominent (red), since this
     is the life-threatening-emergency action.
   - "Call Next of Kin" — `tel:+6591234567` link, secondary prominence
     (blue/teal).
4. **Medical info card** — conditions, allergies, blood type, medications,
   each with a small icon label for fast scanning under stress.
5. **Next-of-kin card** — primary and secondary contact, each showing
   name, relationship, phone number, and its own click-to-call button.
6. **Home address card** — address as text only. No embedded map (avoids
   external map API/key dependency for a static GitHub Pages demo).
7. **Footer** — one line: "Demo page for CG2028 Fall Detection Wearable
   project" plus a GitHub repo link placeholder.

## Visual design

Clean medical/health-tech aesthetic:
- Background: white / light gray
- Primary accent: teal/blue
- Red reserved only for the alert banner and the 995 button, so it doesn't
  compete with the rest of the page
- Rounded cards with soft shadows
- System font stack (no external font dependency)
- Large touch targets throughout — this page will typically be opened on a
  phone by someone in a stressful, time-pressured situation

## Alert data

Static demo content only: a fixed "Fall detected" message with a sample
timestamp, styled as an urgent banner. No live data from the board (this is
a static GitHub Pages site with no backend).

## Technical approach

Plain static site, no framework, no build step:
- `index.html` — page structure and content
- `styles.css` — all styling
- `script.js` — optional; only needed if a small enhancement (e.g. relative
  "X minutes ago" timestamp) is added. Can be omitted if unnecessary.

Deployed via GitHub Pages directly from the repository (root or `/docs`,
decided at implementation time based on repo layout).

**Alternative considered:** a single self-contained `index.html` with inline
CSS/JS. Rejected in favor of separate files for readability and
maintainability, since deployment complexity is identical either way for
GitHub Pages.

## Out of scope / explicitly excluded

- No embedded map or geolocation
- No live/dynamic data feed from the STM32 board
- No additional pages (about-the-project, team, hardware details)
- No real personal data — all names, numbers, and addresses are fictional
