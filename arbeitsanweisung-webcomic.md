# Webcomic „Im System" – Arbeitsanweisung für Claude Code

**Ziel:** 20 Comic-Panel-Bilder als Infinite-Scroll-Webcomic veröffentlichen.  
**Werkzeug:** Claude Code im Terminal  
**Voraussetzung:** Claude Code installiert (`npm install -g @anthropic-ai/claude-code`)

---

## Schritt 1 – Projektordner vorbereiten

Lege folgende Ordnerstruktur manuell an (oder lass Claude Code sie anlegen):

```
webcomic/
├── panels/          ← hier kommen deine Panel-Bilder rein
├── index.html       ← wird von Claude Code erstellt
└── style.css        ← wird von Claude Code erstellt
```

Benenne deine Panel-Bilder einheitlich:

```
panel-01.jpg
panel-02.jpg
panel-03.jpg
...
panel-20.jpg
```

> **Tipp:** Falls deine Panels noch aus dem Gesamtbild ausgeschnitten werden müssen,  
> sage Claude Code: *„Schneide das Bild `comic.jpg` in 20 gleich große Panels (4 Spalten × 5 Reihen) und speichere sie als panel-01.jpg bis panel-20.jpg im Ordner `panels/`."*

---

## Schritt 2 – Claude Code starten

Öffne dein Terminal, navigiere in den Projektordner und starte Claude Code:

```bash
cd webcomic
claude
```

---

## Schritt 3 – Prompt für die HTML-Grundstruktur

Gib Claude Code folgenden Prompt (kopieren und einfügen):

```
Erstelle eine index.html und eine style.css für einen Webcomic mit Infinite-Scroll-Layout.

Anforderungen:
- Titel der Seite: „Im System – Alltag in der Sozialen Arbeit"
- 20 Panel-Bilder im Ordner /panels/, benannt panel-01.jpg bis panel-20.jpg
- Layout: Infinite Scroll, alle Panels untereinander
- Standard-Layout: 2 Panels nebeneinander (CSS Grid, 2 Spalten)
- Sonderpanels über volle Breite (1 Spalte, span 2):
    - panel-04.jpg (dramatische Explosion)
    - panel-16.jpg (FUCK THE SYSTEM – großes Panel)
    - panel-20.jpg (Abschluss mit Herz)
- Mobiloptimierung: unter 600px Breite alle Panels einspaltig
- Schwarzer Hintergrund (#111111), panels haben 4px Abstand
- Jedes <img> hat ein sinnvolles alt-Attribut (kurze Bildbeschreibung)
- Beim Scrollen: panels faden sanft ein (IntersectionObserver + CSS transition)
- Kein JavaScript-Framework, nur vanilla HTML/CSS/JS
- Comic-Titel als Header über den Panels
- Kleines Impressum am Ende: „Eine Geschichte aus der Sozialen Arbeit. Alle Personen fiktiv."
```

---

## Schritt 4 – Sonderpanel-Texte anpassen

Nachdem Claude Code die Dateien erstellt hat, bitte es um folgende Anpassungen:

```
Passe die alt-Attribute der Bilder an mit diesen konkreten Beschreibungen:

panel-01: „Ich saß im Zug, das Gesicht in der Sonne…"
panel-02: „Kürzungen. Bei Kindern. Bei Jugendlichen. Bei Menschen mit Behinderungen."
panel-03: „Für jede Hilfe ein Antrag. Für jede Leistung ein neuer Antrag."
panel-04: „Akten explodieren – das System kollabiert"
panel-05: „Ich versuchte, den Überblick zu behalten…"
panel-06: „Diese ausufernde Bürokratie geht immer zulasten der Klient*innen."
panel-07: „Und irgendwann wurde mir klar: Wir sind alle Klient*innen."
panel-08: „Ich fragte mich, warum das alles so kompliziert ist."
panel-09: „Ach so. Gibt's nicht."
panel-10: „Das Leben ist nicht fair. Und das System gleicht es nicht aus."
panel-11: „Nicht alle haben viel Geld. Aber alle verdienen die Chance auf Bildung."
panel-12: „Vor meinem inneren Auge sah ich Kinder, die nicht mehr in die Schule gehen wollen."
panel-13: „Dann musste ich an die Pandemie denken."
panel-14: „Kinder überfordert. Eltern überfordert."
panel-15: „Und ich saß da und dachte nur:"
panel-16: „FUCK THE SYSTEM."
panel-17: „Stille. Blick aus dem Zugfenster."
panel-18: „Sonnenuntergang über einem See."
panel-19: „Zwei Kinder auf einem Bahnsteig winken dem Zug hinterher. Einfach so. Ohne Grund."
panel-20: „Und ich merkte, dass trotz all des Chaos draußen immer noch kleine Dinge passieren, die sich nicht kaputtregeln lassen."
```

---

## Schritt 5 – Scroll-Animation verfeinern

```
Füge eine Scroll-Animation hinzu:
- Panels starten mit opacity: 0 und transform: translateY(30px)
- Wenn ein Panel in den Viewport scrollt (IntersectionObserver, threshold: 0.15),
  bekommt es die Klasse .visible
- .visible hat: opacity: 1, transform: translateY(0), transition: 0.6s ease
- Panel 16 (FUCK THE SYSTEM) bekommt zusätzlich beim Einblenden
  eine kurze Shake-Animation (3x leichtes Zittern, 0.4s)
```

---

## Schritt 6 – Testen im Browser

```
Öffne index.html im Browser und prüfe:
1. Erscheinen alle 20 Panels?
2. Sind Panel 4, 16 und 20 über volle Breite?
3. Funktioniert die Fade-in-Animation beim Scrollen?
4. Sieht es auf 375px Breite (Mobilansicht) korrekt aus?

Falls Bilder fehlen: Erstelle Platzhalter-Panels (graue Rechtecke mit
Pannelnummer) damit das Layout sichtbar wird.
```

---

## Schritt 7 – Optional: Panels aus Gesamtbild ausschneiden

Falls du noch kein Einzelbilder hast und nur das Gesamtbild (`comic.jpg`):

```
Das Bild comic.jpg enthält 20 Comic-Panels in einem 4-Spalten × 5-Reihen Raster.
Schneide alle 20 Panels aus und speichere sie als panel-01.jpg bis panel-20.jpg
im Ordner panels/.
Reihenfolge: Zeile 1 links nach rechts = panel-01 bis panel-04,
Zeile 2 = panel-05 bis panel-08, usw.
Nutze dafür Python mit der Pillow-Bibliothek.
```

---

## Schritt 8 – Veröffentlichen

### Option A: Netlify Drop (einfachste Methode, kostenlos)
1. Gehe zu [netlify.com/drop](https://netlify.com/drop)
2. Ziehe den gesamten `webcomic/`-Ordner ins Browser-Fenster
3. Fertig – du bekommst sofort eine URL

### Option B: GitHub Pages (kostenlos, versioniert)

```
Initialisiere ein Git-Repository im webcomic-Ordner,
erstelle eine .gitignore die node_modules ausschließt,
und zeige mir die Befehle um es auf GitHub Pages zu veröffentlichen.
```

### Option C: Lokale HTML-Datei
- Einfach `index.html` per Doppelklick im Browser öffnen
- Funktioniert ohne Internet, solange Bilder im `panels/`-Ordner liegen

---

## Übersicht: Welche Panels sind Sonderpanels?

| Panel | Inhalt | Layout |
|-------|--------|--------|
| panel-04 | Akten-Explosion | volle Breite |
| panel-16 | FUCK THE SYSTEM | volle Breite + Shake-Animation |
| panel-20 | Abschluss mit Herz | volle Breite |
| alle anderen | normal | 2-spaltig |

---

## Checkliste vor Veröffentlichung

- [ ] Alle 20 Panel-Bilder im Ordner `panels/` vorhanden
- [ ] Dateien heißen exakt `panel-01.jpg` bis `panel-20.jpg`
- [ ] Seite im Browser getestet (Desktop)
- [ ] Seite im Browser getestet (Mobilansicht, 375px)
- [ ] Alle Panels laden korrekt
- [ ] Scroll-Animation funktioniert
- [ ] Panel 4, 16, 20 sind über volle Breite
- [ ] alt-Attribute gesetzt (Barrierefreiheit)

---

## Häufige Probleme & Lösungen

**Bilder werden nicht angezeigt**
```
Prüfe ob die Bilddateien exakt panel-01.jpg heißen (nicht Panel-01.jpg oder panel-1.jpg).
Dateipfade in HTML und Ordnernamen sind case-sensitive.
```

**Layout bricht auf Mobil**
```
Füge in style.css hinzu:
@media (max-width: 600px) {
  .panel { grid-column: span 2; }
}
```

**Animation funktioniert nicht**
```
Öffne die Browser-Konsole (F12) und prüfe auf JavaScript-Fehler.
IntersectionObserver wird von allen modernen Browsern unterstützt.
```

---

*Erstellt für das Webcomic-Projekt „Im System – Alltag in der Sozialen Arbeit"*
