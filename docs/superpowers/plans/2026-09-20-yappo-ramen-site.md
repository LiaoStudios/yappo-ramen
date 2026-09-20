# Yappo Ramen Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and validate a complete responsive one-page website for Yappo — Ramen & Izakaya using verified business information and selected local photographs.

**Architecture:** A dependency-free static site keeps delivery simple and matches the reference project's architecture. `dist/index.html` contains the semantic page, visual system, and small interaction layer; `dist/assets/images/` contains a curated set of renamed local photographs; `tests/site-smoke.mjs` verifies content, accessibility hooks, and local asset integrity. `.openai/hosting.json` declares `dist` as the publishable static directory.

**Tech Stack:** HTML5, modern CSS, vanilla JavaScript, Node.js smoke test, local image assets.

## Global Constraints

- Use the approved warm white, ink black, sand beige, and powder blue palette.
- Preserve the single-page structure and interaction quality of CHE STILE! without copying its salon branding.
- Use only verified business information from Yappo's official site, Google Business profile, and current public menu.
- Use selected photographs already supplied in `GoogleBusiness/`; do not generate replacement restaurant photography.
- Keep the site responsive, keyboard accessible, and dependency-free.
- Main CTA: official booking link. Secondary actions: menu, phone, Google Maps, and Instagram.

---

### Task 1: Asset set and automated smoke test

**Files:**
- Create: `.openai/hosting.json`
- Create: `dist/assets/images/hero-ramen.jpg`
- Create: `dist/assets/images/ramen-spicy.jpg`
- Create: `dist/assets/images/ramen-selection.jpg`
- Create: `dist/assets/images/yakitori.jpg`
- Create: `dist/assets/images/karaage.jpg`
- Create: `dist/assets/images/takoyaki.jpg`
- Create: `dist/assets/images/dessert.jpg`
- Create: `dist/assets/images/interior.jpg`
- Create: `tests/site-smoke.mjs`

**Interfaces:**
- Consumes: original files `GoogleBusiness/yappo_googlebusiness_005.jpg`, `_003.jpg`, `_008.jpg`, `_009.jpg`, `_010.jpg`, `_015.jpg`, `_083.jpg`.
- Produces: stable descriptive image paths used by `index.html`; a Node test that validates the completed page.

- [ ] **Step 1: Write the failing smoke test**

Create `tests/site-smoke.mjs` with assertions that `dist/index.html` exists; includes `lang="it"`, title, description, Restaurant JSON-LD, all required section IDs, booking/menu/telephone/map/Instagram links, mobile-menu ARIA attributes, lightbox dialog semantics, `prefers-reduced-motion`, and at least eight images with non-empty alt text. Extract every local `src` and assert its file exists.

- [ ] **Step 2: Run the test and verify it fails**

Run: `node tests/site-smoke.mjs`

Expected: failure because `dist/index.html` is not present.

- [ ] **Step 3: Copy the selected photographs into stable paths**

Create `.openai/hosting.json` with `{ "static": { "directory": "dist" } }`. Copy the chosen source images into `dist/assets/images/` with the exact names above. Use `sips -Z 1800` on copied files only when a long edge exceeds 1800 pixels; keep original source files unchanged.

- [ ] **Step 4: Commit the test and curated assets**

Run:

```bash
git add .openai/hosting.json tests/site-smoke.mjs dist/assets/images
git commit -m "test: define Yappo site acceptance checks"
```

### Task 2: Semantic page and visual system

**Files:**
- Create: `dist/index.html`

**Interfaces:**
- Consumes: descriptive files from `dist/assets/images/`.
- Produces: anchors `#storia`, `#menu`, `#esperienza`, `#galleria`, and `#contatti`; reusable `.btn`, `.section`, `.eyebrow`, `.display`, `.reveal`, and `.gallery-item` classes; DOM hooks `navToggle`, `mobileMenu`, `lightbox`, `lightboxImage`, `lightboxCaption`, `lightboxPrev`, `lightboxNext`, and `lightboxClose`.

- [ ] **Step 1: Build the document metadata and structured data**

Add Italian metadata, theme color, canonical business copy, and `Restaurant` JSON-LD containing the verified name, phone `+39 051 040 0065`, address `Via Emilia 169C, 40068 San Lazzaro di Savena BO`, price range `€€`, cuisine type, and opening hours Monday–Tuesday and Thursday–Sunday `12:00–15:00` / `19:00–23:00`, closed Wednesday.

- [ ] **Step 2: Implement the global visual system**

Define CSS tokens `--paper:#f7f4ee`, `--ink:#101113`, `--sand:#ddd2c2`, `--sky:#b9d6df`, `--sky-deep:#769dab`, borders, spacing, type scale, maximum width, focus states, and reduced-motion overrides. Use a warm editorial layout with asymmetric image crops, fine rules, rounded cards only where hierarchy requires them, and no decorative gradients.

- [ ] **Step 3: Implement navigation, hero, and facts strip**

Create a sticky desktop navigation and collapsed mobile navigation; a split hero using `hero-ramen.jpg`; title “Yappo” with “Ramen & Izakaya”; main booking CTA `https://pnssm.pro/4ehzlqm`; secondary menu CTA to the current TheFork menu; and a facts strip for contemporary Japanese cuisine, San Lazzaro, average price €20, and service hours.

- [ ] **Step 4: Implement story, signature dishes, and experience sections**

Use verified copy about Yappo's Bologna origins, its move from Giardini Margherita, and its mix of ramen, yakisoba, rice, modern starters, and Japanese street food. Add menu cards for Yappo Ramen (€16), Tantanmen (€15), Chashu Ramen (€13.90), Yakitori (€8), Karaage (€5.50), and Takoyaki (€5.50). Add a dark “brodo, fuoco, convivialità” section with concise factual descriptions.

- [ ] **Step 5: Implement gallery, location, CTA, and footer**

Create an eight-image editorial gallery; location and hours blocks; phone, Maps, Instagram, and booking links; a final CTA; and a compact footer. Every informative image receives a descriptive Italian alt attribute and explicit dimensions where known.

- [ ] **Step 6: Run the smoke test to expose missing interaction hooks**

Run: `node tests/site-smoke.mjs`

Expected: metadata, content, section, link, and asset checks pass; any interaction-specific assertions may still fail until Task 3.

- [ ] **Step 7: Commit the complete static layout**

Run:

```bash
git add dist/index.html
git commit -m "feat: build Yappo Ramen landing page"
```

### Task 3: Interaction and accessibility behavior

**Files:**
- Modify: `dist/index.html`
- Modify: `tests/site-smoke.mjs`

**Interfaces:**
- Consumes: DOM hooks created in Task 2.
- Produces: mobile navigation behavior; sticky-nav state; reveal animation; accessible gallery lightbox with keyboard navigation and focus restoration; dynamic copyright year.

- [ ] **Step 1: Add interaction assertions before implementation**

Extend the smoke test to require handlers for mobile menu toggling, Escape, ArrowLeft, ArrowRight, lightbox focus restoration, `IntersectionObserver`, and dynamic year output.

- [ ] **Step 2: Run the test and verify the new assertions fail**

Run: `node tests/site-smoke.mjs`

Expected: failure naming the first missing interaction.

- [ ] **Step 3: Implement mobile navigation and reveal behavior**

Toggle `aria-expanded`, `.open`, and document scroll state from `navToggle`; close after a mobile link selection; add shrink state after scrolling; use `IntersectionObserver` for `.reveal`, with an immediate visible fallback when unsupported.

- [ ] **Step 4: Implement the accessible lightbox**

Open from `.gallery-item`; update image, caption, and count; navigate with buttons and arrow keys; close with Escape, the close button, or backdrop click; trap focus within controls; and restore focus to the originating gallery item.

- [ ] **Step 5: Run final automated checks**

Run: `node tests/site-smoke.mjs`

Expected: `All Yappo site checks passed.`

- [ ] **Step 6: Commit interaction behavior**

Run:

```bash
git add dist/index.html tests/site-smoke.mjs
git commit -m "feat: add accessible Yappo site interactions"
```

### Task 4: Local serving, responsive verification, and delivery

**Files:**
- Modify: `dist/index.html` only if verification exposes a concrete defect.

**Interfaces:**
- Consumes: completed static site.
- Produces: verified local website and, where the Sites environment supports it, a hosted preview.

- [ ] **Step 1: Start a local server**

Run: `python3 -m http.server 4173 --bind 127.0.0.1`

Expected: server listens on `http://127.0.0.1:4173/`.

- [ ] **Step 2: Verify HTTP delivery and asset references**

Run: `curl -fsS http://127.0.0.1:4173/ >/dev/null` and request each local image referenced in `index.html`.

Expected: every request returns successfully.

- [ ] **Step 3: Verify representative desktop and mobile layouts**

Inspect the page at desktop and mobile widths only if browser testing is explicitly authorized; otherwise rely on CSS breakpoint review and automated integrity checks as required by the Sites workflow.

- [ ] **Step 4: Run the complete check one final time**

Run: `node tests/site-smoke.mjs`

Expected: `All Yappo site checks passed.`

- [ ] **Step 5: Commit verification fixes if any**

Run:

```bash
git add dist/index.html tests/site-smoke.mjs
git commit -m "fix: polish responsive Yappo presentation"
```
