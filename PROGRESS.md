# Portfolio — Development Progress

Last updated: 2026-05-31  
Live URL: https://d13be0ebbetbkk.cloudfront.net  
Hosting: S3 bucket `maazm-portfolio` (us-west-1) behind CloudFront distribution `E1ET99LYU58P7T`

Deploy command:
```bash
aws s3 sync /home/maaz/personal-website/ s3://maazm-portfolio/ --delete --exclude ".git/*" --exclude "README.md" --exclude "PROGRESS.md"
aws cloudfront create-invalidation --distribution-id E1ET99LYU58P7T --paths "/*"
```

---

## Current State

The site is a dark, grid-operations themed portfolio. Design direction: **Modern-Minimal + Tech-Utility** — Space Grotesk headings, JetBrains Mono for all data/telemetry values, electric green (#22c55e) as the single signal accent, hairline borders.

### Sections (top to bottom)

| Section | Status | Notes |
|---|---|---|
| Nav | Done | Hamburger menu on mobile; links to all sections |
| Hero | Done | Outcome-driven headline, 3 CTAs (View Projects / Launch CAISO Dashboard / Contact), animated 60Hz waveform viz |
| Grid Control Center | Done | 5 live telemetry cards with sparklines (freq, load, renewable %, BESS SOC, LMP · NP15). Horizontal scroll on mobile ≤600px. Control bar shows source badge + live timestamp |
| Projects | Done | CAISO as FLAGSHIP (Problem/Approach/Outcome structure, prominent Launch button). EMS and AWS as secondary. Other Projects at bottom |
| Experience | Done | UmmahSoft (React Native intern), KiloWatts for Humanity, Masjid Muhajireen |
| Engineering Stack | Done | Renamed from "Skills". Columns: Grid Modeling / Software & Data / Infrastructure |
| About | Done | Stats updated to domain-specific: SJSU / 3+ Grid Projects / CAISO / BESS |
| Contact | Done | Email, LinkedIn, GitHub cards |

### Key design decisions made this session
- Font: Inter → Space Grotesk (less generic, better letterforms)
- Tags: removed green-tinted backgrounds → neutral border only
- Card hover: removed vertical lift (translateY anti-pattern) → border highlight + background shift
- Hero CTAs: generic GitHub/LinkedIn/email → View Projects / Launch CAISO Dashboard / Contact
- CAISO hub corrected from NP26 (made up) → NP15 (correct for San Jose / PG&E territory)
- LMP 24h chart updated to show real duck curve with negative midday prices (curtailment in blue)
- Telemetry frequency range tightened to ±0.05 Hz (NERC normal operations)
- Avg LMP stat corrected from $52 → $38/MWh (actual mean of duck curve profile)

---

## What's Next

### High priority
- [ ] **Resume download button** — add to hero or contact section; host PDF on S3
- [ ] **Mobile nav refinement** — current hamburger works but could use a close animation
- [ ] **EMS Simulator project page** — `projects/ems/index.html` exists but content is sparse; build it out with the dispatch algorithm explanation and simulation output charts
- [ ] **CAISO flagship preview image** — replace the canvas LMP chart with an actual screenshot of the live dashboard so visitors see it before clicking

### Medium priority
- [ ] **Scroll progress indicator** — thin green line at the top of the viewport showing scroll position
- [ ] **"Now" section or status line** — one line below the hero showing what you're currently working on / learning
- [ ] **Grid topology SVG** — replace or complement the sine wave hero viz with a simple node-edge power grid diagram
- [ ] **Open graph / social preview** — add og:image, og:title, og:description meta tags for LinkedIn share previews

### Low priority / stretch
- [ ] Add a writing/notes section if you start publishing technical posts about CAISO, LMP, or grid software
- [ ] Dark/light mode toggle (preserve current dark as default)
- [ ] Add smooth page transition on external link click (brief fade before navigating)

---

## File Structure

```
personal-website/
├── index.html         Main single-page portfolio
├── style.css          All styles (Space Grotesk, dark theme, responsive)
├── script.js          Telemetry simulation, charts, nav, animations
├── projects/
│   └── ems/
│       └── index.html EMS Simulator architecture page (sparse — needs work)
├── PROGRESS.md        This file
└── README.md          Deployment instructions
```

## Design Reference

The design was informed by three resources researched this session:
- **sboghossian/design-skill** — anti-slop rules (no Inter everywhere, no purple gradients, mono only for data)
- **sonhaicoder/web-taste-skill** — Modern-Minimal direction (greyscale + single saturated accent, Linear/Vercel aesthetic)
- **Emil Kowalski** — intentional microinteractions, content at rest, precise hover feedback
