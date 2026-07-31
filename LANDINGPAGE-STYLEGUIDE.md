# Feminess Landingpage – Design- & Style-Guide

Abgeleitet von `geburtstag-deal/index.html`. Dieser Guide ist so geschrieben, dass er **1:1 auf eine neue Landingpage übertragen** werden kann – als Briefing für eine KI oder als Checkliste für einen Designer/Entwickler.

> **Stand:** aktualisiert nach mehreren Überarbeitungsrunden der Geburtstags-Deal-Seite. Wichtigste Änderungen gegenüber der ursprünglichen Version: Rosegold-Verlaufstext wurde aus Überschriften/Preisen/Namen entfernt (siehe Abschnitt 5), Fließtext auf dunklem Hintergrund ist jetzt **Weiß** statt Mid-Gray, Währung wird als "EUR" ausgeschrieben statt "€", und es gibt eine neue Regel für Bindestriche in Cormorant-Garamond-Überschriften (Abschnitt 3).

---

## 1. Grundphilosophie

- **Zwei Schriften, klar getrennte Rollen:** Serif für Emotion/Überschriften, Sans-Serif für alles Lesbare.
- **Zwei Hintergrundfarben, im Wechsel:** Helle Sektionen (Weiß/Off-White) und dunkle Sektionen (Tannengrün) lösen sich ab – das gibt der Seite Rhythmus beim Scrollen.
- **Der Rosegold-Verlauf ist reserviert für Buttons und Flächen** (Top-Banner-Hintergrund, CTA-Buttons) – **nicht mehr für Text**. Früher wurde er auch für hervorgehobene Wörter in Überschriften, Preise und Testimonial-Namen verwendet; das wurde bewusst entfernt (schlechte Lesbarkeit/Kontrast). Hervorhebung in Text läuft heute über **Fettung (`<strong>`)** und Farbe, nicht mehr über den Verlauf.
- **Hierarchie kommt fast nur über die Überschriften.** Der Fließtext läuft (bewusst) fast überall in derselben Größe (18px) – Unterschiede entstehen durch Farbe (hell/dunkel je nach Sektion) und durch Bold, nicht durch viele verschiedene Schriftgrößen.

---

## 2. Farbpalette

```css
:root {
  --teal:       #257c6c;   /* mittleres Teal – Akzent, Icons, Trennlinien */
  --teal-dark:  #1b5c50;   /* Haupt-Markenfarbe: dunkles Tannengrün */
  --teal-light: #f8f6f2;   /* = --off-white, für "helle Schrift auf Teal" */
  --teal-pale:  #b8ddd8;   /* helles Mint – dünne Trennlinien zwischen Sektionen */
  --rose:       #cf5a73;   /* Rose/Terrakotta – dekorative Glows */
  --rose-light: #e8a0b0;   /* helles Rose – Kreuz-Icons/Label in "Nein"-Boxen auf dunklem Grund */
  --sand:       #c2ab8d;   /* Sand – Sterne-Bewertungen */
  --black:      #070808;   /* Footer-Hintergrund */
  --dark:       #0d2420;   /* fast schwarzes Grün – Buttontext, kleine Details */
  --off-white:  #f8f6f2;   /* Standard "helle Sektion"-Hintergrund */
  --cream:      #f0f5f4;   /* Hover-Zustand auf Off-White-Elementen */
  --beige:      #ddecea;   /* dünne Trennlinien zwischen Sektionen (hell) */
  --warm-gray:  #5a7a74;   /* Fließtext auf HELLEM Hintergrund (Standard) */
  --mid-gray:   #9ab8b4;   /* historisch: Fließtext auf dunklem Hintergrund – wird NICHT mehr verwendet, siehe Abschnitt 4 */
}
```

**Der Rosegold-Verlauf** (kein CSS-Variable, wird als literaler Gradient überall wiederholt, da `background-clip:text` keine Variablen mit `var()` in manchen Browsern zuverlässig verarbeitet):

```css
background: linear-gradient(90deg, #a0685a 0%, #d4a090 25%, #f0ccc0 50%, #d4a090 75%, #a0685a 100%);
```

Verwendung: **nur noch** CTA-Button-Hintergründe und der Top-Banner-Hintergrund. **Nicht mehr** für Text (siehe Abschnitt 5).

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
| **Cormorant Garamond** (serif) | NUR Überschriften: h1, h2, Karten-Titel, FAQ-Fragen, Zitat-Blöcke |
| **Montserrat** (sans-serif) | ALLES andere: Fließtext, Buttons, Labels, Footer, Countdown, Preis-Zahlen |

### ⚠️ Wichtige Sonderregel: Bindestriche in Cormorant-Überschriften

Der Bindestrich-Glyph von Cormorant Garamond sieht in Überschriften/Titeln optisch unpassend aus (zu hoch, zu dünn im Kontrast zu den Serifen). **Jeder Bindestrich innerhalb eines Cormorant-Garamond-Elements** (h1, h2, Karten-`<h3>`, FAQ-`<summary>`) wird deshalb einzeln in Montserrat gesetzt:

```html
<h2>Dein komplettes <em>Geburtstags<span style="font-family:'Montserrat', sans-serif;">-</span>Special</em></h2>
```

Das gilt auch für Bindestriche, die als eigenständiges Trennzeichen zwischen zwei Satzteilen stehen (" - "), nicht nur für Wort-interne Bindestriche.

**Falle bei `<summary>`-Elementen:** `.faq-item summary` ist `display:flex; justify-content:space-between;`, damit Frage-Text links und das `+`-Icon rechts sitzen. Wird nur ein *Teil* des Fragetexts in ein `<span>` gepackt (z. B. nur der Bindestrich), erzeugt der Browser für Text-vor-Span, Span und Text-nach-Span **drei separate Flex-Items** – `space-between` reißt dann große, falsche Lücken zwischen den Textteilen auf. **Fix:** den kompletten Fragetext in einen äußeren Wrapper-`<span>` packen, der Bindestrich-Span kommt *innerhalb* dieses Wrappers:

```html
<summary><span>Wann endet das Geburtstags<span style="font-family:'Montserrat', sans-serif;">-</span>Special?</span></summary>
```

So zählt der gesamte Fragetext als **ein** Flex-Item, nur Text und `+`-Icon werden auseinandergezogen.

### Kursivschrift – die eine bewusste Ausnahme

Global gilt `em, i { font-style: normal; }` – "kursiv" wird auf dieser Seite normalerweise **nicht** durch Schrägstellung dargestellt (`<em>` diente früher der Rosegold-Farbe, siehe Abschnitt 5). Eine Ausnahme: wörtliche Zitate von Kundinnen im Fließtext werden **wirklich kursiv** gesetzt, per Inline-Override:

```html
<p><em style="font-style: italic;">„Marina, ich hab in den letzten zwei Jahren wirklich alles gegeben…"</em></p>
```

### Größen-/Gewichts-Tabelle

| Element | Schrift | Desktop | Mobil | Weight |
|---|---|---|---|---|
| Top-Banner Text | Montserrat | 18px | 10px | 400 |
| Top-Banner Countdown-Ziffern | Montserrat | 18px | 13px | 600 |
| Top-Banner Countdown-Label | Montserrat | 10px | 7px | 700 |
| h1 (Hero-Überschrift) | Cormorant Garamond | 48px | 43px | 600 |
| h2 (Standard-Sektions-Überschrift) | Cormorant Garamond | 48px | 36px | 600 |
| h2 in besonders textreichen Sektionen (z. B. Ergebnis-Abschnitt, Final-CTA) | Cormorant Garamond | 48px | individuell kleiner (27–30px), damit die Headline nicht mehr als ~2–3 Zeilen umfasst | 600 |
| Karten-Titel (Boni-Karten h3) | Cormorant Garamond | 42px | 30px | 600 |
| Speaker-Name (h3) | Cormorant Garamond | 48px | 48px | 400 |
| FAQ-Frage (`summary`) | Cormorant Garamond | 32px | 33px | 400 |
| Zitat-Block (Quote) | Cormorant Garamond | 28px | 24px | 600 |
| Für-dich-Box-Header | Cormorant Garamond | 24px | 24px | 700 |
| Body-Fließtext (Absätze, Listen) | Montserrat | 18px | 18px | 400 |
| Preis-Zahlen (z. B. "333 EUR") | Montserrat | 44–72px je Kontext | verkleinert, ggf. `white-space:nowrap`, wenn Text länger wird | 600 |
| Buttons | Montserrat | 18px | 15px | 700 |
| Countdown-Ziffern (Final-CTA) | Montserrat | 18px | 18px | 400 |
| Countdown-Label (Final-CTA, Tage/Std/Min) | Montserrat | **11px – kleiner als die Ziffern** | 11px | 700 |
| Footer-Links/Copyright | Montserrat | 18px | 13px | 700 |
| Kleine Eyebrows/Kicker (`.section-label`) | Montserrat | 10–12px | – | 700, Uppercase, Letterspacing 3–4px |

**Prinzip:** Fast der gesamte Fließtext läuft einheitlich auf **18px** – Hierarchie entsteht über die Cormorant-Überschriften, nicht über gestaffelte Body-Größen. Mobile Headlines werden bewusst **größer** relativ zur Desktop-Version gestaffelt als man erwarten würde (näher an der Desktop-Größe), damit sie auf kleinen Screens noch genug Präsenz haben – aber wird eine Headline dadurch zu lang (mehr als 2–3 Zeilen), bekommt sie eine eigene, kleinere Mobile-Override-Regel (siehe Tabelle oben).

**Countdown-Sonderfall:** Anders als man intuitiv erwarten würde, ist im Final-CTA-Countdown das Unit-Label ("TAGE", "STD" …) **kleiner** als die Ziffer darüber/darunter (11px vs. 18px) – die Ziffer soll dominieren, das Label ist nur unterstützende Beschriftung.

---

## 4. Textfarben je nach Sektion

**Auf hellem Hintergrund** (`--off-white` / `#fff`):
- Überschriften: `#0a3828`
- Fließtext: `var(--warm-gray)` als Standard – **Ausnahme:** der Haupt-Fließtext-Abschnitt (`.text-inner p`) und der Garantie-Text (`.guarantee-text`) laufen in `#0a3828` (dunkler, kräftiger) statt `--warm-gray`
- Bold/`<strong>`: `#0a3828`

**Auf dunklem Hintergrund** (`--teal-dark`):
- Überschriften: `#fff`
- Fließtext: **`#fff`** (nicht mehr `var(--mid-gray)` – die Variable existiert noch, wird aber aktuell nirgends mehr für Text verwendet, da Weiß auf Tannengrün besser lesbar ist)
- Bold/`<strong>`: `#fff`

**Karten *innerhalb* einer dunklen Sektion** (z. B. Boni-Karte auf grünem Hintergrund):
- Karte selbst: `#fff` (hell, damit sie sich abhebt)
- Karten-Überschrift: `#0a3828`
- Karten-Text: `var(--warm-gray)`
- Große dekorative Nummer (z. B. "1", "2" im Hintergrund der Karte): `rgba(27,92,80,0.18)`

**Blocksatz:** Der Haupt-Fließtext (`.text-inner p`) und der Garantie-Text (`.guarantee-text`) stehen bewusst im **Blocksatz** (`text-align: justify`), nicht linksbündig – das unterscheidet diese beiden "Lesetext"-Abschnitte optisch von den kürzeren Listen-/Card-Texten, die linksbündig bleiben.

---

## 5. Was wird hervorgehoben – und wie

| Hervorhebung | Wann einsetzen | Umsetzung |
|---|---|---|
| **Bold (`<strong>`)** | Der wichtigste Teilsatz in einem Absatz (nicht ganze Absätze); Zahlen/Werte in Testimonials (z. B. "**260.000 EUR**", "**über eine Million.**") | `font-weight:700`, Farbe = normale Überschriften-/Fließtextfarbe der Sektion (siehe Abschnitt 4), **keine** eigene Akzentfarbe |
| **`<em>` in Überschriften** | Ein einzelnes Schlüsselwort/Kurzphrase in einer `<h1>`/`<h2>`/Karten-Titel, das den Kern des Angebots trägt | `<em>` verwenden, `font-style:normal; font-weight:600; color:inherit;` – **KEIN** Rosegold-Verlauf mehr, das Wort übernimmt einfach die Farbe der umgebenden Überschrift |
| *Kursiv im klassischen Sinn* | **nur für wörtliche Kundinnen-Zitate** im Fließtext (siehe Abschnitt 3) | `<em style="font-style: italic;">` als bewusster Inline-Override |
| Zitat-Block (eigene Box) | Ein zentraler, plakativer Ein-Satz-Gedanke mitten im Fließtext | Eigene `<div>` mit Sektionsfarbe (`--teal-dark`) als Hintergrund, Cormorant 28px/600, weißer Text, zentriert |
| Uppercase + Letterspacing | Buttons, kleine Eyebrows/Kicker, Box-Header (Für-dich Ja/Nein) | `text-transform:uppercase; letter-spacing:1–4px;` |

**Wichtig – Rosegold-Verlaufstext ist obsolet:** Frühere Versionen dieser Seite nutzten `background-clip:text` mit dem Rosegold-Verlauf für `<em>`-Wörter in Überschriften, für Preis-Zahlen und für Testimonial-Autorennamen. Das wurde vollständig entfernt: Preis-Zahlen sind jetzt **Weiß** auf dunklem Grund, Testimonial-Namen laufen in `var(--warm-gray)`, und `<em>` in Überschriften übernimmt per `color:inherit` einfach die Farbe der Überschrift. Der Rosegold-Verlauf bleibt ausschließlich Buttons und dem Top-Banner-Hintergrund vorbehalten.

**Nie verwenden:** unterschiedliche Fließtextgrößen als Hervorhebung, Unterstreichung (außer `text-decoration:line-through` für durchgestrichene alte Preise), Rosegold-Verlauf auf Text, mehr als eine Akzentfarbe gleichzeitig.

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

- Button-Text ist immer **Call-to-Action-artig formuliert und komplett in Großbuchstaben** ("JETZT SPECIAL SICHERN", "HIER PLATZ SICHERN", "ICH WILL DAS SPECIAL", "ICH BIN DABEI") – nie neutral wie "Weiter" oder "Absenden". Kurze, energische 2–4-Wort-Imperative bevorzugt.
- Zusatzinfos zum Angebot (z. B. Garantie-Hinweis, Ratenzahlung) stehen **niemals als eigenes Badge über dem Button**, sondern als schlichte Textzeile **darunter**, in der Sektionsfarbe für Fließtext (siehe Abschnitt 4).
- Wenn eine Zusatzinfo-Zeile mehrere Aussagen enthält, die eigentlich getrennt wirken sollen, werden sie **nicht** mit Satzzeichen (`-`, `·`) getrennt, sondern als **eigene `<p>`-Elemente** untereinander gesetzt, mit leicht reduziertem Abstand über einen Adjacent-Sibling-Selektor (`.final-note + .final-note { margin-top: 6px; }`).

---

## 7. Wiederkehrende Bausteine

**Ja/Nein-Vergleichsbox** ("Ist das für dich?"): zwei Boxen übereinander, deutlich getönter Hintergrund – Ja-Box sanftes Grün (`rgba(37,124,108,0.28)`, Rahmen `rgba(94,198,179,0.35)`), Nein-Box sanftes Rose (`rgba(207,90,115,0.22)`, Rahmen `rgba(207,90,115,0.35)`). Häkchen `✓` bzw. Kreuz `✕` als `::before`-Content vor jedem Listenpunkt, Box-Header-Farbe passend zum Ton (Ja: `--teal-light`, Nein: `--rose-light`).

**FAQ-Akkordeon:** natives `<details>`/`<summary>`, Frage in Cormorant Garamond (32px Desktop / 33px Mobil), `+`/`-` als `::after`-Content statt Icon-Font. Enthält ein `<summary>` einen Bindestrich oder eine Inline-Font-Änderung (z. B. "333 EUR" in Montserrat), **muss** der komplette Fragetext in einen Wrapper-`<span>` gepackt werden (siehe Abschnitt 3, Flex-Falle).

**Testimonial-Karten:** 3-spaltiges Grid (Desktop), Off-White-Karten mit dünner Top-Border in Terrakotta (`#c47868`), 5 Sterne in Sand-Farbe, Autorenname in `var(--warm-gray)` + Uppercase + Letterspacing (kein Rosegold mehr). Konkrete Erfolgszahlen im Zitat-Text (Umsatz-Beträge, "über eine Million.") werden **fett** hervorgehoben.

**Countdown:** In der Top-Banner-Version sind Ziffern und Label eng aufeinander abgestimmt (13px/7px Mobil). Im großen Final-CTA-Countdown ist das Label bewusst **kleiner** als die Ziffer (11px vs. 18px) – die Ziffer dominiert.

**Fly-in-Animation für Listen** (z. B. Nutzen-Aufzählung): Items starten `opacity:0; transform:translateX(-32px)`, IntersectionObserver fügt beim Scrollen-ins-Bild eine `.is-visible`-Klasse hinzu, jedes Item bekommt eigenen `transition-delay` (gestaffelt in ~0.4s-Schritten, Transition-Dauer ~1.2s) – wichtig: Listenpunkte in einen eigenen Wrapper packen, damit `:nth-child` nicht durch Überschrift/Spacer-Divs verschoben wird.

**Absätze statt Satzzeichen-Trenner:** Wo früher ein Satz mit `·` oder `-` zwei Teilaussagen verband ("Noch bis 04.08.2026, 23:59 Uhr · nur 10 Plätze"), werden diese heute als getrennte `<p>`-Elemente untereinander gesetzt – das wirkt ruhiger und lässt sich pro Zeile individuell stylen.

---

## 8. Layout & Spacing

- Sektionen: `padding: 88–110px 0` Desktop, `64–72px 0` Mobil.
- Inhaltsbreite: `max-width` je nach Sektion 600–1100px, `margin:0 auto`, seitliches Padding 40px (Desktop) / 20px (Mobil).
- Trennlinien zwischen Sektionen: `border-top: 2px solid var(--teal-pale)` bzw. `border-bottom: 1px solid var(--beige)` – dünn, kaum sichtbar, kein harter Schnitt.
- Hero: zweispaltiges Grid (Text ~48%, Bild ~52%), **feste Pixel-Höhe** statt `auto` (verhindert, dass ein hochformatiges Foto mit viel Kopffreiraum die ganze Sektion aufbläht – object-fit:cover + object-position:center top schneidet dann sauber von unten ab). Auf Mobil wird der dunkle Verlaufs-"Schleier" über dem Hero-Bild (`.hero-image::before`) per `display:none` entfernt, damit das Foto dort ungetrübt zu sehen ist.
- Buttons/CTAs: mehrfach wiederholt (Hero, nach Intro-Text, nach jeder Nutzen-Sektion, Final-CTA, Floating-CTA unten rechts nach Scroll-Trigger).
- Lange Preis-/Value-Texte, die auf Mobil umbrechen würden (z. B. "Für dich nur 333 EUR"), bekommen eine eigene, kleinere Mobile-Font-Size **plus** `white-space:nowrap`, damit sie garantiert in einer Zeile bleiben statt hässlich umzubrechen.

## 9. Responsive Breakpoints

- `900px`: Hero wechselt von 2-spaltig auf gestapelt (Bild unter dem Text), Testimonials von 3 auf 2 Spalten, Speaker-Grid stapelt.
- `600px`: h2 standardmäßig 36px, h1 43px – Sektionen mit besonders langem Headline-Text bekommen individuelle kleinere Overrides (siehe Tabelle in Abschnitt 3). Top-Banner-Countdown läuft `flex-wrap:nowrap` in einer Zeile. Buttons `width:100%`.

---

## 10. Kurz-Checkliste für eine neue Landingpage

1. Google-Fonts-Link (Cormorant Garamond + Montserrat) einbinden, `:root`-Variablen 1:1 übernehmen.
2. Body-Default: Montserrat 18px, Farbe `#0a3828` auf `--off-white`-Hintergrund.
3. Jede `<h1>`/`<h2>`/Karten-Titel: Cormorant Garamond, 48px/36px mobil (bei Bedarf pro Sektion kleiner), Weight 600, ein Schlüsselwort als `<em>` mit `color:inherit` – **kein** Rosegold-Text mehr.
4. Jeden Bindestrich innerhalb einer Cormorant-Überschrift einzeln in Montserrat setzen (siehe Abschnitt 3) – bei `<summary>`-Elementen den ganzen Text in einen Wrapper-Span packen.
5. Sektionen alternierend hell/dunkel durchtakten; bei dunkel **immer** Textfarben-Set tauschen (Fließtext = Weiß, nicht Mid-Gray) und Karten hell machen.
6. Ein einziger Button-Stil (Pille, Rosegold, dunkler Text, Uppercase, Pulsieren) für alle CTAs.
7. Zusatzinfos/Garantien als eigene Text-Zeile(n) unter dem Button, nicht als Badge davor, nicht mit `·`/`-` zusammengequetscht.
8. Fließtext konsequent bei 18px belassen, keine Zwischengrößen einführen. Währungsbeträge als "EUR" ausschreiben, nicht "€".
