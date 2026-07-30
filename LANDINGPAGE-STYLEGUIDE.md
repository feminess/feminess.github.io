# Feminess Landingpage – Design- & Style-Guide

Abgeleitet von `geburtstag-deal/index.html`. Dieser Guide ist so geschrieben, dass er **1:1 auf eine neue Landingpage übertragen** werden kann – als Briefing für eine KI oder als Checkliste für einen Designer/Entwickler.

---

## 1. Grundphilosophie

- **Zwei Schriften, klar getrennte Rollen:** Serif für Emotion/Überschriften, Sans-Serif für alles Lesbare.
- **Zwei Hintergrundfarben, im Wechsel:** Helle Sektionen (Weiß/Off-White) und dunkle Sektionen (Tannengrün) lösen sich ab – das gibt der Seite Rhythmus beim Scrollen.
- **Ein Akzent für alles Wichtige:** Der Rosegold-Verlauf markiert *überall* die Kaufentscheidung – Buttons, Preise, hervorgehobene Wörter in Überschriften. Er kommt nirgendwo sonst vor, dadurch bleibt er als "hier ist der nächste Schritt"-Signal eindeutig.
- **Hierarchie kommt fast nur über die Überschriften.** Der Fließtext läuft (bewusst) fast überall in derselben Größe (18px) – Unterschiede entstehen durch Farbe (hell/dunkel je nach Sektion) und durch Bold/Kursiv, nicht durch viele verschiedene Schriftgrößen.

---

## 2. Farbpalette

```css
:root {
  --teal:       #257c6c;   /* mittleres Teal – Akzent, Icons, Trennlinien */
  --teal-dark:  #1b5c50;   /* Haupt-Markenfarbe: dunkles Tannengrün */
  --teal-light: #f8f6f2;   /* = --off-white, für "helle Schrift auf Teal" */
  --teal-pale:  #b8ddd8;   /* helles Mint – dünne Trennlinien zwischen Sektionen */
  --rose:       #cf5a73;   /* Rose/Terrakotta – dekorative Glows, Kreuz-Icons */
  --sand:       #c2ab8d;   /* Sand – Sterne-Bewertungen */
  --black:      #070808;   /* Footer-Hintergrund */
  --dark:       #0d2420;   /* fast schwarzes Grün – Buttontext, kleine Details */
  --off-white:  #f8f6f2;   /* Standard "helle Sektion"-Hintergrund */
  --cream:      #f0f5f4;   /* Hover-Zustand auf Off-White-Elementen */
  --beige:      #ddecea;   /* dünne Trennlinien zwischen Sektionen (hell) */
  --warm-gray:  #5a7a74;   /* Fließtext auf HELLEM Hintergrund */
  --mid-gray:   #9ab8b4;   /* Fließtext auf DUNKLEM Hintergrund */
}
```

**Der Rosegold-Verlauf** (kein CSS-Variable, wird als literaler Gradient überall wiederholt, da `background-clip:text` keine Variablen mit `var()` in manchen Browsern zuverlässig verarbeitet):

```css
background: linear-gradient(90deg, #a0685a 0%, #d4a090 25%, #f0ccc0 50%, #d4a090 75%, #a0685a 100%);
```

Verwendung: **jeder** CTA-Button-Hintergrund, jedes hervorgehobene `<em>`-Wort in Überschriften, Preis-Anzeigen, Testimonial-Autorennamen, das "Nein"-Box-Label in Vergleichs-Boxen.

### Sektions-Hintergründe (Reihenfolge auf der Seite, alternierend)

| Sektion | Hintergrund |
|---|---|
| Top-Banner | Rosegold-Verlauf |
| Hero | `--teal-dark` (#1b5c50), einfarbig |
| Haupt-Fließtext | `--off-white` |
| Preis-Reveal-Card | `--teal-dark`, einfarbig |
| Ergebnis-/Nutzen-Liste | `#fff` |
| Für-dich-Vergleich | `--teal-dark` |
| Garantie | `#fff` |
| Boni/Leistungen | `--teal-dark` |
| Testimonials | `#fff` |
| Speaker/Team | `--teal-dark` |
| FAQ | `#fff` |
| Final-CTA | `--teal-dark` |
| Footer | `--black` |

**Regel:** Wenn eine Sektion dunkel ist (`--teal-dark`), **muss** der komplette Text-Farbsatz umgekehrt werden (siehe Abschnitt 4). Karten *innerhalb* einer dunklen Sektion (z. B. Boni-Karten) werden dann selbst **hell** (weiß), damit sie sich vom Sektionshintergrund abheben – nicht dieselbe dunkle Farbe wie die Sektion verwenden.

---

## 3. Schriftsystem

**Google Fonts Import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400;1,600&family=Montserrat:wght@400;600;700&display=swap" rel="stylesheet">
```

| Schrift | Rolle |
|---|---|
| **Cormorant Garamond** (serif) | NUR Überschriften: h1, h2, Preis-Anzeigen im Sinne einer Headline, Karten-Titel, FAQ-Fragen, Zitat-Blöcke |
| **Montserrat** (sans-serif) | ALLES andere: Fließtext, Buttons, Labels, Footer, Countdown |

### Größen-/Gewichts-Tabelle

| Element | Schrift | Desktop | Mobil | Weight |
|---|---|---|---|---|
| Top-Banner Text/Countdown | Montserrat | 18px | 12px | 400 / 600 |
| h1 (Hero-Überschrift) | Cormorant Garamond | 48px | 35px | 600 |
| h2 (alle Sektions-Überschriften) | Cormorant Garamond | 48px | 28px | 600 |
| Karten-Titel (z. B. Boni-Karten h3) | Cormorant Garamond | 48px | 28px | 600 |
| Zitat-Block (Quote) | Cormorant Garamond | 28px | 24px | 600 |
| Für-dich-Box-Header | Cormorant Garamond | 24px | 24px | 700 |
| Body-Fließtext (Absätze, Listen) | Montserrat | 18px | 18px | 400 |
| Buttons | Montserrat | 18px | 15px | 700 |
| Countdown-Ziffern | Montserrat | 18px | 18px | 400 |
| Countdown-Label (Tage/Std/Min) | Montserrat | 18px | 18px | 700 |
| Footer-Links/Copyright | Montserrat | 18px | 13px | 700 |
| Kleine Eyebrows/Kicker (`.section-label`) | Montserrat | 10–12px | – | 700, Uppercase, Letterspacing 3–4px |

**Prinzip:** Fast der gesamte Fließtext läuft einheitlich auf **18px** – Hierarchie entsteht über die Cormorant-Überschriften (48px), nicht über gestaffelte Body-Größen. Kleine Eyebrows/Kicker (winzige Caps-Labels wie "AN DICH") sind die einzige bewusste Ausnahme nach unten.

---

## 4. Textfarben je nach Sektion

**Auf hellem Hintergrund** (`--off-white` / `#fff`):
- Überschriften: `#1b5c50`
- Fließtext: `var(--warm-gray)`
- Bold/`<strong>`: `#1b5c50`

**Auf dunklem Hintergrund** (`--teal-dark`):
- Überschriften: `#fff`
- Fließtext: `var(--mid-gray)`
- Bold/`<strong>`: `#fff`

**Karten *innerhalb* einer dunklen Sektion** (z. B. Boni-Karte auf grünem Hintergrund):
- Karte selbst: `#fff` (hell, damit sie sich abhebt)
- Karten-Überschrift: `#1b5c50`
- Karten-Text: `var(--warm-gray)`
- Große dekorative Nummer (z. B. "1", "2" im Hintergrund der Karte): `rgba(27,92,80,0.18)`

---

## 5. Was wird hervorgehoben – und wie

| Hervorhebung | Wann einsetzen | Umsetzung |
|---|---|---|
| **Bold (`<strong>`)** | Der wichtigste Teilsatz in einem Absatz (nicht ganze Absätze) | `font-weight:700`, Farbe = normale Überschriftenfarbe der Sektion (siehe oben), **keine** eigene Akzentfarbe |
| **Rosegold-Verlaufstext** | Ein einzelnes Wort/Kurzphrase in einer `<h1>`/`<h2>`, das den Kern des Angebots trägt (z. B. "*Umsatz-Mauer*"); Preis-Zahlen; Autorennamen bei Testimonials | `<em>` verwenden, `font-style:normal`, Gradient via `background-clip:text` |
| *Kursiv im klassischen Sinn* | **wird nicht verwendet** | `em, i { font-style: normal; }` global gesetzt – "kursiv" bedeutet auf dieser Seite immer "Rosegold-Verlaufsfarbe", nie echte Schrägstellung |
| Zitat-Block (eigene Box) | Ein zentraler, plakativer Ein-Satz-Gedanke mitten im Fließtext | Eigene `<div>` mit Sektionsfarbe (`--teal-dark`) als Hintergrund, Cormorant 28px/600, weißer Text, zentriert |
| Uppercase + Letterspacing | Buttons, kleine Eyebrows/Kicker, Box-Header (Für-dich Ja/Nein) | `text-transform:uppercase; letter-spacing:1–4px;` |

**Nie verwenden:** unterschiedliche Fließtextgrößen als Hervorhebung, Unterstreichung (außer `text-decoration:line-through` für durchgestrichene alte Preise), mehr als eine Akzentfarbe gleichzeitig.

---

## 6. Buttons

Ein einziger Button-Typ für alle CTAs (Hero-Button, Inline-CTA, Floating-CTA) – **voll abgerundete Pille**, nicht nur leicht abgerundetes Rechteck:

```css
.btn-cta {
  display: inline-block;
  background: linear-gradient(90deg, #a0685a 0%, #d4a090 25%, #f0ccc0 50%, #d4a090 75%, #a0685a 100%);
  color: var(--dark);              /* dunkler Text auf dem hellen Verlauf, NICHT weiß */
  padding: 20px 48px;
  border-radius: 999px;             /* komplett rund = Pillenform */
  font-family: 'Montserrat', sans-serif;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  border: none;
  cursor: pointer;
  animation: pulse-btn 2.2s ease-in-out infinite;   /* dezentes Pulsieren, zieht den Blick */
}
.btn-cta:hover { opacity: 0.88; transform: translateY(-1px); animation: none; }

@keyframes pulse-btn {
  0%, 100% { transform: scale(1);     box-shadow: 0 6px 28px rgba(160,104,90,0.40); }
  50%      { transform: scale(1.04);  box-shadow: 0 10px 36px rgba(160,104,90,0.58); }
}
```

- Button-Text ist immer **Call-to-Action-artig formuliert und komplett in Großbuchstaben** ("JETZT SPECIAL SICHERN", "ICH WILL DEN DEAL", "YES, DAS WILL ICH") – nie neutral wie "Weiter" oder "Absenden".
- Zusatzinfos zum Angebot (z. B. Garantie-Hinweis, Ratenzahlung) stehen **niemals als eigenes Badge über dem Button**, sondern als schlichte Textzeile **darunter**, in der Sektionsfarbe für Fließtext (`--warm-gray` auf hell / `--mid-gray` auf dunkel).

---

## 7. Wiederkehrende Bausteine

**Ja/Nein-Vergleichsbox** ("Ist das für dich?"): zwei Boxen nebeneinander/übereinander, dezent getönter Hintergrund (`rgba(255,255,255,0.06)` auf dunklem Grund), Rahmenfarbe unterscheidet Ja (teal) von Nein (rose). Häkchen `✓` bzw. Kreuz `✕` als `::before`-Content vor jedem Listenpunkt.

**FAQ-Akkordeon:** natives `<details>`/`<summary>`, Frage in Cormorant Garamond 24px, `+`/`–` als `::after`-Content statt Icon-Font.

**Testimonial-Karten:** 3-spaltiges Grid (Desktop), Off-White-Karten mit dünner Top-Border in Terrakotta (`#c47868`), 5 Sterne in Sand-Farbe, Autorenname in Rosegold-Verlauf + Uppercase + Letterspacing.

**Countdown:** Ziffern und Label **gleich groß** (18px) – keine riesigen Zahlen mit winzigem Label, das Label ist sogar fetter (700) als die Ziffern (400).

**Fly-in-Animation für Listen** (z. B. Nutzen-Aufzählung): Items starten `opacity:0; transform:translateX(-32px)`, IntersectionObserver fügt beim Scrollen-ins-Bild eine `.is-visible`-Klasse hinzu, jedes Item bekommt eigenen `transition-delay` (gestaffelt in ~0.4s-Schritten, Transition-Dauer ~1.2s) – wichtig: Listenpunkte in einen eigenen Wrapper packen, damit `:nth-child` nicht durch Überschrift/Spacer-Divs verschoben wird.

---

## 8. Layout & Spacing

- Sektionen: `padding: 88–110px 0` Desktop, `64–72px 0` Mobil.
- Inhaltsbreite: `max-width` je nach Sektion 600–1100px, `margin:0 auto`, seitliches Padding 40px (Desktop) / 20px (Mobil).
- Trennlinien zwischen Sektionen: `border-top: 2px solid var(--teal-pale)` bzw. `border-bottom: 1px solid var(--beige)` – dünn, kaum sichtbar, kein harter Schnitt.
- Hero: zweispaltiges Grid (Text ~48%, Bild ~52%), **feste Pixel-Höhe** statt `auto` (verhindert, dass ein hochformatiges Foto mit viel Kopffreiraum die ganze Sektion aufbläht – object-fit:cover + object-position:center top schneidet dann sauber von unten ab).
- Buttons/CTAs: mehrfach wiederholt (Hero, nach Intro-Text, nach jeder Nutzen-Sektion, Final-CTA, Floating-CTA unten rechts nach Scroll-Trigger).

## 9. Responsive Breakpoints

- `900px`: Hero wechselt von 2-spaltig auf gestapelt (Bild unter dem Text), Testimonials von 3 auf 2 Spalten, Speaker-Grid stapelt.
- `600px`: Alle h2 auf 28px, h1 auf 35px, Buttons `width:100%`, Countdown/Footer-Schrift verkleinert.

---

## 10. Kurz-Checkliste für eine neue Landingpage

1. Google-Fonts-Link (Cormorant Garamond + Montserrat) einbinden, `:root`-Variablen 1:1 übernehmen.
2. Body-Default: Montserrat 18px, Farbe `#1b5c50` auf `--off-white`-Hintergrund.
3. Jede `<h1>`/`<h2>`/Karten-Titel: Cormorant Garamond, 48px/28px mobil, Weight 600, ein Schlüsselwort als `<em>` im Rosegold-Verlauf.
4. Sektionen alternierend hell/dunkel durchtakten; bei dunkel **immer** Textfarben-Set tauschen (siehe Abschnitt 4) und Karten hell machen.
5. Ein einziger Button-Stil (Pille, Rosegold, dunkler Text, Uppercase, Pulsieren) für alle CTAs.
6. Zusatzinfos/Garantien als Text unter dem Button, nicht als Badge davor.
7. Fließtext konsequent bei 18px belassen, keine Zwischengrößen einführen.
