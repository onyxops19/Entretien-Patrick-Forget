# EPF Three-Page Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce three linked HTML files (index.html, realisations.html, contact.html) in the project root that form a complete, navigable site for Entretien Patrick Forget.

**Architecture:** Pure HTML/CSS/JS — no build step, no framework. Each page is a self-contained file sharing the same design system (CSS vars, fonts, navbar, footer). Pages cross-link via relative hrefs.

**Tech Stack:** HTML5, CSS3, vanilla JS, Leaflet.js (map on index), Google Fonts (Montserrat + Cormorant Garamond)

---

### Task 1: Build index.html

**Files:**
- Source: `.superpowers/brainstorm/11559-1777862174/content/epf-design-v3.html`
- Create: `index.html`

- [ ] **Step 1: Copy v3 source to index.html**

```bash
cp /Users/markbenyaminian/Desktop/entretien-patrick-forget/.superpowers/brainstorm/11559-1777862174/content/epf-design-v3.html \
   /Users/markbenyaminian/Desktop/entretien-patrick-forget/index.html
```

- [ ] **Step 2: Update `<title>`**

Change:
```html
<title>EPF — Design Preview v3</title>
```
To:
```html
<title>Entretien Patrick Forget — Nettoyage & Entretien HVAC, Drummondville</title>
```

- [ ] **Step 3: Remove the preview banner**

Remove this block entirely:
```html
<div class="preview-banner">...</div>
```
And remove its CSS:
```css
/* ── PREVIEW BANNER ── */
.preview-banner { ... }
```

- [ ] **Step 4: Update navbar links**

Replace the `<ul class="nav-links">` block with:
```html
<ul class="nav-links">
  <li><a href="#services">Services</a></li>
  <li><a href="realisations.html">Réalisations</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
```
Update the logo href from `href="#"` to `href="index.html"`.

- [ ] **Step 5: Update hero CTAs to point to contact page**

Find the hero CTA buttons and update the soumission link:
```html
<a href="contact.html" class="btn-white-solid">Obtenir une soumission</a>
```

- [ ] **Step 6: Update dark CTA section link**

Find any `href="#contact"` anchor pointing to the contact section and change it to `href="contact.html"`.

- [ ] **Step 7: Verify in browser**

Open `index.html` in a browser. Confirm:
- No blue preview banner
- Navbar links: Services (scrolls), Réalisations (→ realisations.html), Contact (→ contact.html)
- Map loads (Leaflet)
- All scroll animations work

---

### Task 2: Build realisations.html

**Files:**
- Source: `.superpowers/brainstorm/11559-1777862174/content/nos-realisations.html`
- Create: `realisations.html`

- [ ] **Step 1: Copy nos-realisations source**

```bash
cp /Users/markbenyaminian/Desktop/entretien-patrick-forget/.superpowers/brainstorm/11559-1777862174/content/nos-realisations.html \
   /Users/markbenyaminian/Desktop/entretien-patrick-forget/realisations.html
```

- [ ] **Step 2: Update `<title>`**

Change whatever title is there to:
```html
<title>Nos Réalisations — Entretien Patrick Forget</title>
```

- [ ] **Step 3: Remove preview banner if present**

If the file has a `.preview-banner` div and its CSS, remove both.

- [ ] **Step 4: Update navbar links**

Replace the `<ul class="nav-links">` (or equivalent nav) with:
```html
<ul class="nav-links">
  <li><a href="index.html#services">Services</a></li>
  <li><a href="realisations.html">Réalisations</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
```
Update logo href to `href="index.html"`.

- [ ] **Step 5: Update any CTA buttons linking to soumission/contact**

Any button/link with `href="#contact"` or similar → change to `href="contact.html"`.

- [ ] **Step 6: Verify in browser**

Open `realisations.html`. Confirm:
- Navbar logo goes to index.html
- Filter tabs work (Tout / Thermopompe / Conduit / Échangeur / Système)
- Gallery renders, lightbox opens on click, arrow keys + ESC work
- Contact CTA links to contact.html

---

### Task 3: Build contact.html

**Files:**
- Reference design: `.superpowers/brainstorm/14287-1777942749/content/contact-design.html`
- Create: `contact.html`

- [ ] **Step 1: Copy approved contact design**

```bash
cp /Users/markbenyaminian/Desktop/entretien-patrick-forget/.superpowers/brainstorm/14287-1777942749/content/contact-design.html \
   /Users/markbenyaminian/Desktop/entretien-patrick-forget/contact.html
```

- [ ] **Step 2: Update `<title>`**

```html
<title>Contact & Soumission — Entretien Patrick Forget</title>
```

- [ ] **Step 3: Remove preview label**

Remove:
```html
<div class="preview-label">EPF — Page Contact · Aperçu design</div>
```
And its CSS `.preview-label { ... }`.

- [ ] **Step 4: Update navbar links**

Replace nav-links with:
```html
<ul class="nav-links">
  <li><a href="index.html#services">Services</a></li>
  <li><a href="realisations.html">Réalisations</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
```
Update logo href to `href="index.html"`.

- [ ] **Step 5: Add navbar scroll JS**

The contact page needs the navbar scroll behaviour. Add at bottom of `<body>` before `</body>`:
```html
<script>
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 80);
}, { passive: true });
</script>
```
Also add `id="navbar"` to the `<nav>` element.

- [ ] **Step 6: Add scroll reveal JS**

Add after the navbar scroll script:
```html
<script>
const revealEls = document.querySelectorAll('.reveal, .reveal-left, .reveal-right');
const revealObs = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); revealObs.unobserve(e.target); }
  });
}, { threshold: 0.1 });
revealEls.forEach(el => revealObs.observe(el));
</script>
```

- [ ] **Step 7: Add mobile sticky CTA (matching index.html)**

Before `</body>`, add the mobile sticky bar present in index.html:
```html
<div class="mobile-sticky">
  <a href="tel:8199678926">Appeler maintenant — (819) 967-8926</a>
</div>
```
And copy the `.mobile-sticky` CSS from index.html into contact.html's `<style>` block.

- [ ] **Step 8: Verify in browser**

Open `contact.html`. Confirm:
- No preview label
- Navbar scrolls to dark+blur on scroll
- HVAC photo loads, dark overlay renders
- Form card is visible, centered, all 5 fields present
- Coordonnées strip shows phone, email, hours
- Logo/nav links navigate correctly
- Mobile sticky bar visible on narrow viewport

---

### Task 4: Cross-link verification

- [ ] **Step 1: Open index.html and navigate to all pages**

Click: Réalisations → lands on realisations.html ✓
Click: Contact → lands on contact.html ✓
Click logo on each page → returns to index.html ✓

- [ ] **Step 2: Check phone CTA on all pages**

Click `(819) 967-8926` nav CTA on each page → triggers `tel:` link ✓

- [ ] **Step 3: Serve locally to avoid CORS issues with Leaflet**

```bash
cd /Users/markbenyaminian/Desktop/entretien-patrick-forget && python3 -m http.server 8080
```

Open http://localhost:8080 and re-verify the map loads on index.html.
