[Nederlands](README.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · **English**

# cConvert in BricsCAD and AutoCAD

Converts drawings in **BricsCAD** and **AutoCAD** between **Lambert 72**
(EPSG:31370) and **Lambert 2008** (EPSG:3812), using the
[NGI's cConvert API](https://cconvert.geo.be/).

---

## Installation

1. Download the file for your software:

   | File | For |
   | --- | --- |
   | `cconvert_bricscad.des` | BricsCAD |
   | `cconvert_autocad.fas` | AutoCAD |

2. Load it with `APPLOAD`. To load it at every startup, add it to the
   **Startup Suite** in the same dialog.

3. **AutoCAD only:** AutoCAD does not load LISP from untrusted folders. Add the
   folder under *Options → Files → Trusted Locations* (or the `TRUSTEDPATHS`
   system variable).

After loading, you will see:

```
cconvert.lsp loaded L72-L2008 and L2008-L72
```

**Requirements**

- Windows.
- An internet connection: the tool uses the NGI's web services (an offline version is in development).

---

## Usage

There are two commands:

| Command | Direction |
| --- | --- |
| `L72-L2008` | Lambert 72 → Lambert 2008 |
| `L2008-L72` | Lambert 2008 → Lambert 72 |

---

## Height source

The transformation needs a height for every point. Under **Preferences**, you
can select the source of the heights:

1. Point heights for 3D entities + DTM heights for 2D entities (slower, more accurate) — *default*
2. DTM heights for all entities (slower, more accurate, preserves topology exactly)
3. Point heights for 3D entities + project height (faster, accurate given the correct project height)
4. Project height (faster, accurate given the correct project height, preserves topology exactly)

**Original heights are always preserved.** The selected height is used only as
input for the calculation. After conversion, every entity has the same Z as
before.

The choice and the project height apply to the current session. After reloading
the file, the choice reverts to option 1.

---

## Which entities are converted?

`POINT` · `LINE` · `CIRCLE` · `ARC` · `ELLIPSE` · `LWPOLYLINE` ·
`POLYLINE` · `SPLINE` · `TEXT` · `MTEXT` · `ATTRIB` ·
`ATTDEF` · `INSERT` · `HATCH` · `DIMENSION` · `LEADER` · `MULTILEADER` ·
`SOLID` · `3DFACE` · `IMAGE` · `WIPEOUT` · `XLINE` · `RAY` ·
`PDFUNDERLAY` · `DWFUNDERLAY` · `DGNUNDERLAY`

For all other entity types, a fallback with coordinate detection is used.

### What is not converted

- Entities on a locked layer
- Entities outside the valid area
- 3D solids, regions, surfaces and meshes
- The contents of block definitions (only the insertion point is transformed; beware of blocks inserted at 0,0 that contain coordinates in Lambert!)

---

For questions or comments, please contact Klaas Broekaert (klaas@lbda.be).
Thanks to Jeffrey Verbeurgt of the NGI for his input and for verifying the tool.

Neither the developer nor the NGI can be held liable for errors in the results
or for damage resulting from the use of this tool.
