# QA Report: Marylin Camila Mamani Zaciga

**Date:** 2026-02-11
**URL:** https://cofoundy.github.io/portfolio-marylin-mamani/
**Status:** FAIL

## Data Validation
- [x] Name matches source (Sheet: "MARYLIN CAMILA MAMANI ZACIGA" -> page: "Marylin Camila Mamani Zaciga" -- proper case, acceptable)
- [x] Email matches source (marylinzaciga@gmail.com)
- [x] Title consistent with source (Analista de Datos | Estadistica UNMSM -- matches 5to ciclo Estadistica)
- [x] LinkedIn URL matches source (linkedin.com/in/marylin-mamani-zaciga-36901337b)
- [x] Companies listed are real organizations (Inmobiliaria Noa S.A.C., UNMSM, INEI, IEEE CIS)
- [x] Education institutions are real (UNMSM, Sistemas UNI, CINFO UNMSM, PUCP, ICPNA)
- [x] No hallucinated data detected

## Clean Deploy
- [x] No "Powered by" / "Made with" / "Built with" visible text
- [x] No "View source" / "View on GitHub" / "Fork this" template links
- [x] No "Lorem ipsum" / "Your name here" / "[placeholder]" text
- [x] No template watermarks visible to users
- [x] No "undefined" or "null" visible in content
- [ ] **FAIL: Ghost social links in footer** -- Twitter and GitHub icons render as `<a>` tags with NO href attribute (empty links). Client has no Twitter or GitHub configured. Footer.astro lacks conditional rendering for these icons.

## Technical
- [x] Page loads (HTTP 200)
- [x] CSS loads (HTTP 200 -- _astro/index.op7F8SrS.css)
- [x] Favicon loads (HTTP 200 -- favicon.svg with "MM" initials, #1e40af background)
- [x] Profile image file loads (HTTP 200 -- profile.jpg exists in public/)
- [ ] **FAIL: Profile photo NOT displayed on page** -- The hero component does not include an `<img>` tag for the profile photo. The file exists at /profile.jpg and returns HTTP 200, but it is never referenced in any component. For a Pro tier (S/.120) with "Foto profesional" submitted, this is a significant omission.
- [ ] **FAIL: No mobile navigation** -- Header uses `hidden md:block`, completely hiding navigation on screens below 768px. No hamburger menu or mobile alternative exists.
- [x] astro.config.mjs has both site + base correctly set
- [ ] Console errors: Unable to verify (Chrome MCP unavailable)
- [ ] Screenshots: Unable to capture (Chrome MCP unavailable)

## Issues Found

### ISSUE 1 (HIGH): Ghost Social Links in Footer
- **Location:** Footer.astro, lines 73-120
- **Problem:** Twitter (`<a>` line 73) and GitHub (`<a>` line 97) icons render unconditionally, without checking if `siteConfig.social.twitter` or `siteConfig.social.github` exist. Config only has `email` and `linkedin`. The deployed HTML shows `<a target="_blank" rel="noopener noreferrer" aria-label="Twitter">` with NO href.
- **Impact:** Two clickable icons in the footer that link to nothing. Looks broken/unprofessional.
- **Fix:** Add conditional rendering in Footer.astro: `{siteConfig.social?.twitter && (...)}` and `{siteConfig.social?.github && (...)}` (same pattern already used in Hero.astro).

### ISSUE 2 (HIGH): Profile Photo Not Displayed
- **Location:** Hero.astro
- **Problem:** The component does not include any `<img>` element for the profile photo. The file `public/profile.jpg` exists and loads correctly at the deployed URL, but no component references it.
- **Impact:** Client submitted a professional photo (Pro tier S/.120 includes photo integration), but it is invisible on the portfolio. The hero section is text-only.
- **Fix:** Add profile photo to Hero.astro (e.g., 2-column layout with photo, or centered photo above the name).

### ISSUE 3 (MEDIUM): No Mobile Navigation
- **Location:** Header.astro, line 10 (`class="... hidden md:block ..."`)
- **Problem:** The desktop nav is hidden below md breakpoint (768px). No hamburger menu or mobile nav exists anywhere on the page.
- **Impact:** Mobile visitors have no navigation bar. They can only scroll to find sections. For a Pro tier this is below expectations.
- **Fix:** Add a hamburger menu component for mobile, or make the nav visible on all screen sizes with a different layout.

### ISSUE 4 (LOW): HTML Nesting -- Extra Section Wrapper
- **Location:** index.astro, line 30
- **Problem:** A `<section>` wraps Hero through Education, creating 5 opening `<section>` tags but only 4 closing ones in the rendered HTML. While browsers auto-correct this, it is semantically incorrect.
- **Impact:** No visual impact, but may cause issues with accessibility tools.
- **Fix:** Remove the wrapper `<section>` in index.astro or convert to a `<main>` element.

## Evidence
- Screenshots: NOT captured (Chrome MCP server was unavailable during QA)
- HTML source: Verified via curl (full page fetched and analyzed)
- HTTP headers: All verified via curl -sI

## Source Data Cross-Reference
| Field | Google Sheet | Config.ts | Deployed Page | Match |
|-------|-------------|-----------|---------------|-------|
| Name | MARYLIN CAMILA MAMANI ZACIGA | Marylin Camila Mamani Zaciga | Marylin Camila Mamani Zaciga | YES |
| Email | marylinzaciga@gmail.com | marylinzaciga@gmail.com | marylinzaciga@gmail.com | YES |
| LinkedIn | linkedin.com/in/marylin-mamani-zaciga-36901337b/ | linkedin.com/in/marylin-mamani-zaciga-36901337b | linkedin.com/in/marylin-mamani-zaciga-36901337b | YES |
| Title | (from CV/notes) | Analista de Datos / Estadistica UNMSM | Analista de Datos / Estadistica UNMSM | YES |
| Accent Color | AZUL ELEGANTE | #1e40af (navy blue) | #1e40af | YES |
