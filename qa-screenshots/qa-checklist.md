# QA Report: Carlos Beraun Mac Long

**Date:** 2026-02-06
**URL:** https://cofoundy.github.io/portfolio-carlos-beraun/
**Status:** FAIL

## Data Validation
- [x] Name matches source (Sheet: "Carlos Beraun Mac Long" / Site: "Carlos Beraun Mac Long")
- [x] Email matches sheet (`cbmaclong@gmail.com`)
- [x] Job title reasonable ("Lawyer | International Business Professional")
- [x] Companies listed exist in source (Diez Canseco Abogados, INDECOPI, Ripley)
- [x] Education institutions match (Lambton College, UNMSM)
- [x] No hallucinated data detected

## Clean Deploy
- [x] No watermarks
- [x] No placeholder text
- [x] No template links

## Technical
- [x] Page loads (HTTP 200)
- [x] CSS loads (HTTP 200 - `_astro/index.z47Fn8Iq.css`)
- [x] Favicon loads (HTTP 200 - `favicon.svg`)
- [x] LinkedIn link present and correct (`linkedin.com/in/carlosberaun`)
- [x] No critical console errors

## Language
- [ ] **FAIL**: Content is in English but nav items are in Spanish ("Sobre Mi", "Proyectos", "Experiencia", "Educacion")
- [ ] **FAIL**: html lang="es" but all content is in English

## Issues Found
1. **FAIL - Language inconsistency**: Nav/section headers are in Spanish ("Sobre Mi", "Proyectos", "Experiencia", "Educacion") but ALL content is in English. The html lang attribute is "es" but should be "en".
2. **NOTE - No profile photo**: Client uploaded a photo in the form but it was not included on the site.

## Evidence
- qa-desktop.png
