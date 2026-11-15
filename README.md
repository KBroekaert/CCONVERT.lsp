**Nederlands** · [Français](README.fr.md) · [Deutsch](README.de.md) · [English](README.en.md)

# cConvert in BricsCAD en AutoCAD

Zet tekeningen in **BricsCAD** en **AutoCAD** om tussen **Lambert 72**
(EPSG:31370) en **Lambert 2008** (EPSG:3812), met de
[cConvert API van het NGI](https://cconvert.geo.be/).

---

## Installatie

1. Download het bestand voor uw software:

   | Bestand | Voor |
   | --- | --- |
   | `cconvert_bricscad.des` | BricsCAD |
   | `cconvert_autocad.fas` | AutoCAD |

2. Laad het met `APPLOAD`. Wilt u het bij elke start laden, voeg het dan in
   hetzelfde venster toe aan de **Startup Suite**.

3. **Alleen AutoCAD:** AutoCAD laadt geen LISP uit mappen die niet vertrouwd
   zijn. Voeg de map toe via *Options → Files → Trusted Locations* (of de
   systeemvariabele `TRUSTEDPATHS`).

Na het laden verschijnt:

```
cconvert.lsp loaded L72-L2008 and L2008-L72
```

**Vereisten**

- Windows.
- Een internetverbinding: de tool gebruikt de webdiensten van het NGI (er wordt gewerkt aan een offline versie).

---

## Gebruik

Er zijn twee commando's:

| Commando | Richting |
| --- | --- |
| `L72-L2008` | Lambert 72 → Lambert 2008 |
| `L2008-L72` | Lambert 2008 → Lambert 72 |

---

## Hoogtebron

De transformatie heeft voor elk punt een hoogte nodig. Onder **Preferences**
kunt u de bron voor de hoogtes selecteren:

1. Point heights for 3D entities + DTM heights for 2D entities (slower, more accurate) — *standaard*
2. DTM heights for all entities (slower, more accurate, preserves topology exactly)
3. Point heights for 3D entities + project height (faster, accurate given the correct project height)
4. Project height (faster, accurate given the correct project height, preserves topology exactly)

**De oorspronkelijke hoogtes blijven altijd behouden.** De gekozen hoogte dient
alleen als invoer voor de berekening. Na de omzetting heeft elke entiteit
dezelfde Z als ervoor.

De keuze en de projecthoogte gelden voor de huidige sessie. Na het herladen van
het bestand staat de keuze weer op optie 1.

---

## Welke entiteiten worden omgezet?

`POINT` · `LINE` · `CIRCLE` · `ARC` · `ELLIPSE` · `LWPOLYLINE` ·
`POLYLINE` · `SPLINE` · `TEXT` · `MTEXT` · `ATTRIB` ·
`ATTDEF` · `INSERT` · `HATCH` · `DIMENSION` · `LEADER` · `MULTILEADER` ·
`SOLID` · `3DFACE` · `IMAGE` · `WIPEOUT` · `XLINE` · `RAY` ·
`PDFUNDERLAY` · `DWFUNDERLAY` · `DGNUNDERLAY`

Voor alle andere entiteitstypes wordt een fallback met coördinaatherkenning gehanteerd.

### Wat niet wordt omgezet

- Entiteiten op een vergrendelde laag
- Entiteiten buiten het geldige gebied
- 3D-solids, regio's, oppervlakken en meshes
- De inhoud van blokdefinities (enkel het insertion point wordt getransformeerd, let op met blocks op 0,0 met daarin coördinaten in Lambert!)

---

Voor vragen of opmerkingen kunt u contact opnemen met Klaas Broekaert
(klaas@lbda.be). Met dank aan Jeffrey Verbeurgt van het NGI om mee te denken en de
tool te verifiëren.

Noch de ontwikkelaar, noch het NGI kan aansprakelijk gesteld worden voor fouten
in de resultaten of voor schade die voortvloeit uit het gebruik van deze tool.
