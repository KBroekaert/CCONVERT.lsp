[Nederlands](README.md) · **Français** · [Deutsch](README.de.md) · [English](README.en.md)

# cConvert dans BricsCAD et AutoCAD

Convertit des dessins dans **BricsCAD** et **AutoCAD** entre **Lambert 72**
(EPSG:31370) et **Lambert 2008** (EPSG:3812), à l'aide de
l'[API cConvert de l'IGN](https://cconvert.geo.be/).

---

## Installation

1. Téléchargez le fichier correspondant à votre logiciel :

   | Fichier | Pour |
   | --- | --- |
   | `cconvert_bricscad.des` | BricsCAD |
   | `cconvert_autocad.fas` | AutoCAD |

2. Chargez-le avec `APPLOAD`. Pour le charger à chaque démarrage, ajoutez-le à
   la **Startup Suite** dans la même fenêtre.

3. **AutoCAD uniquement :** AutoCAD ne charge pas de LISP depuis des dossiers
   non approuvés. Ajoutez le dossier via *Options → Files → Trusted Locations*
   (ou la variable système `TRUSTEDPATHS`).

Après le chargement, le message suivant s'affiche :

```
cconvert.lsp loaded L72-L2008 and L2008-L72
```

**Prérequis**

- Windows.
- Une connexion Internet : l'outil utilise les services web de l'IGN (une version hors ligne est en préparation).

---

## Utilisation

Il y a deux commandes :

| Commande | Sens |
| --- | --- |
| `L72-L2008` | Lambert 72 → Lambert 2008 |
| `L2008-L72` | Lambert 2008 → Lambert 72 |

---

## Source des hauteurs

La transformation a besoin d'une hauteur pour chaque point. Sous
**Preferences**, vous pouvez sélectionner la source des hauteurs :

1. Point heights for 3D entities + DTM heights for 2D entities (slower, more accurate) — *par défaut*
2. DTM heights for all entities (slower, more accurate, preserves topology exactly)
3. Point heights for 3D entities + project height (faster, accurate given the correct project height)
4. Project height (faster, accurate given the correct project height, preserves topology exactly)

**Les hauteurs d'origine sont toujours conservées.** La hauteur choisie sert
uniquement de donnée d'entrée pour le calcul. Après la conversion, chaque entité
a le même Z qu'auparavant.

Le choix et la hauteur de projet valent pour la session en cours. Après un
rechargement du fichier, le choix revient à l'option 1.

---

## Quelles entités sont converties ?

`POINT` · `LINE` · `CIRCLE` · `ARC` · `ELLIPSE` · `LWPOLYLINE` ·
`POLYLINE` · `SPLINE` · `TEXT` · `MTEXT` · `ATTRIB` ·
`ATTDEF` · `INSERT` · `HATCH` · `DIMENSION` · `LEADER` · `MULTILEADER` ·
`SOLID` · `3DFACE` · `IMAGE` · `WIPEOUT` · `XLINE` · `RAY` ·
`PDFUNDERLAY` · `DWFUNDERLAY` · `DGNUNDERLAY`

Pour tous les autres types d'entités, une méthode de repli avec détection des coordonnées est utilisée.

### Ce qui n'est pas converti

- Les entités sur un calque verrouillé
- Les entités en dehors de la zone de validité
- Les solides 3D, régions, surfaces et maillages
- Le contenu des définitions de blocs (seul le point d'insertion est transformé ; attention aux blocs insérés en 0,0 qui contiennent des coordonnées en Lambert !)

---

Pour toute question ou remarque, vous pouvez contacter Klaas Broekaert
(klaas@lbda.be). Merci à Jeffrey Verbeurgt de l'IGN pour ses idées et pour la
vérification de l'outil.

Ni le développeur ni l'IGN ne peuvent être tenus responsables des erreurs dans
les résultats ou des dommages résultant de l'utilisation de cet outil.
