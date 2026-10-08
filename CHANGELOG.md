# Changelog

Alle noemenswaardige wijzigingen aan dit project. Nieuwste bovenaan.
Format gebaseerd op [Keep a Changelog](https://keepachangelog.com/nl/1.1.0/).

Categorieën: **Toegevoegd**, **Gewijzigd**, **Opgelost**, **Verwijderd**, **Beveiliging**, **Onderhoud**.

## [Unreleased]

## [2026-10-08]

### Onderhoud
- POC. Niet live op een eigen domein; kan later verder.
- Documentatie: README, CHANGELOG, AGENTS, CLAUDE.
- Node 22 via `.nvmrc` en `NODE_VERSION` in `netlify.toml`. Build `npm run build`, publish `dist`. Header `X-Robots-Tag: noindex, nofollow`.

## [2026-10]

### Gewijzigd
- `scroll-fix-mobile` gemerged naar `main` (PR #11). Dat is de stand die Netlify deployt.

## [2025-11]

### Opgelost
- ScrollTrigger wacht op `window.load`, zodat video en beeld een hoogte hebben vóór de triggers.
- Lenis gekoppeld aan ScrollTrigger (`scroll`-update, refresh na `scrollEnd`). Gedeelde scroll-config voor mobiel en desktop (`scroll-config.js`). Hash-links (`#about`) via Lenis.

## [2025-07]

### Gewijzigd
- Hero-video: `pr-teaser-dummy.mp4` vervangen door `pr-teaser-opener-clean.mp4`. Bestandsnaam met typefout (`.mp4a`) gecorrigeerd.
- Menu-styling opgenomen in `main.scss`.

## [2025-06]

### Toegevoegd
- Eerste opzet: Vite, GSAP, Lenis, Utopia, SCSS.
- Contactsectie (aanvragen, pers, samenwerkingen).
- Scrollindicator in de hero, projectbeelden en fade op titels.

### Gewijzigd
- About op mobiel: relatieve positie, automatische hoogte, centrering.
- Hoogtes van `100vh` naar `100dvh`. Contact-grid op kleine schermen.
- ScrollTrigger-normalisatie en refresh bij resize en Lenis-scroll in de projectsectie.

### Verwijderd
- Ongebruikte video-scroll in de hero.
