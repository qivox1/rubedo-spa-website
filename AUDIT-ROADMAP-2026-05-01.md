# Rubedo Spa — Audit & Optimierungs-Roadmap

**Erstellt:** 1. Mai 2026
**Live-Domain (aktuell):** https://rubedo-spa-website.pages.dev
**Ziel-Domain:** https://rubedo-spa.de
**Repo:** https://github.com/qivox1/rubedo-spa-website
**Last commit checked:** `76744ef` (Triptychon-Bild-Fix)

Dieser Bericht ist eine konsolidierte Bestandsaufnahme nach dem 1. Mai 2026 und gleichzeitig eine priorisierte Arbeitsliste zum sukzessiven Abarbeiten. Die Sprints sind so geschnitten, dass jeder einzeln abgeschlossen werden kann, ohne von späteren Sprints abzuhängen.

---

## Inhaltsverzeichnis

1. [Executive Summary](#1-executive-summary)
2. [Status quo — was bereits sitzt](#2-status-quo)
3. [Sprint 1 — kritisch, diese Woche](#3-sprint-1)
4. [Sprint 2 — wichtig, nächste 2 Wochen](#4-sprint-2)
5. [Sprint 3 — Premium-Polish, 4–8 Wochen](#5-sprint-3)
6. [Externe Tool-Registrierungen (Checkliste)](#6-externe-tools)
7. [Page-by-Page Findings](#7-page-findings)
8. [Code-Snippets für die kritischen Fixes](#8-code-snippets)
9. [HWG-Compliance-Scan](#9-hwg)
10. [Referenzen, Standards, Doku-Quellen](#10-referenzen)

---

## 1. Executive Summary <a id="1-executive-summary"></a>

Die Seite ist **inhaltlich auf Premium-Niveau** angekommen: Architektur in 5 Top-Level-Items konsolidiert, drei Säulen mit kompletten Sub-Pages, Magazin mit zwei vollwertigen Artikeln, EU-AI-Act-konforme C2PA-Kennzeichnung, Datenschutz mit DNA-Skin-Klausel, Impressum mit USt-IdNr, Building-Hero von fal.ai retuschiert, Lina als wiederkehrende Klientinnen-Persona etabliert.

**Was uns daran hindert, in Suchmaschinen ganz vorne zu sein:**

1. **Domain-Mismatch:** Wir ranken aktuell unter `rubedo-spa-website.pages.dev` statt `rubedo-spa.de`. Das ist Ranking-Bremse Nummer eins.
2. **Search Console nicht verifiziert:** Wir wissen nicht, was Google sieht oder beanstandet.
3. **Sitemap-Verweis in robots.txt zeigt auf eine falsche URL** und auf eine nicht existierende `sitemap-index.xml`.
4. **H1 und Title der Startseite enthalten kein lokales Such-Keyword** — wir verschenken „Longevity-Studio Minden" in der wichtigsten On-Page-Position.
5. **Magazin hat erst zwei Artikel.** Für Topic-Authority brauchen wir 12–20 Artikel innerhalb von 6 Monaten.
6. **GA4 misst nur Pageviews,** keine Conversions. Wir haben keine Lead-Funnel-Sichtbarkeit.

Wenn Sprint 1 (siehe unten) durchgezogen ist, sind wir SEO-fundamental aufgestellt. Sprint 2 baut die Konversionsstrecke aus. Sprint 3 ist Premium-Polish.

---

## 2. Status quo — was bereits sitzt <a id="2-status-quo"></a>

### Architektur & Inhalt
- 24 indexierbare URLs in der Sitemap
- 5 Top-Level-Navigationspunkte (Philosophie · Anwendungen · Monica · Magazin · Kontakt) mit Mega-Menu unter „Anwendungen"
- 3 Säulen-Hubs + 5 Behandlungs-Sub-Pages (Ganzkörper, Körperformung, Wrap, Bandage, Rubedo Suite, Atem-Ritual)
- Longevity-Studio-Minden-Page mit Building-Fotografie und retuschiertem Hero
- Magazin mit Themenwelten („Longevity / Kryotherapie / DNA Skin / Inner Source") und 2 Artikeln
- Über-Monica mit AboutPage- und Person-Schema, vollständigen Credentials
- Impressum mit USt-IdNr `DE 98426105747`, AI-Klausel, Verantwortlich-Tag
- Datenschutz mit DSGVO Art. 9 / GenDG-Klausel für DNA-Skin, plus AI-Bild-Hinweis
- /ki-bilder/-Erklärseite mit C2PA, EU AI Act, Persona-Hinweis, Werkzeug-Liste

### Technisch
- Astro 5 Static, Cloudflare Pages Hosting, automatischer Build via api-push.sh
- Tailwind v3 (NICHT v4 — Linux-Bug bestätigt, Lock-File ok)
- WebP-Bilder mit Preload für Hero, Self-hosted Fonts (Outfit + Cormorant Garamond)
- View Transitions, Reveal-on-Scroll, Klaro Cookie-Consent mit Consent-Mode v2
- HealthAndBeautyBusiness-Schema global, Service-Schema auf Behandlungs-Pages, FAQPage-Schema auf Magazin-Artikeln
- C2PA „cr"-Pin via globales JS auf alle `<img>`-Tags ohne `data-ai="false"`
- Robots.txt mit explizitem `Allow:` für GPTBot, ClaudeBot, PerplexityBot, Google-Extended, CCBot

### Tracking
- GA4 Property `G-41DDXKN7XL` aktiv im Code, IP-Anonymisierung an
- GTM Container `GT-P3N6R5J2` lädt nach Consent
- Klaro Consent-Mode v2 default-deny
- Cookie-Banner mit Auswahl „Alle akzeptieren / Nur notwendige / Auswahl speichern"

---

## 3. Sprint 1 — kritisch, diese Woche <a id="3-sprint-1"></a>

> Geschätzter Aufwand: 2–4 Stunden gebündelt.
> Ziel: SEO-Grundfundament steht, Tools messen, Suchmaschinen sind onboardet.

### 1.1 robots.txt korrigieren 🔴

Datei: `website/public/robots.txt`

**Problem:** Sitemap-Verweis zeigt auf `https://rubedo-spa.de/sitemap-index.xml` — Domain noch nicht aktiv, Datei existiert nicht.

**Aktion:** auf aktuelle Live-URL umstellen. Sobald Custom-Domain umgezogen ist, wieder auf `https://rubedo-spa.de/sitemap-0.xml` setzen.

```diff
- Sitemap: https://rubedo-spa.de/sitemap-index.xml
+ Sitemap: https://rubedo-spa-website.pages.dev/sitemap-0.xml
```

### 1.2 H1 + Title der Startseite SEO-optimieren 🔴

Datei: `website/src/pages/index.astro`

**Problem:** H1 ist „Smart Beauty for Conscious Humans." — markenstark, aber **null Suchvolumen** in DE. Title-Tag enthält kein Lokal-Keyword.

**Aktion 1 (H1):**
```diff
- <h1>Smart Beauty for Conscious Humans.</h1>
+ <h1>Longevity-Studio Minden — Smart Beauty for Conscious Humans.</h1>
```

Alternativ als zwei Zeilen mit visuellem Trenner (eleganter):
```html
<h1>
  <span class="rb-h1__primary">Longevity-Studio Minden.</span>
  <span class="rb-h1__claim">Smart Beauty for Conscious Humans.</span>
</h1>
```

**Aktion 2 (Title-Tag):**
```diff
- const title = `${site.name} — ${site.claim}`;
+ const title = `${site.name} Minden — Longevity-Studio · ${site.claim}`;
```

Längen prüfen: max. 60 Zeichen für Google-Snippet. Kürzere Variante:
`"Rubedo Spa Minden — Longevity-Studio · Smart Beauty"` (50 Zeichen).

### 1.3 Google Search Console verifizieren 🔴

**Schritte:**
1. https://search.google.com/search-console öffnen
2. Property anlegen: Typ „Domain" (besser als „URL-Präfix") für `rubedo-spa.de`
   *Falls Domain noch nicht aktiv:* übergangsweise URL-Präfix `https://rubedo-spa-website.pages.dev/`
3. DNS-TXT-Verifikation oder Meta-Tag-Verifikation
4. Verifikations-Tag in `BaseLayout.astro` einbauen:
```html
<meta name="google-site-verification" content="DEIN_TOKEN_HIER" />
```
5. Sitemap einreichen: `sitemap-0.xml`
6. URL-Inspection für Startseite und drei Säulen-Hubs durchführen, „Indexierung anfordern"

### 1.4 Bing Webmaster Tools verifizieren 🔴

ChatGPT verwendet teilweise Bing-Index.

**Schritte:**
1. https://www.bing.com/webmasters
2. Property hinzufügen
3. Verifikation per Meta-Tag oder DNS
4. Sitemap einreichen

### 1.5 `/llms.txt` anlegen 🔴

Standard für AI-Engines (analog robots.txt). Datei: `website/public/llms.txt`

```
# Rubedo Spa — llms.txt
# Standard: https://llmstxt.org

> Rubedo Spa ist ein Longevity-Studio in Minden, Deutschland.
> Geführt von Monica Galletti — CIDESCO Beauty Therapist,
> DNA Skin Expert (Beauty ID Switzerland), NLP Master.
> Drei Säulen: DNA Skin Intelligence, Kryo Vital, Inner Source.

## Säulen
- [DNA Skin Intelligence](https://rubedo-spa.de/dna-skin-intelligence/) — Personalisierte Hautpflege auf Basis von 20 Beauty-Genen, 12-Wochen-Programm.
- [Kryo Vital](https://rubedo-spa.de/kryo-vital/) — Drei Minuten kontrollierter Kältereiz für Vitalität. Ganzkörper-Kryotherapie, Druckwellen, Bandagen.
- [Inner Source Rituals](https://rubedo-spa.de/inner-source/) — Massage-Rituale (Abhyanga, Hot Stone, Hot Bambu, Balinesisch) plus neurosomatische Atemarbeit.

## Über
- [Über Monica Galletti](https://rubedo-spa.de/ueber-monica/) — Vita, Zertifizierungen, Methodik
- [Longevity-Studio Minden](https://rubedo-spa.de/longevity-studio-minden/) — Studio-Profil, Werte, Standort
- [Philosophie](https://rubedo-spa.de/philosophie/) — Smart Beauty for Conscious Humans

## Magazin
- [Wellness in Minden — moderne Technologien](https://rubedo-spa.de/magazin/wellness-minden-technologie/)
- [Ganzkörper-Kryotherapie Minden](https://rubedo-spa.de/magazin/kryotherapie-minden/)

## Hinweise
- Bildinhalte sind überwiegend KI-generiert (siehe /ki-bilder/) und entsprechend mit C2PA Content Credentials gekennzeichnet.
- Das Studio macht keine Heilversprechen; alle Anwendungen sind Wellness-Pflege gemäß HWG.
```

### 1.6 HWG-Korrektur „Reiz für Regeneration" 🔴

Datei: `website/src/pages/index.astro` (Drei-Säulen-Teaser, Säule Kryo Vital)

**Problem:** Aktuell steht im Pillar-Claim:
> „Kälte als Reiz für Regeneration und Vitalität."

„Reiz für Regeneration" ist eine Wirkungsbehauptung — HWG-grenzwertig.

**Lösung:**
```diff
- "Kälte als Reiz für Regeneration und Vitalität."
+ "Kälte als bewusster Reiz — drei Minuten, die viele Gäste als Frischekick beschreiben."
```

Subjektive Wahrnehmungsformel ist HWG-sicher.

Gleiche Stelle prüfen auf `/philosophie/` Seite.

### 1.7 GA4 Conversion-Events 🔴

In `src/components/Analytics.astro` oder via GTM-Container:

**Event 1:** Klick auf „Termin buchen" / „Erstgespräch sichern"
- Event-Name: `lead_termin_buchen`
- Trigger: Klick auf `<a href*="/termin-buchen/"]`

**Event 2:** Magazin-Artikel zu 50 % gescrollt
- Event-Name: `magazin_artikel_engaged`
- Trigger: Scroll-Tiefe-Trigger im GTM

**Event 3:** Klick auf Behandlungs-Detail
- Event-Name: `treatment_detail_view`
- Trigger: Klick auf `.rb-tcard__cta`

In GA4 Admin → Events → die drei Events als **Konversion** markieren.

### 1.8 Sprint-1-Checklist

- [ ] robots.txt Sitemap-URL korrigiert
- [ ] Startseite H1 mit Lokal-Keyword
- [ ] Startseite Title-Tag mit Lokal-Keyword
- [ ] Google Search Console verifiziert + Sitemap eingereicht
- [ ] Bing Webmaster Tools verifiziert + Sitemap eingereicht
- [ ] `public/llms.txt` deployed
- [ ] HWG-Korrektur „Reiz für Regeneration" (Index + Philosophie)
- [ ] GA4 Conversion-Event `lead_termin_buchen` aktiv

---

## 4. Sprint 2 — wichtig, nächste 2 Wochen <a id="4-sprint-2"></a>

> Geschätzter Aufwand: 1–2 Tage.
> Ziel: Custom Domain ist scharf, DNA-Funnel hat Zwischenstufe, Magazin wächst.

### 2.1 Custom Domain `rubedo-spa.de` aktivieren 🟡

**Schritte:**
1. domainfactory (df.eu) → DNS-Verwaltung der Domain `rubedo-spa.de`
2. CNAME-Record setzen:
   - Name: `@` (oder `www`)
   - Ziel: `rubedo-spa-website.pages.dev`
3. Cloudflare Pages → Custom Domain anhängen → Verifikation abwarten
4. SSL-Zertifikat (Cloudflare automatisch) abwarten
5. In `astro.config.mjs`:
```diff
export default defineConfig({
- site: 'https://rubedo-spa-website.pages.dev',
+ site: 'https://rubedo-spa.de',
  // ...
});
```
6. In `src/lib/site.ts`:
```diff
- url: 'https://rubedo-spa-website.pages.dev',
+ url: 'https://rubedo-spa.de',
```
7. robots.txt Sitemap-URL final auf `https://rubedo-spa.de/sitemap-0.xml` umstellen
8. Search Console Property auf `rubedo-spa.de` umziehen, alte pages.dev als „Change of Address"

**Achtung:** Schema-`url`-Felder werden automatisch durch den Build neu generiert (sie nutzen `site.url`). Manueller Cross-Check der wichtigsten Pages nach dem Switch ist Pflicht.

### 2.2 DNA-Skin Funnel-Zwischenstufe 🟡

Aktuell: Startpreis 2.000 € sehr direkt. Conversion-Killer.

**Konzept:** dreistufiger Funnel
1. Erstgespräch (15 Min, kostenfrei) — Lead-Magnet
2. **NEU: 90-Min-Erstanalyse vor Ort — 149 €** (Soft-Yes)
3. 12-Wochen-Programm — 2.000 €

**Aktion:**
- Auf `/dna-skin-intelligence/` einen neuen Block oberhalb des „Investition"-Blocks einfügen
- Pricing-Tabelle erweitern um die 149-€-Stufe
- CTA-Button-Hierarchie anpassen: primär „149 € Erstanalyse" (statt direkt 2.000 €)

### 2.3 Service-Schema auf Säulen-Hubs ergänzen 🟡

Aktuell: nur `HealthAndBeautyBusiness` auf den Hubs. Ergänze `ItemList`, das die Sub-Services aufzählt.

**Beispiel für `/kryo-vital/`:**
```js
const itemListSchema = {
  '@context': 'https://schema.org',
  '@type': 'ItemList',
  name: 'Kryo Vital — Anwendungen',
  itemListElement: [
    { '@type': 'ListItem', position: 1, url: `${site.url}/kryo-vital/ganzkoerper/`, name: 'Ganzkörper-Kryotherapie' },
    { '@type': 'ListItem', position: 2, url: `${site.url}/kryo-vital/koerperformung/`, name: 'Körperformung & Druckwellen' },
    { '@type': 'ListItem', position: 3, url: `${site.url}/kryo-vital/koerperformung/wrap/`, name: 'Body Slimming Wrap' },
    { '@type': 'ListItem', position: 4, url: `${site.url}/kryo-vital/koerperformung/bandage/`, name: 'Body Slimming Bandage' },
  ],
};
```

Analog für `/inner-source/` (Rubedo Suite, Atem-Ritual).

### 2.4 Kontakt-Seite Google-Maps-Embed 🟡

Aktuell nur stilistischer Pin. UX und Local-SEO leiden.

**Optionen:**
- **Beste:** statisches Map-Image (Google Maps Static API mit Klaro-Consent), kostenlos bis 28.500 Aufrufe/Monat
- **Premium:** OpenStreetMap/Leaflet Embed (kein Google-Tracking, einfach DSGVO-konform)
- **Schnell:** Google-Maps-iframe-Embed mit Klaro-Consent-Lock

### 2.5 Magazin: 6 neue Artikel publizieren 🟡

Priorität nach Suchvolumen + Conversion-Pfad:

| # | Titel-Vorschlag | Kategorie | Keyword-Fokus |
|---|---|---|---|
| 1 | „Was kostet Kryotherapie? Ein transparenter Überblick" | Kryotherapie | „kryotherapie kosten" |
| 2 | „DNA-Hautpflege: Was 20 Beauty-Gene über deine Haut verraten" | DNA Skin | „dna hautpflege", „beauty gene" |
| 3 | „Bewusste Atemübungen für stressige Wochen — 3 Mikro-Praktiken" | Inner Source | „atemübungen stress", „atemtechnik entspannung" |
| 4 | „Wellness Wochenende Minden — wie ein bewusster Reset aussieht" | Longevity | „wellness wochenende minden" |
| 5 | „Druckwellen-Anwendung vs. manuelle Lymphdrainage — der Unterschied" | Kryotherapie | „druckwellen massage", „pressotherapie" |
| 6 | „Hot Stone Wirkung: was die Wärme im Nervensystem auslöst" | Inner Source | „hot stone wirkung", „hot stone massage" |

Pro Artikel ~1.200–1.800 Wörter, mit 2–3 fal.ai-Bildern (Lina-Konsistenz), FAQ-Schema, internen Links zu den Säulen-Hubs.

### 2.6 FAQ-Antworten erweitern (AI-Search-Optimierung) 🟡

Aktuell: viele FAQ-Antworten sind 2–3 Sätze. AI-Engines (ChatGPT, Perplexity, Google AI Overviews) bevorzugen 60–120-Wort-Antworten.

**Pattern:**
1. Direkte Antwort (1 Satz)
2. Kontext / Erklärung (2–3 Sätze)
3. Brand-Anker („Im Rubedo Spa Minden ...")

Alle FAQ-Items in den Säulen-Hubs und Behandlungspages durchgehen. ~2 Stunden.

### 2.7 Sprint-2-Checklist

- [ ] Custom Domain rubedo-spa.de aktiv
- [ ] DNA-Skin Funnel-Zwischenstufe „149 € Erstanalyse"
- [ ] Service-Schema (`ItemList`) auf Säulen-Hubs
- [ ] Google-Maps-Embed auf Kontakt
- [ ] 6 neue Magazin-Artikel publiziert
- [ ] FAQ-Antworten auf 60–120 Wörter erweitert

---

## 5. Sprint 3 — Premium-Polish, 4–8 Wochen <a id="5-sprint-3"></a>

### 3.1 Booking-Calendar-Embed 🟢

Google Workspace `rubedospa@gmail.com` aktivieren → Appointment Schedule erstellen → Embed-URL in `site.ts` `booking.embedUrl` eintragen → `/termin-buchen/` Seite zeigt das Embed mit Klaro-Consent.

### 3.2 Cloudflare Turnstile für Termin-Form 🟢

Site-Key in Cloudflare Dashboard erzeugen, in Form integrieren. DSGVO-konformer Spam-Schutz ohne Cookie.

### 3.3 Performance-Quickwins 🟢

- **`srcset` + `sizes`** auf Hero-Images: 800w / 1200w / 1600w-Varianten generieren, damit Mobile nicht das volle 1600w-Bild lädt. Erwarteter LCP-Gewinn: ~30 % auf Mobile.
- **Critical-CSS-Inlining** für Hero-Sektion. Tool: `@beasties/beasties` (Astro-Plugin). LCP-Gewinn: ~150 ms.
- **`loading="lazy"`** auf alle Below-the-Fold-Bilder verifizieren.

### 3.4 Mobile-Sticky-CTA „Termin buchen" 🟢

Auf Mobile am unteren Bildschirmrand ein dezentes Sticky-Element, das einen direkten Tap zum Termin-Booking erlaubt. Standard-Conversion-Hebel im Premium-Spa-Bereich.

### 3.5 EN-Version 🟢

Hreflang-Strategie:
```html
<link rel="alternate" hreflang="de" href="https://rubedo-spa.de/" />
<link rel="alternate" hreflang="en" href="https://rubedo-spa.de/en/" />
<link rel="alternate" hreflang="x-default" href="https://rubedo-spa.de/" />
```

Übersetzungs-Strategie: Astro i18n Routing, professionelle Translation für Schlüsselseiten (Index, Säulen, Monica), Magazin nur DE.

### 3.6 Kunden-Reviews einsammeln + Schema 🟢

Sobald erste Kunden-Reviews vorliegen: `Review`- und `AggregateRating`-Schema einbauen. Erscheint dann in Google-Rich-Snippets.

### 3.7 Self-Hosted-Fonts mit `font-display: swap` 🟢

Bereits self-hosted, aber `font-display`-Strategie prüfen. `swap` ist Standard, aber bei den Display-Fonts könnte `optional` (für non-LCP) Performance bringen.

### 3.8 Sprint-3-Checklist

- [ ] Booking-Calendar-Embed
- [ ] Cloudflare Turnstile auf Forms
- [ ] `srcset` + `sizes` auf Hero-Images
- [ ] Critical-CSS-Inlining
- [ ] Mobile-Sticky-CTA
- [ ] EN-Version Schlüsselseiten
- [ ] Review-Sammlung + Review-Schema
- [ ] Font-display-Optimierung

---

## 6. Externe Tool-Registrierungen <a id="6-externe-tools"></a>

| Tool | URL | Status | Aktion |
|---|---|---|---|
| Google Search Console | https://search.google.com/search-console | ❌ | Property anlegen, verifizieren, Sitemap einreichen |
| Bing Webmaster Tools | https://www.bing.com/webmasters | ❌ | Property anlegen, verifizieren, Sitemap einreichen |
| Google Analytics 4 | https://analytics.google.com | ✅ | Property `G-41DDXKN7XL` aktiv. Conversion-Events ergänzen |
| Google Tag Manager | https://tagmanager.google.com | ✅ | Container `GT-P3N6R5J2` aktiv. Tags konfigurieren |
| Google Business Profile | https://business.google.com | ❌ | Studio anlegen mit Marienstraße 58, Fotos, Öffnungszeiten — wesentlich für Local-SEO |
| Google PageSpeed Insights | https://pagespeed.web.dev | ❌ | Periodisch testen, nach Sprint 3 aufs Ziel: 90+ Desktop, 80+ Mobile |
| Lighthouse CI | https://github.com/GoogleChrome/lighthouse-ci | ❌ | Optional: bei jedem Push automatisch Performance-Report |
| Schema.org Validator | https://validator.schema.org/ | — | Vor jedem Schema-Refactor durchlaufen lassen |
| Rich Results Test | https://search.google.com/test/rich-results | — | Pro Schema-Page checken |
| Fonts.google → Self-Host | https://gwfh.mranftl.com/fonts | ✅ | Bereits self-hosted |
| Cloudflare Turnstile | https://dash.cloudflare.com → Turnstile | ❌ | Site-Key generieren |
| Klaro Cookie | https://github.com/kiprotect/klaro | ✅ | Läuft, könnte für Server-Side-Tagging erweitert werden |

---

## 7. Page-by-Page Findings <a id="7-page-findings"></a>

### `/` — Startseite
- 🔴 H1 + Title ohne Lokal-Keyword (siehe 1.2)
- 🔴 Pillar-Claim Kryo HWG-grenzwertig (siehe 1.6)
- 🟡 Pull-Quote-Bild kontrastiert schwach mit Text → Overlay verstärken
- 🟡 Lead-Magnet-Block ohne „Kostenfrei"-Badge → Conversion-Hebel
- 🟢 Triptychon-Bild gefixt (commit `76744ef`)
- 🟢 Monica-Vignette mit Caption-Link sauber

### `/philosophie/`
- 🔴 Pillar-Claim Kryo HWG-Korrektur identisch zur Startseite
- 🟡 H1 „Weniger Methoden." stark, aber + Lokal-Bezug fehlt
- 🟢 7 H2s, gute Tiefe

### `/longevity-studio-minden/`
- 🟢 Hero mit retuschiertem Building-Bild
- 🟢 Stuck-Detail im Img-Text-Block
- 🟢 Längsseiten-Banner vor CTA
- 🟢 SEO-Slug optimal

### `/dna-skin-intelligence/`
- 🟢 16 H2s — höchste Tiefe der Seite, Top-Ranking-Kandidat für „dna hautpflege minden"
- 🟡 Funnel-Zwischenstufe 149 € fehlt (siehe 2.2)
- 🟡 Service-Schema fehlt (`ItemList` mit referenzierten Sub-Pages)

### `/kryo-vital/` + Sub-Pages
- 🔴 HWG-Pillar-Claim
- 🟡 Service-Schema-`ItemList` ergänzen
- 🟢 Sub-Pages haben alle eigenes Service-Schema + FAQ-Schema
- 🟢 Premium-Bilder konsistent

### `/inner-source/` + Sub-Pages
- 🟡 Service-Schema-`ItemList` ergänzen
- 🟢 Atem-Ritual mit eigenem Lina-Hero (commit `49b63be`)
- 🟢 Mehr-Lesen-Verlinkungen funktionieren

### `/ueber-monica/`
- 🟢 Person-Schema komplett
- 🟢 H1 Hero-Größe (commit `88269ff`)
- 🟡 `sameAs` in Person-Schema fehlt — sobald Social-Profile-URLs in `site.ts`, hier einbinden

### `/magazin/`
- 🟢 Filter-Pills mit neuen Kategorien (Longevity, Kryotherapie)
- 🟢 Themenwelten-Karten benannt nach Säulen
- 🟡 Featured-Slot-Logik prüfen (welcher Artikel landet im Hero?)

### `/magazin/wellness-minden-technologie/`
- 🟢 Premium-Hero (Lina + Spa-Tools)
- 🟢 Inline-Still-Life im Vergleich-Block
- 🟢 FAQ-Schema, Article-Schema, Breadcrumb

### `/magazin/kryotherapie-minden/`
- 🟢 HWG-konform überarbeitet (Original-WP-Text war problematisch)
- 🟢 Lina-After-Bild im Wirkung-Abschnitt
- 🟡 Externe Quelle „Cleveland Clinic" referenziert — gut für E-E-A-T, könnte um zwei weitere wissenschaftliche Quellen ergänzt werden

### `/kontakt/`
- 🟡 Google-Maps-Embed fehlt (siehe 2.4)
- 🟢 Eingangs-Hero mit Building-Foto
- 🟢 Fassaden-Detail-Akzent
- 🟢 NAP-Daten korrekt und prominent

### `/termin-buchen/`
- 🔴 Kein funktionaler Buchungsfluss (Google-Calendar-Embed fehlt)
- 🟢 Erstgespräch-Hinweis prominent

### `/datenschutz/`
- 🟢 Vollständig DSGVO-konform
- 🟢 Art.-9-Klausel für DNA
- 🟢 AI-Bild-Klausel
- 🟢 TOC mit Sprungmarken

### `/impressum/`
- 🟢 § 5 TMG vollständig
- 🟢 USt-IdNr eingetragen
- 🟢 AI-Klausel
- 🟢 Bildnachweise + Berufsregelungen

### `/ki-bilder/`
- 🟢 EU AI Act + C2PA-Erklärung
- 🟢 Persona-Hinweis (Lina fiktiv)
- 🟢 Werkzeug-Liste

### `/gutscheine/`
- 🟡 Inhalt prüfen — diese Seite habe ich nicht im Detail durchgesehen, könnte Aktualisierungs-Bedarf haben

---

## 8. Code-Snippets für die kritischen Fixes <a id="8-code-snippets"></a>

### 8.1 robots.txt Zeile

```diff
# in public/robots.txt:
- Sitemap: https://rubedo-spa.de/sitemap-index.xml
+ Sitemap: https://rubedo-spa-website.pages.dev/sitemap-0.xml
```

### 8.2 Startseite H1 + Title

```diff
# in src/pages/index.astro:
---
- const title = `${site.name} — ${site.claim}`;
+ const title = `${site.name} Minden — Longevity-Studio · ${site.claim}`;
  const description = `Rubedo Spa Minden — Longevity-Studio mit drei Säulen: DNA Skin Intelligence, Kryo Vital, Inner Source. Geführt von Monica Galletti.`;
---

  <h1 class="rb-h1-stacked">
-   Smart Beauty for Conscious Humans.
+   <span class="rb-h1__primary">Longevity-Studio Minden.</span>
+   <span class="rb-h1__claim">Smart Beauty for Conscious Humans.</span>
  </h1>
```

CSS dafür (in `index.astro` `<style>` oder template.css):
```css
.rb-h1-stacked {
  display: flex; flex-direction: column;
  font-family: var(--rb-font-display);
  line-height: 1.05;
}
.rb-h1__primary {
  font-size: clamp(40px, 6vw, 88px);
  font-weight: 400;
  letter-spacing: -0.01em;
  color: var(--rb-ink-900);
}
.rb-h1__claim {
  font-size: clamp(20px, 2.4vw, 32px);
  font-weight: 400;
  letter-spacing: 0.01em;
  color: var(--rb-gold-700);
  margin-top: 8px;
}
```

### 8.3 GA4 Conversion-Event in GTM

Trigger in GTM:
- Type: Click - All Elements
- Trigger fires on: Some Click Elements
- Filter: `Click URL` matches RegEx `\/termin-buchen\/`

Tag in GTM:
- Type: GA4 Event
- Event Name: `lead_termin_buchen`
- Configuration Tag: deine GA4-Config

In GA4 Admin → Conversions → markieren als Conversion.

### 8.4 Service-Schema ItemList für `/kryo-vital/`

```js
// in src/pages/kryo-vital/index.astro
const url = `${site.url}/kryo-vital/`;
const itemListSchema = {
  '@context': 'https://schema.org',
  '@type': 'ItemList',
  '@id': `${url}#anwendungen`,
  name: 'Kryo Vital — Anwendungen im Rubedo Spa Minden',
  numberOfItems: 4,
  itemListElement: [
    {
      '@type': 'ListItem',
      position: 1,
      url: `${site.url}/kryo-vital/ganzkoerper/`,
      name: 'Ganzkörper-Kryotherapie',
    },
    {
      '@type': 'ListItem',
      position: 2,
      url: `${site.url}/kryo-vital/koerperformung/`,
      name: 'Körperformung & Druckwellen-Anwendung',
    },
    {
      '@type': 'ListItem',
      position: 3,
      url: `${site.url}/kryo-vital/koerperformung/wrap/`,
      name: 'Body Slimming Wrap',
    },
    {
      '@type': 'ListItem',
      position: 4,
      url: `${site.url}/kryo-vital/koerperformung/bandage/`,
      name: 'Body Slimming Bandage',
    },
  ],
};
// In BaseLayout schemaExtras={[itemListSchema]} ergänzen
```

### 8.5 llms.txt Vollversion

(siehe Sprint 1.5 oben — direkt nach `public/llms.txt`)

---

## 9. HWG-Compliance-Scan <a id="9-hwg"></a>

Vollständige Suche durch alle deployten Pages auf gefährliche Begriffe:

| Begriff | Vorkommen | Status |
|---|---|---|
| „Heilung" | 0 | ✅ |
| „heilen" / „heilt" | 0 | ✅ |
| „Anti-Aging" | 0 | ✅ |
| „Schmerzlinderung" | 0 (Magazin-WP-Original noch problematisch) | ✅ |
| „Lymphdrainage" | 0 (bewusst durch „Druckwellen-Anwendung" ersetzt) | ✅ |
| „Reduktion von Cellulite" | 0 | ✅ |
| „Behandlung von" | 0 | ✅ |
| „Reiz für Regeneration" | 1 (Startseite + Philosophie) | 🔴 fix per 1.6 |
| „Entzündungshemmung" | 0 (im neuen Inhalt) | ✅ |

Weitere präventive Checks:
- ✅ Kein medizinischer Disclaimer fehlt — wir haben überall „Wir machen keine Heilversprechen" oder ähnliches
- ✅ Keine Erfolgs-Garantien
- ✅ Keine Vorher-Nachher-Bilder

**Empfehlung:** Vor jedem neuen Magazin-Artikel den HWG-Check als Pre-Publish-Schritt: Begriffe „behandeln", „heilen", „lindern", „therapieren" suchen — falls vorhanden, in Wahrnehmungsformel umschreiben.

---

## 10. Referenzen, Standards, Doku-Quellen <a id="10-referenzen"></a>

### SEO
- [Google Search Central — SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)
- [Schema.org HealthAndBeautyBusiness](https://schema.org/HealthAndBeautyBusiness)
- [Schema.org Service](https://schema.org/Service)
- [Schema.org FAQPage](https://schema.org/FAQPage)
- [Astro Sitemap Integration](https://docs.astro.build/en/guides/integrations-guide/sitemap/)

### GEO / AI-Search
- [llmstxt.org — llms.txt Standard](https://llmstxt.org)
- [C2PA Content Credentials Spec 2.0](https://c2pa.org/specifications/specifications/2.0/specs/C2PA_Specification.html)
- [EU AI Act Art. 50 — Volltext](https://artificialintelligenceact.eu/article/50/)

### Tools
- [Google PageSpeed Insights](https://pagespeed.web.dev)
- [Schema Validator](https://validator.schema.org/)
- [Rich Results Test](https://search.google.com/test/rich-results)
- [Klaro Cookie Manager](https://heyklaro.com)
- [Cloudflare Turnstile](https://www.cloudflare.com/products/turnstile/)

### Rechtliches
- [HWG — Heilmittelwerbegesetz](https://www.gesetze-im-internet.de/heilmwerbg/)
- [DSGVO — Volltext](https://dsgvo-gesetz.de)
- [GenDG — Gendiagnostikgesetz](https://www.gesetze-im-internet.de/gendg/)
- [Kosmetikverordnung EU 1223/2009](https://eur-lex.europa.eu/legal-content/DE/TXT/?uri=CELEX:02009R1223-20240517)

---

## Schluss-Notiz

Der nächste Build, der die Sprint-1-Items abgeschlossen hat, wird in Google Search Console nach 7–14 Tagen erste Performance-Daten zeigen. Echtes Ranking auf „Longevity-Studio Minden" und „Kryotherapie Minden" wird realistisch ab 6–10 Wochen sichtbar — vorausgesetzt Custom Domain ist aktiv und die Sitemap wird abgearbeitet.

Bei Fragen oder wenn du einen einzelnen Sprint gemeinsam durchziehen willst, kannst du jederzeit wieder eine Session starten. Alle Code-Änderungen sind im Repo nachvollziehbar; das Push-Setup (`api-push-with-delete.py`) erlaubt Adds und Deletes in einem atomaren Commit.

Stand: 1. Mai 2026, 17:00 Uhr.
