# Plan: Rebuild airwayclinic.se

## Goal
Rebuild the Airway Clinic website from the current GHL-hosted basic layout into a stunning, modern, mobile-first static site — keeping all existing content, deployed for free, with the AI chatbot widget integrated.

## Current State
- **Hosted on:** GoHighLevel (GHL) funnel/website builder
- **Domain:** airwayclinic.se
- **Current look:** Basic GHL template — text-heavy, no visual hierarchy, bland styling, weak mobile experience
- **Content:** Rich medical content (7 services, 2 team members, testimonials, contact form, bilingual EN/SE)
- **Existing integrations:** GHL contact form, GHL review widget, AI chatbot (CF Worker), intake survey form

## What We Keep
- All medical copy (services, team bios, philosophy, testimonials)
- Contact form (GHL embed or rebuild as static → GHL webhook)
- Bilingual support (English + Swedish)
- Google Maps embed (Sveavägen 91, Stockholm)
- AI chatbot widget (already deployed)
- GHL tracking code for lead capture
- Review/testimonial content

## Proposed Design

### Style: Custom blend — medical premium meets Scandinavian minimal
Not picking one of the 54 templates directly. Airway Clinic is a **medical clinic**, not a plumber — the design needs to feel:
- **Trustworthy & clinical** (clean whites, precise typography)
- **Warm & human** (not cold/hospital-like)
- **Scandinavian** (lots of whitespace, natural tones, simplicity)
- **Premium** (like a private specialist clinic)

### Color Palette
- **Primary:** Deep teal/green `#0d7377` (medical trust, breathing/airway association)
- **Accent:** Warm gold `#c8963e` (premium, warmth)
- **Backgrounds:** White `#ffffff` + soft cream `#faf8f5` (warmth, not sterile)
- **Text:** Charcoal `#1a1a2e` (softer than pure black)
- **Dark sections:** Slate `#1a1a2e` (footer, CTA)

### Typography
- **Primary:** DM Sans (clean, modern, medical-friendly)
- **Headings:** Playfair Display or similar serif (premium, editorial)
- **Body:** 16-18px, generous line-height (1.6-1.7) for readability

## Site Structure (10 sections, single page)

### 1. Navbar (sticky)
- Airway Clinic logo/text mark
- Nav links: Services · About · Team · Contact
- Language toggle: EN | SV
- "Book Consultation" CTA button
- Mobile hamburger menu

### 2. Hero
- **Headline:** "Because breathing matters" or "Gentle, guided natural improvements"
- **Subtext:** One-liner about holistic airway dentistry
- **CTA:** Book Consultation + Learn More
- **Visual:** Subtle animated background (soft gradient, breathing/pulsing effect)
- **Trust badges:** 30+ Years · Stockholm · Holistic Approach

### 3. Philosophy Strip
- Narrow band: "We don't just treat symptoms. We find the functional cause."
- Subtle pattern or texture background

### 4. Services (7 cards)
- **Grid layout** (not plain list like current)
- Each card: icon + title + short description + "Learn more" link
- Card hover: subtle lift + teal border highlight
- Services:
  1. Growth Guidance Programs (*"Because children can't wait"*)
  2. Myofunctional Therapy
  3. Airway & Sleep Optimisation
  4. ALF Therapy
  5. Jaw Functional Orthopaedics (JFO)
  6. TMJ & Facial Pain Treatment
  7. General Dental Care
- Each "Learn more" could expand inline or scroll to a dedicated section

### 5. Why Airway Clinic (dark section)
- Stats/highlights:
  - 30+ years experience
  - Holistic approach
  - Multi-specialist team
  - Patients from 3 countries
- Background: slate dark with subtle geometric pattern

### 6. Team (2 profiles)
- **Dr. Sia** — Photo + bio + credentials + ALF training note
- **Jessica Gorlee** — Photo + bio + OMFT certification
- Side-by-side cards with warm styling

### 7. Testimonials
- 3 testimonial cards (rotating or static grid)
- Star rating visual
- Quote + attribution
- GHL review widget could be embedded here instead

### 8. CTA Banner
- "Start Your Journey to Better Breathing"
- Book Consultation button
- Warm gradient background (teal to dark)

### 9. Contact (split layout)
- Left: Contact form (GHL embed or static form → GHL webhook)
  - Bilingual toggle note: "(Du kan också fylla i det här formuläret på svenska)"
  - Fields: First Name, Last Name, Phone, Email, Main Concerns, Consent checkboxes
- Right: Map embed + address + phone + email
- Opening hours if available

### 10. Footer
- Multi-column: Services, About, Contact
- Privacy Policy | Terms of Service links
- "Website by Cloud Hak" credit
- Bilingual footer note

### 11. Chatbot Widget (floating)
- Already deployed CF Worker
- Embed widget JS/CSS
- Positioned bottom-right, above mobile CTA

### 12. Mobile Sticky CTA
- "Book Consultation" floating bar at bottom on mobile
- Appears after scrolling past hero

## Technical Approach

### Stack
- **Static HTML/CSS/JS** — no WordPress, no framework
- **Hosted on:** GitHub Pages (free, fast, SSL included)
- **DNS:** Point airwayclinic.se to GitHub Pages (or keep GHL + iframe redirect during transition)

### Build Method
- **GLM-5.1 builds the site** (it's a family clinic, quality matters)
- Single `index.html` with inline CSS and JS
- Swedish version as `index-sv.html` (or JS-based language toggle)

### Bilingual Strategy
**Option A (recommended):** Single page with JS language toggle
- All EN text in data attributes, JS swaps to SV on toggle
- URL stays the same, cleaner UX
- SEO: add `hreflang` tags

**Option B:** Two separate pages
- `index.html` (English) + `sv.html` (Swedish)
- Simpler build, better SEO per language

### GHL Integration
- Keep the GHL contact form as an iframe embed OR rebuild as static form that POSTs to GHL webhook
- GHL tracking code snippet in `<head>` for lead attribution
- Review widget embedded in testimonials section

### SEO
- Schema.org LocalBusiness + Dentist JSON-LD
- Proper meta tags, Open Graph
- Semantic HTML throughout
- `hreflang` for bilingual

## Migration Plan
1. Build new site on GitHub Pages (staging URL)
2. Nima reviews and approves
3. Point airwayclinic.se DNS to GitHub Pages
4. Keep GHL account active for lead pipeline, forms, and CRM
5. Old GHL site becomes unnecessary for web presence

## Files to Create
```
~/projects/airwayclinic-se/
├── .github/workflows/deploy.yml
├── .nojekyll
├── index.html          # Main site (English)
├── index-sv.html       # Swedish version (if Option B)
├── chat-widget.css     # Chatbot styles
├── chat-widget.js      # Chatbot scripts
└── README.md
```

## Open Questions for Nima
1. **Photos** — Do you have professional photos of Dr. Sia and Jessica? Or should we use placeholder stock photos for now?
2. **Language** — Should the Swedish version be a separate page or a JS toggle? (I recommend JS toggle for simplicity)
3. **Booking** — Should "Book Consultation" go to the GHL form, a phone call, or a separate booking page?
4. **Form** — Keep GHL embedded form or rebuild as static + webhook?
5. **Design direction** — Does the teal/gold/cream palette feel right, or would you prefer something different? I can mock up 2-3 color options.

## Estimated Build Time
- **Phase 1 (Core site):** 1-2 hours on GLM-5.1
- **Phase 2 (Bilingual + GHL integration):** 30 min
- **Phase 3 (Chatbot widget + testing):** 30 min
- **Phase 4 (DNS migration):** 15 min + DNS propagation

## Risks
- **DNS migration** — Need to coordinate with whoever manages airwayclinic.se domain registrar
- **GHL form embed** — May need CORS headers or iframe workarounds
- **SEO disruption** — Brief dip during DNS switch, mitigated by keeping same content/structure
