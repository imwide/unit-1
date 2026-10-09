# flowzz – Überarbeitung der Startseite

Ergebnis: [index_modernisiert.html](./index_modernisiert.html)
Basis war die unveränderte [index.html](./index.html). Alle anderen Dateien sind unangetastet.

## Warum nicht die bisherige Überarbeitung?

Die andere HTML-Datei (`flowzz - Der Nr. 1 Preisvergleich_ …html`) hat die Seite eher verschlechtert:

- Die beiden Partner-Banner (Green Joy / Oya) werden nur noch als graue Flächen ohne Bild angezeigt.
- Es gibt leere „Anzeige"-Leisten ohne Inhalt, die wie kaputte Elemente wirken.
- Zwischen Text und Buttons stehen lose Texte wie „Autor, Datum & Quellen" und „Hinweis: …", die doppelt vorkommen.
- Die Navigation hat Gruppenlabels („Produkte", „Wissen", „Service"). Sie sind klein, farbig abgesetzt und sehen aus wie Links.
- Die Bilder in den Ratgeber-Blöcken fehlten weiterhin (siehe unten).

Das war vor allem CSS, das nur auf Barrierefreiheit-Kennzahlen (Mindestgröße, Kontrast) optimiert war, aber nicht auf das Gesamtbild.

## Die 5 überarbeiteten Bereiche

### 1. Header / Navigation
**Problem:** Zwei Zeilen (Logo + Suche, darunter 9 gleich gewichtete Links), der Warenkorb mit der „0" hing einsam rechts, das Konto-Icon war nicht zu sehen. Dazu waren Suche und Icons für die Mobil-/Desktop-Varianten mehrfach im Code. Der Header war `fixed` mit einem 108-px-Platzhalter, der leeren Raum erzeugte.
**Lösung:** Eine Zeile mit Logo, 6 Hauptlinks, „Mehr"-Menü (Top Ten, Shop, Kontakt), kompakter Suche und Icons. Er ist `sticky`. Mobil gibt es ein Burger-Menü ohne JavaScript-Abhängigkeit (`<details>`).

### 2. Top-Produkte-Karussell
**Problem:** Die Pfeile erschienen doppelt (oben und unten), waren winzige Blatt-Symbole und standen direkt unter einem unauffälligen Titel. Die 13 Produkte waren intern verdoppelt (26 Karten), und die Pfeile steuerten ein Transform-Skript, das mit dem Scrollen kollidierte.
**Lösung:** Nativer Scroll-Container mit Snap-Punkten, eine Pfeil-Gruppe rechts neben dem größeren Titel, Chevron-Icons, Duplikate ausgeblendet, Hover-Effekt auf den Karten.

### 3. Kategorie-Tabs + „THC Blüten ab 2,95 €"-Teaser
**Problem:** Fünf Tabs, aber nur der Inhalt des ersten existiert. Ein Klick auf einen anderen Tab ließ den Bereich komplett leer werden. Die Tab-Beschriftungen waren zweizeilig und zu groß, die mittlere Teaser-Karte war durch das Swiper-Skalieren größer als die anderen, und zwei Buttons sahen nach Zufall unterschiedlich aus.
**Lösung:** Die Tabs sind jetzt ehrliche Schnellzugriff-Links. Die Teaser-Karten sind gleich groß, haben einheitliche Buttons, einen klaren Primär-/Sekundär-Button links und sind horizontal scrollbar.

### 4. Partner-Banner (Anzeigen)
**Problem:** Der „Mehr erfahren"-Button lag auf den Bildtexten („IS ALWAYS GREENER") und überdeckte sie. Die Banner waren als Werbung nicht gekennzeichnet. Von 6 Bannern waren nur 2 sichtbar, die übrigen nur über einen Transform-Slider erreichbar.
**Lösung:** Einheitliche abgerundete Karten mit Label „Anzeige", Button in der freien Ecke (mobil oben rechts) und alle 6 Banner per Pfeil oder Wischen erreichbar.

### 5. Ratgeber-Bereich („Wie erkenne ich…", „Cannabis auf Rezept…", „Preise vergleichen")
**Problem:** In beiden Textblöcken war die **Bildhälfte leer** (Bildcontainer hatte Höhe 0, weil das Seitenverhältnis fehlte). Dadurch standen Text und Leerfläche untereinander, grau auf grau und ohne Abstand. Die Links („weiterlesen") waren nur unterstrichener Text, und der Preisvergleich-Hinweis ging als Fließtext unter.
**Lösung:** Zwei Karten mit Bild und Text im Wechsel, echte Buttons statt Textlinks, und der Preisvergleich-Hinweis als farbiger Call-to-Action-Block in Markenfarbe.

## Technische Fixes (keine Neugestaltung)

- Der Favoriten-Drawer wurde ohne Skript am Seitenende gerendert (≈330 px leere Fläche unter dem Footer, mobil auch seitliches Scrollen). Er ist jetzt ausgeblendet.
- Leere Werbeplätze (`section-revive-ad`) sind ausgeblendet.
- Das alte Inline-Skript (Transform-Slider, kaputte Tabs) wurde durch ein kleines Skript für Pfeile und Menüs ersetzt.

## Geprüft

Die Prüfung lief mit headless Chrome bei 1440, 1024, 900, 768 und 390 px Breite:

- keine defekten Bilder, keine fehlgeschlagenen Requests, keine JS-Fehler
- Schrift (Inter) wird geladen, kein horizontales Scrollen
- Pfeile, „Mehr"-Menü und Burger-Menü funktionieren

## Bewusst nicht angefasst (Limit von 5 Bereichen)

Der lange SEO-Textblock am Seitenende („Willkommen bei flowzz…") ist weiterhin eine Textwüste. Er wäre der nächste Kandidat, z. B. als aufklappbarer Bereich. Auch die „Medizinische Cannabisblüten"-Karten und der Footer sind unverändert.

## Nachtrag: Top-Produkte-Karten (2. Iteration)

Der Bereich „Top Produkte" ganz oben wirkte weiterhin wie ein Werbebanner-Raster. Das habe ich als Fortsetzung von Bereich 2 überarbeitet.

**Problem (warum es überladen wirkte):**
- Jede Karte zeigte 10 Informationen gleichzeitig: Typ-Chip, „Neu"-Badge, Herz, Name, Sortenname, Sternebewertung samt Anzahl, „Ansehen" mit Pfeil, THC/CBD, Preis, „lieferbar" und einen Button. Dazu kommen Bilder, die schon selbst laut gestaltet sind (Markenlogos, Slogans, THC-Werte) und randlos, voll gesättigt und bündig nebeneinanderstehen. Das ergibt die dichte Optik von Google-Display-Anzeigen.
- Alle Karten hatten gleich viel visuelles Gewicht, ein Vergleich über den Preis war schwer.
- „Ansehen" und der Button waren doppelt, weil die ganze Karte ohnehin ein Link ist.
- Ein Chip mit nur „-" zeigte bei Produkten ohne Typ einen leeren Platzhalter.

**Lösung (Progressive Disclosure):**
- **Ruhezustand:** nur Bild, „Neu"-Badge, Herz, Name (max. 2 Zeilen) und Preis. Der Preis ist grün hervorgehoben, „ab" und „/ 1 g" sind klein und grau.
- **Bild als Kachel:** 8 px Innenabstand und abgerundete Ecken, die Karte hat nur noch einen feinen Rand ohne Schatten. Das Bild wirkt dadurch wie ein Produktfoto in einer Karte statt wie ein Banner.
- **Hover und Tastaturfokus** (`:hover` und `:focus-within`): Ein weißes Info-Panel wächst vom unteren Kartenrand nach oben über das Bild. Es zeigt Typ-Chip, Sortenname, Bewertung, THC/CBD, Verfügbarkeit und den Button „Rezeptwunsch". Die Kartenhöhe bleibt fix, deshalb verschiebt sich nichts im Layout.
- **Touch-Geräte** (kein Hover): Ohne Hover wären die Infos nie erreichbar. Dort bleiben Name, THC/CBD, Preis und „lieferbar" dauerhaft sichtbar, Bewertung und Button entfallen (die Karte führt per Tipp zur Produktseite).
- Leere „-"-Chips werden ausgeblendet, „Ansehen" und der Pfeil entfallen.

**Bewusst offen:** Die Produktbilder selbst sind Werbegrafiken der Hersteller und lassen sich ohne neue Bilder nicht beruhigen. Die Kachel-Optik mildert das nur.

**Geprüft:** Hover und Tab-Fokus zeigen das Panel und blenden es wieder aus, die Pfeile scrollen weiter, es gibt keine JS-Fehler und kein horizontales Scrollen (Desktop 1440 px und Touch 390 px).
