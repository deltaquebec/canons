# Canons: Classical Page Layout for LaTeX

**Deterministic, historically-grounded page layouts with margin control**

The **canons** package family implements classical and classical-inspired page construction canons as explicit mathematical rules, providing reproducible layouts based on historical book design. Whether you need Van de Graaf's medieval proportions, Tufte's asymmetric margins, or a custom modular grid, canons delivers precise, scale-equivariant layouts through the familiar `geometry` interface.

🔗 [Overleaf](https://www.overleaf.com/read/mzqmhhznwkwg#88e0a5)

---

## Package Family

This repository contains three compatible packages:

| Package | Purpose | Standalone? |
|---------|---------|-------------|
| **canons** | Page layout via classical canons | ✅ Yes (core package) |
| **canons-margins** | Margin notes and numbered sidenotes | ✅ Yes |
| **canons-fullwidth** | Content spanning text + margin area | ⚠️ Recommended with canons |

---

## Key Features

### 📐 canons.sty (Core Package)

- **Five classical canons**: Van de Graaf, Villard de Honnecourt, Tufte, Canon des Ateliers, Grid
- **Four margin modes**: symmetric (outer margins), antisymmetric (inner margins), right-sided, left-sided
- **Gutter support**: Two calculation modes for binding allowance
- **Grid canon**: Modular N×N system with parametric control
- **Deterministic**: Same inputs produce same output
- **Class-agnostic**: Works with article, book, report
- **Exports dimensions** for downstream packages

### 🪶 canons-margins.sty

- **Unified control**: Manage margin notes and sidenotes together or independently
- **Four numbering schemes**: global, per-section, per-chapter, per-page
- **Smart justification**: Adapts to margin placement automatically
- **Integrates with sidenotes package** when present
- **Configurable**: Sizes, colors, alignment all controllable

### 🧩 canons-fullwidth.sty

- **Fullwidth environments**: Content spanning text block + margin
- **Tufte-inspired**: Wide figures without scaling
- **Mode-aware**: Adapts to all four margin modes automatically
- **Two variants**: Single-page (`fullwidth`) and multi-page (`fullwidth*`)
- **Caption flexibility**: Standard positioning or Tufte-style margin captions

---

## Installation

```bash
# Clone the repository
git clone https://github.com/deltaquebec/canons.git

# Copy .sty files to your local texmf tree
cp canons/src/*.sty ~/texmf/tex/latex/canons/

# Update TeX filename database
texhash ~/texmf
```

Or place the `.sty` files in your project directory.

---

## Quick Start

### Basic Usage

```latex
% Classic book with Van de Graaf proportions
\documentclass{book}
\usepackage[canon=vdg, margins=symmetric, gutterval=8mm]{canons}
\usepackage{canons-margins}
\usepackage{canons-fullwidth}

\begin{document}

Main text with proper proportions.\sidenote{Numbered annotation}

\begin{figure}[h]
  \begin{fullwidth}
    \includegraphics[width=\linewidth]{wide-plot.pdf}
  \end{fullwidth}
  \caption{Figure spanning text and margin}
\end{figure}

\end{document}
```

### Minimal Examples

```latex
% Notes-heavy article
\usepackage[canon=tufte, margins=right]{canons}
\usepackage[numbering=perpage, color=darkgray]{canons-margins}

% Economical textbook
\usepackage[canon=vdh, vdhN=12, paper=a4paper]{canons}

% Luxury display
\usepackage[canon=ateliers, ateliersstyle=luxury]{canons}

% Custom modular grid
\usepackage[canon=grid, gridN=12, gridinner=1, gridouter=3]{canons}
```

---

## Available Canons

| Canon | Description | Key Feature |
|-------|-------------|-------------|
| **Van de Graaf** (`vdg`) | Medieval manuscript proportions | 1/9 margins, 2/3 text area |
| **Villard de Honnecourt** (`vdh`) | Parametric family (N=3,6,9,12,15) | Width-based geometric divisions |
| **Tufte** (`tufte`) | Edward Tufte's book design | Wide outer margin for notes |
| **Canon des Ateliers** (`ateliers`) | French printing tradition | Three styles: ordinary/neater/luxury |
| **Grid** (`grid`) | Modern modular system | Full N×N parametric control |

---

## Core Options Reference

### Canon Selection

| Option | Description |
|--------|-------------|
| `canon=vdg` | Van de Graaf canon (1/9 margins) — *default* |
| `canon=vdh` | Villard de Honnecourt canon (N-fold divisions) |
| `canon=tufte` | Edward Tufte's book layout system |
| `canon=ateliers` | Canon des Ateliers (ordinary/neater/luxury) |
| `canon=grid` | Grid-based canon (N×N divisions) |
| `canon=false` | Disable canon logic; use `geometry` only |

### Margin Modes

| Option | Description |
|--------|-------------|
| `margins=symmetric` | Two-sided layout with alternating inner/outer margins *(book/report default)* |
| `margins=antisymmetric` | Two-sided layout with marginalia inside the gutter |
| `margins=right` | One-sided layout with right-side marginalia *(article default)* |
| `margins=left` | One-sided layout with left-side marginalia |

### Canon-Specific Parameters

| Option | Description |
|--------|-------------|
| `vdhN=<int>` | Division factor for Honnecourt canon (3, 6, 9, 12, 15) |
| `ateliersstyle=<style>` | Style variant: ordinary, neater, or luxury |
| `gridN=<int>` | Number of grid divisions (≥3) |
| `gridinner=<cells>` | Grid cells for inner margin |
| `gridouter=<cells>` | Grid cells for outer margin |
| `gridtop=<cells>` | Grid cells for top margin |
| `gridbottom=<cells>` | Grid cells for bottom margin |

### Layout & Debugging

- `gutterval=<length>` — set binding gutter width
- `guttermode=geometry|satzspiegel` — choose gutter adjustment mode
- `showframe` — visualize layout frame
- `landscape` — landscape orientation
- `paper=<size>` — pass paper size to `geometry`

---

## Provided Commands

| Command | Description |
|---------|-------------|
| `\pagecanoninfo` | Displays current canon and layout parameters |
| `\pagecanonmargins` | Returns current margin mode |
| `\pagecanonsetup{...}` | Reapply or modify layout mid-document |
| `\marginandtext` | Textblock + margin + separator width |
| `\marginandsep` | Margin + separator width |
| `\fullwidthoverhang` | Distance extending into margin area |

---

## Documentation

Comprehensive documentation is included for each package:

- **[canons.pdf](docs/documentation-canons.pdf)**: complete reference for the core layout package;
- **[canons-margins.pdf](docs/documentation-canons-margins.pdf)**: margin notes and sidenotes guide;
- **[canons-fullwidth.pdf](docs/documentation-canons-fullwidth.pdf)**: fullwidth environments reference.

Each manual includes:
- conceptual framework and design philosophy;
- complete option reference;
- usage patterns and common tasks;
- integration examples;
- troubleshooting guide;
- quick reference appendix.

Behind the scenes initial sketchwork and proportion work:

- **[bts-ratio.pdf](bts/bts-ratio.pdf)**: some handwork on docuemnt ratios;
- **[bts-sketch.pdf](bts/bts-sketch.pdf)**: some sketches of document leylines drawn with ruler.

---

## Design Philosophy

### Why canons?

The *page canon* encodes an implicit geometry of information; by reintroducing the proportional ideals of Honnecourt, Van de Graaf, and Tufte into LaTeX, this project treats page composition as a mathematical artifact that balances the aesthetic harmony of Western Medieval and Renaissance design with the analytic control required for technical and academic documents.

If you want **deterministic, reproducible** layouts from classical canons with explicit control of marginalia and gutters, and you **do not** want a full document class, use canons. If you want a comprehensive book production framework, use `memoir` or KOMA-Script; if you want a curated editorial idiom, use `tufte-book`.

### Key Principles

1. **Canons as mathematical rules**: Scale-equivariant functions from page dimensions to margins
2. **Integration over reimplementation**: Coordinate existing packages rather than replace them
3. **Explicit over implicit**: Margin semantics declared, not inferred
4. **User freedom**: Provide mechanisms, not policies

### What Sets Canons Apart

- **Algebraic implementations** of historical geometric constructions
- **Grid canon** exposes the implicit modular structure of classical canons
- **Margin mode semantics**: `symmetric`/`antisymmetric`/`right`/`left` explicit and class-aware
- **Gutter philosophies**: Two distinct approaches (geometry; satzspiegel)
- **Exported dimensions**: Downstream packages get `\marginandtext`, `\fullwidthoverhang`, etc.

---

## Dependencies

### canons.sty
`geometry`, `calc`, `xparse`, `ifthen`, `etoolbox`, `pgfkeys`, `array`

### canons-margins.sty
- **Required**: `marginnote`, `marginfix`, `ifthen`, `etoolbox`, `xparse`, `kvoptions`, `xcolor`, `perpage`
- **Optional**: `sidenotes` (integrates if present)

### canons-fullwidth.sty  
`caption`, `adjustbox`, `ifoddpage`, `changepage`, `xpatch`, `pgfkeys`, `ifthen`, `xcolor`

All dependencies are available in standard TeX distributions (TeX Live, MiKTeX).

---

## Compatibility

**Supported document classes:**
- ✅ `article`, `book`, `report` (full support)
- ⚠️  `memoir`, KOMA-Script classes (warnings issued; avoid mixing layout systems)
- ❌ `tufte-book`, `tufte-handout` (use their native features instead)

**Integration:**
- Works with `sidenotes` package (canons-margins patches it)
- Compatible with standard `figure`, `table`, caption packages
- Coordinates with `geometry` package options

---

## Contributing

Contributions are welcome! Please:

1. check existing issues before opening new ones;
2. include minimal working examples for bug reports;
3. follow the existing code style;
4. update documentation for new features;
5. test with multiple document classes.

---

## Future work

- [ ] Additional historical canons
- [ ] Baseline grid integration
- [ ] Per-page canon switching
- [ ] Advanced float positioning for fullwidth content
- [ ] Gallery of example documents
- [ ] Visualization macros for canon grids

---

## Citation

If you use these packages in academic work, please cite:

```bibtex
@misc{canons2025,
  author = {Quigley, Daniel},
  title = {Canons: Classical Page Layout for LaTeX},
  year = {2025},
  url = {https://github.com/deltaquebec/canons},
  version = {1.2},
  note = {LPPL 1.3c}
}
```

---

## License

**LaTeX Project Public License 1.3c**

This work may be distributed and/or modified under the conditions of the LaTeX Project Public License, either version 1.3c of this license or (at your option) any later version.

---

## Author

**Daniel Quigley**  
📧 [dquigleydev@gmail.com](mailto:dquigleydev@gmail.com)  
🔗 [GitHub](https://github.com/deltaquebec)  
🔗 [Website](https://dquigley.dev)

---

## Acknowledgments

This project draws conceptual inspiration from:

- **Jan Tschichold**
- **Robert Bringhurst**
- **Edward Tufte**

Special thanks to:
- The `geometry`,`memoir`, `KOMA-script`, and `tufte-latex` package maintainers for providing solid foundations
- The LaTeX community for feedback and testing
- All contributors who have helped improve these packages

---

## See Also

- [tufte-latex](https://github.com/Tufte-LaTeX/tufte-latex) - Complete Tufte document classes
- [memoir](https://ctan.org/pkg/memoir) - Comprehensive book production class
- [KOMA-Script](https://ctan.org/pkg/koma-script) - European book design tradition
- [typearea](https://ctan.org/pkg/typearea) - KOMA's layout calculator

---

**Version**: 1.2.0 (core), 1.2.0 (margins), 1.2.0 (fullwidth)  
**Last updated**: October 2025  
**Status**: Active development
