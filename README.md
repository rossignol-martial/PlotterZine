# PlotterZine

**Outil de mise en page fanzine pour penplotter — application web standalone, zéro installation.**

PlotterZine est un fichier HTML unique qui tourne entièrement dans le navigateur. Il permet de composer des fanzines à partir de fichiers SVG vectoriels, d'ajuster le cadrage de chaque page, et d'exporter une imposition prête à tracer au penplotter.

---

## Démo rapide

Télécharger [plotterZine.html]((https://rossignol-martial.github.io/outil-trames/plotterZine.html) et l'ouvrir dans un navigateur — aucune connexion, aucun serveur requis.

---

## Formats d'imposition

| Mode | Papier | Pages | Coupe | Résultat |
|------|--------|-------|-------|----------|
| **A3 — 8p A6** | A3 portrait | 8 × A6 paysage | 1 fente verticale | Cahier 8p paysage |
| **A3 — 8p Coupe T** | A3 paysage | 8 × A6 portrait | 2 coupes en T | Cahier 8p portrait |
| **A3 — 8p Coupe L** | A3 paysage | 8 × A6 portrait + verso 16p | 1 coupe H partielle | Accordéon / livret 16p |
| **A3 — 4p A4** | A3 paysage | 4 × A4 portrait recto/verso | Aucune | Livret A4, 8 pages |
| **A3 — Leporello** | A3 paysage | 4 panneaux 105×297mm | Aucune | Accordéon 4 panneaux |

---

## Fonctionnalités

### Composition
- Bibliothèque de pages SVG — import multiple, drag & drop, vignettes avec indicateur de placement
- Cadrage interactif — zoom molette, pan clic-glissé, sliders ±, rotations 90°
- Aperçu temps réel avec repères : zones, lignes de pli, coupes, marges 5mm, n° pages, repères de coupe

### Options avancées — Mode A3 4p A4
- Subdivision de chaque page en grille : 1×1 à 3×3, horizontal ou vertical
- Fusion panoramique : p4+p1 (recto) ou p2+p3 (verso) en grand espace A3

### Options avancées — Leporello
- Scinder chaque panneau en 2 SVG indépendants (haut/bas)
- Fusionner les panneaux 2+3 en espace panoramique 210×297mm

### Options avancées — Coupe L
- Recto (p1–p8) + Verso (p9–p16)
- Zones 12 et 13 verrouillées (collées, hachures grises)
- Export automatique recto + verso en un clic

### Export SVG
- 2 calques Inkscape : **Contenu** (SVG vectoriels) + **Repères techniques** (plis, coupes, marges, n° pages, croix de coupe)
- Fichiers en mm, 1 unité SVG = 1 mm
- Export portrait automatique pour A4, Leporello, Coupe L

---

## Impositions détaillées

### A3 — 8p A6 (fente centrale)
```
A3 portrait 297×420mm — 2 colonnes × 4 rangées
┌──────────┬──────────┐
│  p8  ↕   │  p7  ↕   │
├──────────┼──────────┤
│  p1  ↕   │  p6  ↕   │
│          ┆          │  ← fente verticale
├──────────┼──────────┤
│    p2    │    p5    │
├──────────┼──────────┤
│    p3    │    p4    │
└──────────┴──────────┘
```

### A3 — 8p Coupe T
```
A3 paysage 420×297mm — 4 colonnes × 2 rangées
┌─────┬─────╤─────┬─────┐
│  2  │  1  │  8  │  7  │  haut (tête en haut)
├─────┼─────┘─────┼─────┤  ← coupe H partielle
│  3↕ │  4↕ │  5↕ │  6↕ │  bas (tête en bas)
└─────┴──↑──┴─────┴─────┘
         coupe V partielle
```

### A3 — 8p Coupe L
```
A3 paysage 420×297mm — 4 colonnes × 2 rangées
┌─────┬─────┬─────┬─────┐
│  8  │  7  │  6  │  5  │  haut (tête en haut)
┝━━━━━┿━━━━━┿━━━━━┛     │  ← coupe H partielle
│  1↕ │  2↕ │  3↕ │  4↕ │  bas (tête en bas)
└─────┴─────┴─────┴─────┘
Verso (p9–p16) : zones 12 et 13 verrouillées (collées)
```

### A3 — 4p A4 recto/verso
```
RECTO                    VERSO
┌──────────┬──────────┐  ┌──────────┬──────────┐
│    p4    │    p1    │  │    p2    │    p3    │
└──────────┴──────────┘  └──────────┴──────────┘
```

### A3 — Leporello
```
┌─────────┬─────────┬─────────┬─────────┐
│    1    │    2    │    3    │    4    │
└─────────┴─────────┴─────────┴─────────┘
  105mm     105mm     105mm     105mm = 420mm
```

---

## Repères visuels

| Repère | Couleur | Signification |
|--------|---------|---------------|
| Zones | Vert clair | Cases tête en haut |
| Zones | Bleu clair | Cases tête en bas |
| Zones | Hachures grises | Zone collée / non imprimable |
| Lignes de pli | Tirets rouges | Axes de pliage |
| Coupes | Bleu plein | Lignes de coupe |

---

## Fichiers exportés

| Mode | Fichier(s) |
|------|------------|
| A3 — 8p A6 | `fanzine_A6_8p_A3.svg` |
| A3 — 8p Coupe T | `fanzine_coupT_A3.svg` |
| A3 — 8p Coupe L | `fanzine_coupL_recto.svg` + `fanzine_coupL_verso.svg` |
| A3 — 4p A4 | `fanzine_A4_recto.svg` + `fanzine_A4_verso.svg` |
| A3 — Leporello | `leporello_A3.svg` |

---

## Workflow plotter

```
PlotterZine (export SVG)
  └─ Inkscape
      ├─ Calque "Repères techniques" → tracer en premier (stylo 0.1mm)
      └─ Calque "Contenu"           → tracer le fanzine
```

Compatible AxiDraw (extension Inkscape officielle), tout plotter GRBL/EBB.

---

## Raccourcis

| Action | Geste |
|--------|-------|
| Sélectionner une page | Clic sur la vignette |
| Placer une page | Clic sur une case du canvas |
| Zoom image | Molette sur l'image |
| Déplacer image | Clic-glissé sur l'image |
| Import rapide | Drag & drop fichier(s) SVG |
| Plein écran | Bouton ⛶ |

---

## Préparer les SVG source

- Définir un `viewBox` sur chaque fichier SVG (obligatoire)
- Prévoir une marge interne de 3–4mm dans les SVG source
- Travailler en **traits purs** (stroke, pas de fill) pour le plotter
- Nettoyer avec *Inkscape > Fichier > Nettoyer le document* avant import

---

## Structure du dépôt

```
plotterZine/
├── plotterZine.html             # Application complète (~300KB, fichier unique)
├── README.md                    # Ce fichier
└── PlotterZine_Manuel_v2.docx   # Manuel utilisateur illustré (11 captures + 5 schémas)
```

---

## Compatibilité navigateurs

| Navigateur | Support |
|------------|---------|
| Chrome / Chromium | ✅ |
| Firefox | ✅ |
| Edge | ✅ |
| Safari | ✅ |

---

## Licence

**CC BY-NC 4.0** — Martial Rossignol

Usage personnel et non commercial libre. Attribution requise.  
[creativecommons.org/licenses/by-nc/4.0](https://creativecommons.org/licenses/by-nc/4.0/)

---

## Contribuer

Issues et pull requests bienvenues pour :
- Nouveaux formats d'imposition (cahier agrafé, dos carré collé…)
- Compatibilité d'autres formats papier
- Améliorations de l'interface
- Corrections de bugs

---

*Fait avec ☕ et de l'encre — pour ceux qui font encore des trucs en vrai.*
