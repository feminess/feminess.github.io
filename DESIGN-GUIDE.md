# Feminess Landingpage – Design-Guide

Dieser Guide beschreibt das Design-System der Feminess-Landingpages (Referenz: `geburtstag/index.html`). Er ist dafür gedacht, Claude als Kontext zu geben, wenn eine **neue** Landingpage im selben Look gebaut werden soll. Alles hier ist eigenständiges HTML/CSS/JS ohne Build-Step – jede Seite ist eine einzelne `index.html`-Datei mit Inline-`<style>` und `<script>`.

Wenn du eine neue Landingpage baust: Kopiere die relevanten Code-Blöcke aus diesem Guide, passe Inhalte/Bilder/Formular-ID an, und behalte die Struktur bei. Nicht das Layout neu erfinden.

---

## 1. Stimmung

Warm, persönlich, leicht luxuriös. Dunkelgrüner Markenton als Anker (Header, Hero, große Flächen), Rosegold als Akzent für Emotion/Highlights (nie als Fläche, nur als Text-Verlauf oder Button-Glow), viel Weißraum, große fette Headlines, informelle Du-Ansprache im Fließtext.

---

## 2. Farben

Immer als CSS-Variablen in `:root` definieren, nie Hex-Werte doppelt im Stylesheet verstreuen. Diese Seite nutzt bewusst **zwei unterschiedliche, verwandte Grüntöne** – nicht einen einzigen:

```css
:root {
  --teal:       #126D4C;  /* Smaragdgrün – Hero, Boni-Boxen, Akzent-Text, große Flächen */
  --teal-dark:  #126D4C;  /* identisch zu --teal, historisch getrennt, praktisch synonym */
  --teal-light: var(--off-white);
  --rose:       #cf5a73;  /* Popup-Rahmen, dezente rote Akzente */
  --rose-light: #e8a0b0;
  --sand:       #c2ab8d;
  --sand-light: var(--off-white);
  --black:      #070808;  /* Footer */
  --dark:       #0d2420;  /* Popup-Hintergrund, dunkles Verlaufsziel */
  --off-white:  #f8f6f2;  /* Seiten-Hintergrund */
  --cream:      #f0f5f4;
  --beige:      #ddecea;  /* dezente 1px-Trennlinien */
  --warm-gray:  #5a7a74;  /* Fließtext-Farbe (kein Schwarz!) */
  --mid-gray:   #9ab8b4;  /* sekundäre/gedimmte Texte auf dunklem Grund */
  --gradient-rosegold: linear-gradient(90deg, #f0ccc0 0%, #d4a090 50%, #a0685a 100%);
}
```

Zusätzlich **zwei fest kodierte, eigenständige Farben** (bewusst NICHT über `--teal` laufen lassen, weil sie sich vom Hero abheben sollen):

- **Top-Banner-Leiste** (ganz oben, Countdown-Zeile): `#0d4b35`
- **Volltonfarbe-Balken/Zwischenüberschriften-Bars** (z. B. `.quote-block`): `#1b5c50`
- **Button-Grundfarbe**: `#861627` (dunkles Bordeaux/Rot – bewusst NICHT grün oder rosegold, damit CTAs klar als Buttons erkennbar sind)

**Faustregel:** Hero/große Flächen = `--teal` (#126D4C). Kleinere Balken/Leisten, die sich davon abheben sollen = eigene feste Hex-Werte (`#0d4b35`, `#1b5c50`). Buttons = immer `#861627`. Rosegold nie als Fläche, nur als Text-Verlauf oder Button-Glow-Akzent.

Wenn eine neue Seite eine eigene Markenfarbe bekommen soll: nur `--teal`/`--teal-dark` austauschen, den Rest (Banner, Balken, Buttons) bewusst gegenprüfen, ob sie mitziehen oder eigenständig bleiben sollen – das ist eine Design-Entscheidung, keine automatische Ableitung.

---

## 3. Typografie

Eine einzige Schriftart für die ganze Seite: **Montserrat** (Google Fonts), keine Serifenschrift, keine zweite Displayschrift.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

```css
body {
  font-family: 'Montserrat', sans-serif;
  font-size: 18px;
  line-height: 1.75;
  background: var(--off-white);
  color: var(--teal-dark);
}
h1, h2 {
  font-family: 'Montserrat', sans-serif;
  font-size: 48px;
  font-weight: 700;
  color: var(--teal-dark); /* pro Sektion ggf. auf #fff überschreiben, siehe unten */
}
```

**Regel:** Überschriften (h1/h2) = 48px, Bold (700). Wirklich alles andere (Fließtext, Buttons, Labels, Footer, Formular) = 18px. Es gibt bewusst keine dritte Zwischengröße – das ist ein reduziertes, zweistufiges Type-System.

Anmerkung zur Schriftwahl: Ursprünglich war "Gotham Bold" für Headlines gewünscht. Das ist eine kostenpflichtige Schrift ohne Google-Fonts-Verfügbarkeit – falls eine neue Seite Gotham haben soll, braucht es entweder eine gehostete Font-Datei vom Kunden, oder man bleibt bei Montserrat Bold als kostenloser, optisch ähnlicher Alternative.

---

## 4. Signature-Technik: Rosegold-Buchstaben-Verlauf

Das Markenzeichen dieser Seiten: Hervorgehobene Wörter in Überschriften bekommen **pro Buchstabe einen eigenen vollständigen Rosegold-Verlauf** (wie das "E" im Feminess-Logo) – nicht einen einzigen Verlauf über das ganze Wort gespannt. Nur `<em>`-Text in `h1`/`h2` bekommt diese Behandlung, der Rest der Überschrift bleibt in Volltonfarbe (grün oder weiß, je nach Hintergrund).

CSS:

```css
.letter-grad {
  background: var(--gradient-rosegold);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
}
```

JS (am Ende von `<body>`, nach allen Headlines):

```html
<script>
(function() {
  function wrapLetters(node) {
    Array.from(node.childNodes).forEach(function(child) {
      if (child.nodeType === Node.TEXT_NODE) {
        var frag = document.createDocumentFragment();
        child.textContent.split('').forEach(function(ch) {
          if (ch.trim() === '') {
            frag.appendChild(document.createTextNode(ch));
          } else {
            var span = document.createElement('span');
            span.className = 'letter-grad';
            span.textContent = ch;
            frag.appendChild(span);
          }
        });
        child.parentNode.replaceChild(frag, child);
      } else if (child.nodeType === Node.ELEMENT_NODE && child.tagName !== 'BR') {
        wrapLetters(child);
      }
    });
  }
  // Scope anpassen: welche <em> sollen den Verlauf bekommen?
  document.querySelectorAll('h1 em, h2 em').forEach(wrapLetters);
})();
</script>
```

**Wichtig:** Die Überschrift selbst (h1/h2) braucht eine Fallback-`color` (z. B. `#fff` auf dunklem Grund, `var(--teal-dark)` auf hellem Grund) für den nicht-`<em>`-Text und für den Fall, dass JS nicht läuft.

Wo dieser Verlauf **nicht** hinsoll: normale Buttons, Fließtext-Hervorhebungen (`<strong>`) – die nutzen stattdessen einfach `var(--teal-dark)` als Volltonfarbe.

---

## 5. Buttons

Alle CTAs (primär, floating, Formular-Submit) sehen identisch aus und teilen sich dieselben Keyframes.

```css
.btn-cta {
  display: inline-block;
  position: relative;
  overflow: hidden; /* für den Glanz-Sweep */
  background: #861627;
  color: #fff;
  padding: 20px 48px;
  border-radius: 8px;
  font-family: 'Montserrat', sans-serif;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  border: none;
  cursor: pointer;
  animation: pulse-btn 2.2s ease-in-out infinite;
}
.btn-cta:hover { opacity: 0.88; transform: translateY(-1px); animation: none; }

/* Leucht-Puls */
@keyframes pulse-btn {
  0%, 100% { transform: scale(1);     box-shadow: 0 0 3px 1px rgba(255,120,140,0.9),  0 0 20px rgba(255,80,100,0.8), 0 0 48px rgba(134,21,39,0.75), 0 6px 28px rgba(134,21,39,0.40); }
  50%       { transform: scale(1.04); box-shadow: 0 0 6px 3px rgba(255,120,140,1),    0 0 34px rgba(255,80,100,0.95),0 0 72px rgba(134,21,39,0.9),  0 10px 36px rgba(134,21,39,0.58); }
}

/* Glanz-Sweep, der diagonal über den Button läuft */
.btn-cta::after {
  content: '';
  position: absolute;
  top: 0; left: -75%;
  width: 50%; height: 100%;
  background: linear-gradient(120deg, transparent 0%, rgba(255,255,255,0.55) 50%, transparent 100%);
  transform: skewX(-20deg);
  animation: btn-shine 3s ease-in-out infinite;
  pointer-events: none;
}
@keyframes btn-shine {
  0%   { left: -75%; }
  35%  { left: 130%; }
  100% { left: 130%; }
}
```

Für den "floating CTA" (fixer Button unten rechts, erscheint nach dem Scrollen über die Hero-Section hinaus) und den Formular-Submit-Button dieselbe `background`, denselben Puls (`pulse-cta`/`pulse-btn`, minimal unterschiedliche Intensität) und denselben `::after`-Sweep wiederverwenden – siehe `geburtstag/index.html` Zeilen ~163–330 für die 1:1-Kopiervorlage.

**Wichtig:** Jedes Element mit `::after`-Sweep braucht `position: relative` (oder `fixed`) UND `overflow: hidden`, sonst läuft der Glanzstreifen über den Button hinaus.

---

## 6. Popup/Modal-Pattern statt Inline-Formular

Formulare (z. B. Newsletter-Opt-in) sitzen NICHT direkt in der Hero-Section, sondern in einem Klick-Popup. Jeder CTA-Button trägt `data-open-popup` und öffnet dasselbe Modal.

```html
<button type="button" class="btn-cta" data-open-popup>Jetzt eintragen</button>

<div class="popup-overlay" id="vipPopup" role="dialog" aria-modal="true" aria-label="Anmeldung">
  <div class="popup-box">
    <button class="popup-close" id="popupClose" aria-label="Schließen">&times;</button>
    <div class="popup-kicker">Kicker-Text</div>
    <h2>Überschrift <em>Highlight</em></h2>
    <p class="popup-sub">Kurzer Support-Satz.</p>
    <!-- Formular hier -->
  </div>
</div>
```

```css
.popup-overlay {
  display: none; position: fixed; inset: 0;
  background: rgba(7,8,8,0.72);
  backdrop-filter: blur(4px);
  z-index: 1000;
  align-items: center; justify-content: center; padding: 24px;
}
.popup-overlay.is-visible { display: flex; }
.popup-box {
  background: var(--dark);
  border: 1px solid rgba(255,255,255,0.08);
  border-top: 3px solid var(--rose);
  border-radius: 8px;
  max-width: 480px; width: 100%;
  padding: 44px 40px 36px;
  animation: popup-in 0.3s ease forwards;
  max-height: 90vh; overflow-y: auto;
}
@keyframes popup-in {
  from { opacity: 0; transform: translateY(24px) scale(0.97); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}
```

```js
(function() {
  var popup = document.getElementById('vipPopup');
  var btnClose = document.getElementById('popupClose');
  function show() { popup.classList.add('is-visible'); }
  function hide() { popup.classList.remove('is-visible'); }
  btnClose.addEventListener('click', hide);
  popup.addEventListener('click', function(e) { if (e.target === popup) hide(); });
  document.addEventListener('keydown', function(e) { if (e.key === 'Escape') hide(); });
  document.querySelectorAll('[data-open-popup]').forEach(function(el) {
    el.addEventListener('click', function(e) { e.preventDefault(); show(); });
  });
})();
```

---

## 7. Seitenstruktur (Section-Reihenfolge)

Typischer Aufbau von oben nach unten:

1. **Top-Banner** – schmale volle-Breite-Leiste, Countdown, `#0d4b35`
2. **Hero** – zweispaltig (Text links ~55%, Bild rechts ~45%), Hintergrund `var(--teal-dark)`, Bild mit Rand-Abblendung ins Hintergrundgrün (siehe unten), CTA-Button
3. **Fließtext-Sektion** – schmale Spalte (`max-width: 740px`), warmgraue Absätze, mind. ein `.quote-block` als volle-Breite-Zwischenüberschrift
4. **"Für dich / nicht für dich"-Boxen** – zwei Karten nebeneinander (grün getönt = ja, rosé getönt = nein)
5. **Final-CTA** – dunkle Sektion, Portrait-Bild, Countdown, letzter Button
6. **Floating-CTA** – fixer Button, erscheint nach dem Scrollen aus der Hero-Section
7. **Footer** – schwarz, Logo + Rechtslinks

### Hero-Bild-Details

- Desktop: Bild rechts, `object-fit: cover`, `position: absolute; inset: 0;` (NICHT normal im Fluss, sonst beeinflusst das intrinsische Seitenverhältnis des Bildes die Grid-Zeilenhöhe)
- Rand-Abblendung links (in Richtung Text) per `::before` mit `mask-image`-Verlauf, gefüllt mit `var(--teal-dark)` – sorgt für nahtlosen Übergang Bild → Hintergrund
- **Mobile: Bild wandert NACH dem Text** (unter Headline/Subtitle/Button), nicht davor – kein `order: -1` verwenden
- `object-position` am Bild individuell justieren, je nach Bildausschnitt (z. B. `center 40%`), damit kein unnötiger Leerraum über dem Kopf entsteht

### Volle-Breite-Balken (z. B. Zwischenüberschriften)

Technik, um aus einem zentrierten `max-width`-Container auszubrechen:

```css
.quote-block {
  position: relative; left: 50%; right: 50%;
  width: 100vw; margin-left: -50vw; margin-right: -50vw;
  background: #1b5c50;
  text-align: center; padding: 32px 40px; margin-top: 32px; margin-bottom: 32px;
}
```

`body { overflow-x: hidden; }` muss gesetzt sein, sonst erzeugt der `100vw`-Trick horizontales Scrollen.

---

## 8. Responsive-Verhalten

Zwei Breakpoints:

- **Tablet `@media (max-width: 900px)`** – Hero wird einspaltig (Bild auf 45vh, Text volle Breite darunter), Footer stapelt sich
- **Mobile `@media (max-width: 600px)`** – Innenabstände reduziert, Hero-Bild auf `60vw` Höhe

Da Typografie auf nur zwei feste Größen (48px/18px) reduziert ist, gibt es **keine** Font-Size-Overrides in den Media Queries mehr – nur Padding/Spacing/Layout-Anpassungen. Wenn eine neue Seite doch eine dritte Größe braucht, konsequent durchziehen statt einzelne `!important`-Overrides pro Breakpoint zu streuen.

---

## 9. Countdown-Timer

Zwei synchron laufende Countdowns (Banner oben + Final-CTA unten), gleiches Zieldatum:

```js
const target = new Date('2026-08-03T21:59:00Z'); // Zieldatum in UTC!
function pad(n) { return String(n).padStart(2,'0'); }
function updateIds(tgt, idSets) {
  const diff = tgt - new Date();
  const d = diff > 0 ? Math.floor(diff/86400000) : 0;
  const h = diff > 0 ? Math.floor((diff%86400000)/3600000) : 0;
  const m = diff > 0 ? Math.floor((diff%3600000)/60000) : 0;
  const s = diff > 0 ? Math.floor((diff%60000)/1000) : 0;
  idSets.forEach(([dEl,hEl,mEl,sEl]) => {
    document.getElementById(dEl).textContent = pad(d);
    document.getElementById(hEl).textContent = pad(h);
    document.getElementById(mEl).textContent = pad(m);
    document.getElementById(sEl).textContent = pad(s);
  });
}
setInterval(() => updateIds(target, [['f-days','f-hours','f-minutes','f-seconds']]), 1000);
```

Deutsche Zeit (CEST = UTC+2) im Kopf behalten: Zieldatum immer als UTC-Zeit im String angeben (2 Stunden von der gewünschten deutschen Uhrzeit abziehen).

---

## 10. Formular-Integration (ActiveCampaign)

Formulare kommen von ActiveCampaign (`marina232.activehosted.com`). Beim Bau einer neuen Seite:

1. Falls die echte Formular-ID noch nicht vorliegt: Platzhalter-ID nutzen (z. B. `999`), Formular optisch fertig bauen, TODO-Kommentar direkt über dem `<form>`-Tag hinterlassen. NICHT raten oder eine fremde ID wiederverwenden.
2. Sobald der Nutzer den echten AC-Embed-Code liefert: NUR die eigentliche Formularlogik (Felder, hidden inputs inkl. `or`-Wert, das komplette Validierungs-Skript) 1:1 übernehmen – NICHT das mitgelieferte generische AC-CSS (weiße Box) verwenden, sondern das bestehende dunkle Popup-Theme (`#_form_XXX_`-Selektoren mit Marken-Styling) beibehalten und nur die ID austauschen.
3. Platzhalter-Texte (Feld-Placeholder, Button-Label) an den informellen Du-Ton der Seite anpassen, nicht die AC-Standardtexte übernehmen.
4. Absenden im Test **nicht** tatsächlich auslösen – das würde einen echten Test-Kontakt in die Kunden-Liste eintragen. Nur Struktur/Wiring per DOM-Inspektion verifizieren (Formular-ID, `action`-URL, hidden fields).

---

## 11. Checkliste für eine neue Landingpage

- [ ] Eine einzelne `index.html`-Datei, kein Build-Step, alles inline
- [ ] `:root`-Farbvariablen oben im `<style>`, keine Hex-Duplikate im restlichen CSS
- [ ] Nur Montserrat, nur zwei Textgrößen (48px Headlines / 18px Rest)
- [ ] Rosegold-Buchstaben-Verlauf nur auf `<em>` in Überschriften, Rest der Headline in Volltonfarbe
- [ ] Alle CTAs identisch: `#861627`, Puls-Glow, Glanz-Sweep, `data-open-popup`
- [ ] Ein zentrales Popup-Modal für das Formular, kein Inline-Formular im Hero
- [ ] Hero-Bild mobil NACH dem Text, nicht davor
- [ ] `body { overflow-x: hidden; }` wenn volle-Breite-Balken (`100vw`-Trick) verwendet werden
- [ ] Countdown-Zieldatum als UTC-String (CEST − 2h)
- [ ] Bilder aus `../webinar/Bilder/` wiederverwenden statt neue hochzuladen, wenn passend
- [ ] Vor Go-Live: echte ActiveCampaign-Formular-ID einsetzen, Platzhalter-Kommentare entfernen
