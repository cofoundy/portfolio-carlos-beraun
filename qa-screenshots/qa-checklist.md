# QA Report: Carlos Beraun Mac Long

**Date:** 2026-02-11
**URL:** https://cofoundy.github.io/portfolio-carlos-beraun/
**Status:** FAIL

## Data Validation
- [x] Name matches source: "Carlos Beraun Mac Long" matches Google Sheet exactly
- [x] Email matches source: "cbmaclong@gmail.com" matches Google Sheet exactly
- [x] Title reasonable: "Lawyer | International Business Professional" -- consistent with CV/form data (abogado, 13+ years)
- [x] Companies listed exist in CV: INDECOPI, Diez Canseco Abogados, Ripley -- all from CV
- [x] Education institutions exist in CV: Lambton College (Ontario), UNMSM -- both from CV
- [x] Dates from source: 2017-2024, 2014-2017, 2013, 2023-2025, 2004-2009 -- match CV
- [x] No hallucinated data detected

## Clean Deploy
- [x] No "Powered by" / "Made with" / "Built with" visible text
- [x] No "View source" / "View on GitHub" / "Fork this" template links
- [x] No "Lorem ipsum" / "Your name here" / "[placeholder]" text
- [x] No "undefined" or "null" visible in content
- [ ] **ISSUE: Astro generator meta tag visible in HTML source** -- `<meta name="generator" content="Astro v5.12.3">` (minor, not user-visible)
- [ ] **ISSUE: Programming symbols pattern in hero background** -- `</>, =>, [], <>, (), ::, ==, ++` programming symbols are used as decorative SVG pattern in the hero. This is a developer/tech template artifact. Carlos Beraun is a LAWYER, not a developer. These code symbols are inappropriate for his profession.

## Technical
- [x] CSS loads: HTTP 200 -- `/portfolio-carlos-beraun/_astro/index.DjP8OqGM.css`
- [x] Favicon loads: HTTP 200 -- `/portfolio-carlos-beraun/favicon.svg`
- [ ] **ISSUE: No profile image** -- No `<img>` tags for profile photo found in HTML. The `public/` directory only contains `favicon.svg`. Client submitted a photo via Google Form but it was not included.
- [ ] **ISSUE: No mobile navigation** -- Header uses `hidden md:block`, completely hidden on mobile with no hamburger menu alternative. Mobile users have no navigation.
- [ ] **ISSUE: Escaped HTML in Education degree** -- `<strong>International Business</strong>` in config.ts education degree field renders as literal `&lt;strong&gt;International Business&lt;/strong&gt;` text because Education.astro line 28 uses `{edu.degree}` (text interpolation) instead of `<Fragment set:html={edu.degree} />`. The user sees the raw HTML tags as visible text.
- [x] No critical console errors (Chrome MCP unavailable; no JS errors evident from source analysis)

## Issues Found

### FAIL-1: Escaped HTML tags visible in Education section (CRITICAL)
The education degree for Lambton College renders as literal text:
`<strong>International Business</strong> - Graduate Certificate`
instead of rendering "International Business" in bold.
- **Location:** Education section, first entry
- **Root cause:** `config.ts` line 75 contains `<strong>` tags, but `Education.astro` line 28 renders `{edu.degree}` with text interpolation instead of `set:html`
- **Fix:** Change line 28 in Education.astro to use `<h3 ... set:html={edu.degree} />` OR remove `<strong>` from config.ts degree field

### FAIL-2: Programming symbols background pattern (WRONG PROFESSION)
The hero background contains a decorative SVG pattern with programming symbols: `</>`, `=>`, `[]`, `<>`, `()`, `::`, `==`, `++`, `;`
These are software development symbols. Carlos Beraun is a **lawyer** specializing in consumer protection and international business.
- **Location:** Hero section, SVG pattern `id="programming-symbols"`
- **Fix:** Remove the programming-symbols pattern or replace with profession-appropriate decorative elements (e.g., abstract geometric lines, scales of justice pattern, or clean grid only)

### FAIL-3: No profile photo included
Client uploaded a professional photo via Google Form (`https://drive.google.com/open?id=11X5PvJDb6GusPgwBw-3b9fm5Cl7PiHtc`) but no profile image exists on the deployed site. The `public/` directory only has `favicon.svg`.
- **Fix:** Download client photo, process to `public/profile.jpg`, and add an `<img>` element to the Hero section

### FAIL-4: No mobile navigation
The header navigation (`Header.astro`) uses `class="hidden md:block"` which completely hides the nav on screens below `md` (768px). There is no hamburger menu or alternative mobile navigation.
- **Fix:** Add a mobile hamburger menu with slide-out or dropdown nav for screens below `md` breakpoint

### WARN-1: Astro generator meta tag (MINOR)
`<meta name="generator" content="Astro v5.12.3">` is present. Not user-visible but reveals technology stack.
- **Fix:** Optional. Can remove via Astro config if desired.

## Evidence
- Chrome MCP unavailable for screenshots in this session
- All findings verified via curl HTML extraction and source code analysis
