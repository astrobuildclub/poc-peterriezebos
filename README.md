# peterriezebos.netlify.app

> POC-website voor kunstenaar Peter Riezebos: hero, about, projecten en contact. Geen eigen domein; alleen de Netlify-URL. Kan later verder.

| | |
|---|---|
| **Klant** | Peter Riezebos (contactpersoon TODO) |
| **Bedrijf** | All This |
| **Status** | POC · niet live, kan later verder (okt 2026) |
| **SLA** | Nee |
| **Live** | Geen eigen domein. POC: [peterriezebos.netlify.app](https://peterriezebos.netlify.app) |
| **Netlify** | team All This (`allthis-digital`), site `peterriezebos` |
| **CMS** | geen |
| **Repo** | [github.com/astrobuildclub/poc-peterriezebos](https://github.com/astrobuildclub/poc-peterriezebos) |
| **Notion** | TODO |

## Stack

- Vite 5 · Node 22 (`.nvmrc`) · static (`dist`)
- Styling: SCSS, Utopia (`utopia-core-scss`), custom properties · Fonts: Neue Haas Grotesk (Adobe Fonts / Typekit `ghj8hze`), fallback Inter
- Animatie: GSAP 3.12 (ScrollTrigger, SplitText) · Lenis
- Consent: geen · Hosting: Netlify

Geen Astro.

## Lokaal starten

```bash
nvm use
npm install
npm run dev            # http://localhost:3000
```

Overige scripts: `npm run build`, `npm run preview`.

Controle 11 oktober 2026, Node 22: `npm install` en `npm run build` slagen. Vite waarschuwt dat de legacy Sass JS API verdwijnt (Dart Sass 2); de build rondt wel af.

### Environment-variabelen

Geen. Er is geen `.env.example`.

## Structuur

```
index.html          Homepage
menu.html           Los menu-prototype (niet in de Vite-entry)
src/
  js/               main.js + modules (lenis, scroll-config, hero, about, projects, menu)
  styles/           Reset, variabelen, componenten (SCSS)
  media/            Beeld, video, svg
```

## Content en CMS

Geen CMS. Tekst en media staan in `index.html` en `src/media/`. About-momenten bevatten nog placeholdertekst (lorem ipsum).

## Branches

Netlify (site `peterriezebos`, team `allthis-digital`) deployt **`main`**: build `npm run build`, publish `dist`. In de Netlify-UI staat de repo nog als `allthis-mieras/peterriezebos`; die URL verwijst door naar `astrobuildclub/poc-peterriezebos`. `allowed_branches` is alleen `main`. Deze PR voegt dezelfde build-instellingen toe in `netlify.toml`.

| Branch | Wat erop staat |
|---|---|
| `main` | Productie. Bevat de merges van `mieras` (t/m de hero-video, juli 2025) en van `scroll-fix-mobile` (PR #11, 5 okt 2026). |
| `mieras` | Werkbranch tot de videobestandsnaam-fix (`pr-teaser-opener-clean.mp4`, 9 juli 2025). Die commits zitten in `main`. Geen commits die `main` niet heeft. |
| `scroll-fix-mobile` | Lenis + ScrollTrigger voor mobiel (nov 2025): wachten op `window.load`, `scroll-config.js`, hash-scroll. Gemerged naar `main` via PR #11. Geen commits die `main` niet heeft. |

## Privacy, toegankelijkheid en SEO

- Consent: geen. Adobe Fonts laadt vanaf `use.typekit.net`. `menu.html` laadt GSAP van cdnjs en SplitText van een CodePen-asset.
- WCAG: geen formele 2.2 AA-audit. GSAP/Lenis negeren `prefers-reduced-motion` (de marquee in CSS niet).
- SEO volgens `~/Code/_standards/SEO.md`: niet ingericht (POC). `netlify.toml` zet `X-Robots-Tag: noindex, nofollow` zodra dit op `main` staat en Netlify opnieuw bouwt.

## Deploy

- `main` → [peterriezebos.netlify.app](https://peterriezebos.netlify.app)
- Werkwijze: branch → PR → merge. Niet direct naar `main`.
- Nieuwe features alleen na overleg.

## Bekende issues en afspraken

- POC, oktober 2026. Niet live op een eigen domein. Kan later verder. Geen nieuwe features zonder overleg.
- Netlify-koppeling toont nog `allthis-mieras/peterriezebos`. GitHub stuurt die URL door naar `astrobuildclub/poc-peterriezebos`. De branch die deployt is `main`.

---

Eigenaar: All This · Wat er gedaan is: zie [`CHANGELOG.md`](CHANGELOG.md) · Werkafspraken voor ontwikkelaars en AI-agents: [`AGENTS.md`](AGENTS.md)
