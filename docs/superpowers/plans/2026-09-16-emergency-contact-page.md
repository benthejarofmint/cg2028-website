# Emergency Contact Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single static, mobile-first emergency contact web page for a fictional elderly resident (Mr. Tan Boon Huat), to be reached by scanning the NFC tag on a fall-detection wearable, and publishable as-is on GitHub Pages.

**Architecture:** Plain static site with three files at the repo root — `index.html` (structure/content), `styles.css` (all styling), `README.md` (project description). No build step, no framework, no backend, no JavaScript (all content is static per spec).

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox), no external dependencies (system font stack, inline SVG avatar, emoji icons).

---

## Note on "tests" for this plan

This is a static content page with no application logic, so there are no unit tests. "Verification" steps instead use `grep` to confirm required content/attributes exist in the markup, and the Browser tool to visually confirm rendering and check for console errors. This replaces the TDD red/green loop for this kind of work.

---

### Task 1: Project README

**Files:**
- Create: `README.md`

- [ ] **Step 1: Write README.md**

```markdown
# Elderly Fall Detection — Emergency Contact Page

A static web page shown when someone scans the NFC tag on a fall-detection
wearable (built on the STM32 B-L4S5I-IOT01A board). It gives a bystander
everything they need to help immediately: who the person is, relevant
medical information, and one-tap ways to call emergency services or the
person's next of kin.

This is a demo for a CG2028 lab project. All personal information on the
page (name, medical details, phone numbers, address) is fictional.

## Structure

- `index.html` — page content and structure
- `styles.css` — all styling

## Running locally

Open `index.html` directly in a browser, or serve the folder with any
static file server, e.g.:

\`\`\`bash
python3 -m http.server 8000
\`\`\`

Then visit `http://localhost:8000`.

## Deploying to GitHub Pages

1. Push this repository to GitHub.
2. In the repo settings, under **Pages**, set the source to the `main`
   branch, root folder.
3. GitHub will publish the page at
   `https://<username>.github.io/<repo-name>/`.
4. Point the NFC tag's stored URL at that address.
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "STM32 B-L4S5I-IOT01A" README.md`
Expected output: `1`

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "docs: add project README"
```

---

### Task 2: HTML page structure and content

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fall Alert — Tan Boon Huat</title>
  <meta name="description" content="Emergency contact information for Tan Boon Huat, shown after a fall-detection wearable alert.">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="alert-banner" role="alert">
    <div class="alert-content">
      <span class="alert-icon" aria-hidden="true">⚠️</span>
      <div class="alert-text">
        <p class="alert-title">Fall Detected</p>
        <p class="alert-subtitle">Detected at 3:42 PM &middot; Please check on them and use the buttons below if needed</p>
      </div>
    </div>
  </div>

  <main>
    <section class="identity-card">
      <div class="avatar" aria-hidden="true">
        <svg viewBox="0 0 24 24" fill="white" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 12c2.7 0 4.9-2.2 4.9-4.9S14.7 2.2 12 2.2 7.1 4.4 7.1 7.1 9.3 12 12 12zm0 2.5c-3.3 0-9.8 1.6-9.8 4.9v2.4h19.6v-2.4c0-3.3-6.5-4.9-9.8-4.9z"/>
        </svg>
      </div>
      <div class="identity-info">
        <h1>Tan Boon Huat</h1>
        <p class="identity-meta">78 years old</p>
        <p class="identity-meta">Wearable Unit #A7-042 &middot; STM32 B-L4S5I-IOT01A</p>
      </div>
    </section>

    <section class="cta-row">
      <a class="btn btn-emergency" href="tel:995">
        <span class="btn-icon" aria-hidden="true">📞</span>
        Call 995
      </a>
      <a class="btn btn-kin" href="tel:+6591234567">
        <span class="btn-icon" aria-hidden="true">👪</span>
        Call Next of Kin
      </a>
    </section>

    <section class="card medical-card">
      <h2>Medical Information</h2>
      <ul class="info-list">
        <li>
          <span class="info-label">🩺 Conditions</span>
          <span class="info-value">Hypertension, Type 2 Diabetes, Mild Osteoarthritis</span>
        </li>
        <li>
          <span class="info-label">⚠️ Allergies</span>
          <span class="info-value">Penicillin</span>
        </li>
        <li>
          <span class="info-label">🩸 Blood Type</span>
          <span class="info-value">O+</span>
        </li>
        <li>
          <span class="info-label">💊 Medications</span>
          <span class="info-value">Metformin, Amlodipine</span>
        </li>
      </ul>
    </section>

    <section class="card kin-card">
      <h2>Next of Kin</h2>
      <div class="contact">
        <div class="contact-info">
          <p class="contact-name">Tan Mei Ling <span class="contact-relation">(Daughter)</span></p>
          <p class="contact-phone">+65 9123 4567</p>
        </div>
        <a class="btn-call" href="tel:+6591234567" aria-label="Call Tan Mei Ling">📞 Call</a>
      </div>
      <div class="contact">
        <div class="contact-info">
          <p class="contact-name">Tan Wei Jie <span class="contact-relation">(Son)</span></p>
          <p class="contact-phone">+65 8234 5678</p>
        </div>
        <a class="btn-call" href="tel:+6582345678" aria-label="Call Tan Wei Jie">📞 Call</a>
      </div>
    </section>

    <section class="card address-card">
      <h2>Home Address</h2>
      <p>Blk 456 Ang Mo Kio Ave 10, #08-123<br>Singapore 560456</p>
    </section>
  </main>

  <footer>
    <p>Demo page for a CG2028 Fall Detection Wearable project</p>
  </footer>
</body>
</html>
```

- [ ] **Step 2: Verify required content is present**

Run:
```bash
grep -c 'href="tel:995"' index.html
grep -c 'href="tel:+6591234567"' index.html
grep -c 'href="tel:+6582345678"' index.html
grep -c "Tan Boon Huat" index.html
grep -c "Penicillin" index.html
grep -c "Ang Mo Kio" index.html
```
Expected output for each: `1`, `2` for the `tel:+6591234567` grep (it appears in both the CTA button and the next-of-kin card), `1` for the rest.

- [ ] **Step 3: Open the page in the browser and confirm it loads cleanly**

Use the Browser tool to navigate to the local `index.html` file (e.g. `file:///Users/benjaminloh/Desktop/nus/Y3S1/cg2028/lab/assignment/emergency_website/index.html`), then check the console for errors.

Expected: page renders unstyled (no `styles.css` yet is fine at this point) with all text content visible, zero console errors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add emergency contact page markup"
```

---

### Task 3: Styling

**Files:**
- Create: `styles.css`

- [ ] **Step 1: Create styles.css**

```css
:root {
  --color-bg: #f4f7f9;
  --color-card-bg: #ffffff;
  --color-primary: #0f6e84;
  --color-text: #1f2937;
  --color-text-muted: #5b6b74;
  --color-alert: #d92d20;
  --color-border: #e3e8eb;
  --radius: 16px;
  --shadow: 0 2px 8px rgba(15, 42, 51, 0.08);
  --font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: var(--font-family);
  background: var(--color-bg);
  color: var(--color-text);
  line-height: 1.5;
}

.alert-banner {
  background: var(--color-alert);
  color: #fff;
  position: sticky;
  top: 0;
  z-index: 10;
  padding: 12px 16px;
}

.alert-content {
  display: flex;
  align-items: center;
  gap: 12px;
  max-width: 480px;
  margin: 0 auto;
}

.alert-icon {
  font-size: 28px;
}

.alert-title {
  margin: 0;
  font-weight: 700;
  font-size: 16px;
}

.alert-subtitle {
  margin: 2px 0 0;
  font-size: 13px;
  opacity: 0.9;
}

main {
  max-width: 480px;
  margin: 0 auto;
  padding: 20px 16px 40px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.identity-card {
  display: flex;
  align-items: center;
  gap: 16px;
  background: var(--color-card-bg);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 20px;
}

.avatar {
  width: 64px;
  height: 64px;
  border-radius: 50%;
  background: var(--color-primary);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.avatar svg {
  width: 36px;
  height: 36px;
}

.identity-info h1 {
  margin: 0 0 4px;
  font-size: 20px;
}

.identity-meta {
  margin: 2px 0;
  font-size: 13px;
  color: var(--color-text-muted);
}

.cta-row {
  display: flex;
  gap: 12px;
}

.btn {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px;
  border-radius: var(--radius);
  font-weight: 700;
  font-size: 16px;
  text-decoration: none;
  box-shadow: var(--shadow);
}

.btn-emergency {
  background: var(--color-alert);
  color: #fff;
}

.btn-kin {
  background: var(--color-primary);
  color: #fff;
}

.card {
  background: var(--color-card-bg);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 20px;
}

.card h2 {
  margin: 0 0 12px;
  font-size: 15px;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  color: var(--color-text-muted);
}

.info-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.info-list li {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  border-bottom: 1px solid var(--color-border);
  padding-bottom: 12px;
  font-size: 14px;
}

.info-list li:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.info-label {
  color: var(--color-text-muted);
  flex-shrink: 0;
}

.info-value {
  text-align: right;
  font-weight: 600;
}

.contact {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid var(--color-border);
}

.contact:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.contact-name {
  margin: 0;
  font-weight: 600;
  font-size: 15px;
}

.contact-relation {
  color: var(--color-text-muted);
  font-weight: 400;
  font-size: 13px;
}

.contact-phone {
  margin: 2px 0 0;
  color: var(--color-text-muted);
  font-size: 13px;
}

.btn-call {
  background: var(--color-primary);
  color: #fff;
  text-decoration: none;
  padding: 8px 14px;
  border-radius: 999px;
  font-size: 13px;
  font-weight: 600;
  white-space: nowrap;
}

.address-card p {
  margin: 0;
  font-size: 14px;
}

footer {
  text-align: center;
  padding: 16px;
  font-size: 12px;
  color: var(--color-text-muted);
}

@media (max-width: 360px) {
  .cta-row {
    flex-direction: column;
  }
}
```

- [ ] **Step 2: Reload the page in the browser at desktop width**

Use the Browser tool to reload the `index.html` file. Take a screenshot.

Expected: sticky red alert banner at top; white identity card with teal circular avatar; two side-by-side call buttons (red "Call 995", teal "Call Next of Kin"); medical info, next-of-kin, and address cards as rounded white cards with soft shadows on a light gray background; footer text centered at the bottom.

- [ ] **Step 3: Resize to mobile width and re-check**

Use the Browser tool's resize/viewport action to set width to 375px (mobile). Reload and screenshot.

Expected: no horizontal scrollbar; all cards remain full-width and readable; call buttons stay side-by-side down to 360px, then stack vertically below that per the `@media (max-width: 360px)` rule.

- [ ] **Step 4: Check browser console for errors**

Use the Browser tool's console-read action.

Expected: zero errors or warnings.

- [ ] **Step 5: Commit**

```bash
git add styles.css
git commit -m "style: add visual design for emergency contact page"
```

---

### Task 4: Accessibility and final verification pass

**Files:**
- Modify (if issues found): `index.html`

- [ ] **Step 1: Verify all three tel: links use valid formats**

Run: `grep -o 'href="tel:[^"]*"' index.html`

Expected output (three unique lines, one repeated):
```
href="tel:995"
href="tel:+6591234567"
href="tel:+6591234567"
href="tel:+6582345678"
```

- [ ] **Step 2: Verify accessibility attributes are present**

Run:
```bash
grep -c 'role="alert"' index.html
grep -c 'aria-label="Call Tan Mei Ling"' index.html
grep -c 'aria-label="Call Tan Wei Jie"' index.html
grep -c 'aria-hidden="true"' index.html
```
Expected output: `1`, `1`, `1`, and `4` or more (decorative icons: alert icon, avatar, two CTA button icons).

- [ ] **Step 3: Verify page metadata**

Run:
```bash
grep -c "<title>Fall Alert" index.html
grep -c 'name="description"' index.html
```
Expected output: `1`, `1`.

- [ ] **Step 4: Take a final full-page screenshot for the record**

Use the Browser tool to screenshot the full page at both desktop and mobile widths, confirming the result matches the design spec at `docs/superpowers/specs/2026-09-16-emergency-contact-page-design.md`.

- [ ] **Step 5: Commit any fixes found during this pass**

If Steps 1–4 required changes to `index.html` or `styles.css`, commit them:

```bash
git add index.html styles.css
git commit -m "fix: address accessibility/verification findings"
```

If no changes were needed, skip this step.

---

## Deployment (manual, not automated by this plan)

This plan produces a working static site locally. Publishing it requires the user's own GitHub account and explicit action:

1. Create a new repository on GitHub (e.g. `emergency-website`).
2. Add it as a remote and push: `git remote add origin <repo-url>` then `git push -u origin main`.
3. In the repo's **Settings → Pages**, set source to the `main` branch, root folder.
4. The page will be live at `https://<username>.github.io/<repo-name>/`.
5. Program the board's NFC tag with that URL.

These steps are not executed as part of this plan — they require the user to create/own the GitHub repository.
