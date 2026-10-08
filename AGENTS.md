# AGENTS.md: Peter Riezebos (POC)

Geen nieuwe features zonder overleg. Dit is een slapende POC (oktober 2026): niet live op een eigen domein, kan later verder.

Instructies voor AI-agents en ontwikkelaars. Lees eerst `README.md` en `CHANGELOG.md`.

## Project
- Klant: Peter Riezebos · Bedrijf: All This · SLA: Nee
- Status: POC · niet live, kan later verder (okt 2026)
- Stack: Vite 5, SCSS, Utopia, GSAP 3.12, Lenis, Node 22 (zie `.nvmrc`)
- CMS: geen
- Geen Astro

## Werkwijze
- Niets verwijderen. Niet pushen naar `main`. Geen force-push.
- Werk nooit direct op `main`. Branch → PR → merge.
- Branchnamen: `feat/…`, `fix/…`, `chore/…`, `docs/…`.
- Commit nooit `.env`-bestanden of tokens.
- Bij een wijziging: een regel onder `## [Unreleased]` in `CHANGELOG.md`. Verandert setup, stack of deploy? Werk `README.md` bij.
- Site blijft op Netlify (`peterriezebos`, team `allthis-digital`) met `X-Robots-Tag: noindex, nofollow`.

## Conventies
- Moderne CSS: custom properties, logical properties. Kleuren in deze POC zijn nog geen OKLCH.
- Toegankelijkheid: WCAG 2.2 AA. `prefers-reduced-motion` geldt ook voor GSAP en Lenis; dat ontbreekt nu in de JS.
- AVG: geen tracking of extra third-party scripts zonder consent. Adobe Fonts (Typekit) en de CDN-scripts op `menu.html` laden nu altijd.
- Animaties (GSAP): leg in een comment kort de logica uit (timeline, trigger, cleanup).
- Afbeeldingen: geen vastgelegd profiel volgens `~/Code/_standards/IMAGES.md` (TODO).

## GSAP en Lenis

De volgorde in `src/js/main.js` is verplicht, en pas na `window.load`:

1. `initScrollConfig()` — `ScrollTrigger.config`, `normalizeScroll(true)`
2. `initLenis()` — koppelt scroll aan `ScrollTrigger.update`
3. `initHero()`, `initAbout()`, `initProjects()`
4. `ScrollTrigger.refresh()`

Valkuilen die in de code zitten:

- Zonder `window.load` rekent ScrollTrigger triggers terwijl video en beelden nog groeien. Niet terug naar `DOMContentLoaded`.
- Lenis moet `ScrollTrigger.update` op `scroll` krijgen. Zonder die koppeling vuren pins niet, vooral op mobiel.
- `normalizeScroll(true)` hoort één keer, in `scroll-config.js`. Een tweede aanroep (die stond in `projects.js`) maakt het scrollgedrag inconsistent.
- `ScrollTrigger.refresh()` draait nu dubbel na elke scroll: in `lenis.js` op `scrollEnd` én nog eens in `projects.js` via `window.lenis`. Dat is bewust laten staan als “backwards compatibility”; niet een derde listener toevoegen.
- `ignoreMobileResize: true` plus een debounce van 250ms op `resize` en 500ms op `orientationchange`. Geen extra resize-handlers die zelf `refresh()` doen (de hero-`fitText` mag wel de font-size zetten).
- De hero pint `+=200%` (`pin`, `anticipatePin: 1`). In `onUpdate` start elke scroll-tick een nieuwe `gsap.to` op de video-opacity. Dat stapelt tweens. Pin + Lenis + `normalizeScroll` is de combinatie die op mobiel sprong.
- Projecten pinnen `.project__sticky` en schuiven de slides horizontaal. De eindafstand komt uit de breedte van de slides (`invalidateOnRefresh: true`). Na een layoutwijziging is één refresh genoeg.
- `ScrollTrigger.matchMedia` in `scroll-config.js` geeft `{ add, remove }` terug en de callbacks zijn leeg. Vanaf GSAP 3.12 is de bedoelde API `gsap.matchMedia()` met `mm.add()`. Deze queries doen nu niets; niet aannemen dat mobiel en desktop hier al uit elkaar getrokken zijn.
- Hash-scroll (`#about`) gebruikt `setTimeout(100)` en `lenis.scrollTo` met `duration: 0`. Lenis staat op `window.lenis`.
- De Lenis-`requestAnimationFrame`-loop stopt nergens.
- `SplitText` in `hero.js` komt uit `gsap/SplitText` (Club-plugin) en gebruikt `SplitText.create`. `menu.js` is een los script op `menu.html`: GSAP via cdnjs, SplitText via een CodePen-URL, geen imports, en het zit niet in `main.js`. Niet in de Vite-bundle trekken zonder die twee paden gelijk te trekken.
