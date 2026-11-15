[Nederlands](README.md) · [Français](README.fr.md) · **Deutsch** · [English](README.en.md)

# cConvert in BricsCAD und AutoCAD

Rechnet Zeichnungen in **BricsCAD** und **AutoCAD** zwischen **Lambert 72**
(EPSG:31370) und **Lambert 2008** (EPSG:3812) um, mit der
[cConvert-API des NGI](https://cconvert.geo.be/).

---

## Installation

1. Laden Sie die Datei für Ihre Software herunter:

   | Datei | Für |
   | --- | --- |
   | `cconvert_bricscad.des` | BricsCAD |
   | `cconvert_autocad.fas` | AutoCAD |

2. Laden Sie sie mit `APPLOAD`. Soll sie bei jedem Start geladen werden, fügen
   Sie sie im selben Fenster zur **Startup Suite** hinzu.

3. **Nur AutoCAD:** AutoCAD lädt kein LISP aus nicht vertrauenswürdigen
   Ordnern. Fügen Sie den Ordner über *Options → Files → Trusted Locations*
   hinzu (oder über die Systemvariable `TRUSTEDPATHS`).

Nach dem Laden erscheint:

```
cconvert.lsp loaded L72-L2008 and L2008-L72
```

**Voraussetzungen**

- Windows.
- Eine Internetverbindung: Das Tool nutzt die Webdienste des NGI (an einer Offline-Version wird gearbeitet).

---

## Verwendung

Es gibt zwei Befehle:

| Befehl | Richtung |
| --- | --- |
| `L72-L2008` | Lambert 72 → Lambert 2008 |
| `L2008-L72` | Lambert 2008 → Lambert 72 |

---

## Höhenquelle

Die Transformation benötigt für jeden Punkt eine Höhe. Unter **Preferences**
können Sie die Quelle der Höhen auswählen:

1. Point heights for 3D entities + DTM heights for 2D entities (slower, more accurate) — *Standard*
2. DTM heights for all entities (slower, more accurate, preserves topology exactly)
3. Point heights for 3D entities + project height (faster, accurate given the correct project height)
4. Project height (faster, accurate given the correct project height, preserves topology exactly)

**Die ursprünglichen Höhen bleiben immer erhalten.** Die gewählte Höhe dient nur
als Eingabe für die Berechnung. Nach der Umrechnung hat jedes Objekt dasselbe Z
wie zuvor.

Die Auswahl und die Projekthöhe gelten für die aktuelle Sitzung. Nach dem
erneuten Laden der Datei steht die Auswahl wieder auf Option 1.

---

## Welche Objekte werden umgerechnet?

`POINT` · `LINE` · `CIRCLE` · `ARC` · `ELLIPSE` · `LWPOLYLINE` ·
`POLYLINE` · `SPLINE` · `TEXT` · `MTEXT` · `ATTRIB` ·
`ATTDEF` · `INSERT` · `HATCH` · `DIMENSION` · `LEADER` · `MULTILEADER` ·
`SOLID` · `3DFACE` · `IMAGE` · `WIPEOUT` · `XLINE` · `RAY` ·
`PDFUNDERLAY` · `DWFUNDERLAY` · `DGNUNDERLAY`

Für alle anderen Objekttypen wird ein Fallback mit Koordinatenerkennung verwendet.

### Was nicht umgerechnet wird

- Objekte auf einem gesperrten Layer
- Objekte außerhalb des gültigen Bereichs
- 3D-Volumenkörper, Regionen, Flächen und Netze
- Der Inhalt von Blockdefinitionen (nur der Einfügepunkt wird transformiert; Vorsicht bei Blöcken, die bei 0,0 eingefügt sind und Koordinaten in Lambert enthalten!)

---

Für Fragen oder Anmerkungen wenden Sie sich bitte an Klaas Broekaert
(klaas@lbda.be). Vielen Dank an Jeffrey Verbeurgt vom NGI für das Mitdenken und
die Überprüfung des Tools.

Weder der Entwickler noch das NGI können für Fehler in den Ergebnissen oder für
Schäden, die aus der Nutzung dieses Tools entstehen, haftbar gemacht werden.
