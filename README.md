# Canons: Classical Page Layout for LaTeX

**Deterministic, historically-grounded page layouts with margin control**

The **canons** package family implements classical and classical-inspired page construction canons as explicit mathematical rules, providing reproducible layouts based on historical book design. Whether you need Van de Graaf's medieval proportions, Tufte's asymmetric margins, or a custom modular grid, canons delivers precise, scale-equivariant layouts through the familiar `geometry` interface.

🔗 [Overleaf](https://www.overleaf.com/read/mzqmhhznwkwg#88e0a5)

---

## Package Family

This repository contains three compatible packages:

| Package | Purpose | Standalone? |
|---------|---------|-------------|
| **canons** | page layout via classical canons | yes (core package) |
| **canons-margins** | margin notes and numbered sidenotes | yes |
| **canons-fullwidth** | content spanning text and margin area | recommended with canons |

---

## Features

### canons.sty (core package)

- **Five classical canons**: Van de Graaf, Villard de Honnecourt, Tufte, Canon des Ateliers, Grid;
- **Four margin modes**: symmetric (outer margins), antisymmetric (inner margins), right-sided, left-sided;
- **Gutter support**: two calculation modes for binding allowance;
- **Grid canon**: modular N×N system with parametric control;
- **Deterministic**: same inputs produce same output;
- **Class-agnostic**: works with article, book, report;
- **Exports dimensions** for downstream packages.

### canons-margins.sty

- **Unified control**: manage margin notes and sidenotes together or independently;
- **Four numbering schemes**: global, per-section, per-chapter, per-page;
- **Smart justification**: adapts to margin placement automatically;
- **Integrates with sidenotes package** when present;
- **Configurable**: sizes, colors, alignment all controllable.

### canons-fullwidth.sty

- **Fullwidth environments**: content spanning text block and margin;
- **Tufte-inspired**: wide figures without scaling;
- **Mode-aware**: adapts to all four margin modes automatically;
- **Two variants**: single-page (`fullwidth`) and multi-page (`fullwidth*`);
- **Caption flexibility**: standard positioning or Tufte-style margin captions.

---

## Installation

```bash
# clone repository
git clone https://github.com/deltaquebec/canons.git

# copy .sty files to local texmf tree
cp canons/src/*.sty ~/texmf/tex/latex/canons/

# update TeX filename database
texhash ~/texmf
```

Or place the `.sty` files in your project directory.

---

## Quick start

### Basic usage

```latex
% classic book with Van de Graaf proportions
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

### Minimal examples

```latex
% notes-heavy article
\usepackage[canon=tufte, margins=right]{canons}
\usepackage[numbering=perpage, color=darkgray]{canons-margins}

% economical textbook
\usepackage[canon=vdh, vdhN=12, paper=a4paper]{canons}

% luxury display
\usepackage[canon=ateliers, ateliersstyle=luxury]{canons}

% custom modular grid
\usepackage[canon=grid, gridN=12, gridinner=1, gridouter=3]{canons}
```

---

## Available canons

| Canon | Description | Key Feature |
|-------|-------------|-------------|
| **Van de Graaf** (`vdg`) | medieval manuscript proportions | 1/9 margins, 2/3 text area |
| **Villard de Honnecourt** (`vdh`) | parametric family (N=3,6,9,12,15) | width-based geometric divisions |
| **Tufte** (`tufte`) | Edward Tufte's book design | wide outer margin for notes |
| **Canon des Ateliers** (`ateliers`) | french printing tradition | three styles: ordinary/neater/luxury |
| **Grid** (`grid`) | modern modular system | full N×N parametric control |

---

## Reference

### Canon selection

| Option | Description |
|--------|-------------|
| `canon=vdg` | Van de Graaf canon (1/9 margins) — *default* |
| `canon=vdh` | Villard de Honnecourt canon (N-fold divisions) |
| `canon=tufte` | Edward Tufte's book layout system |
| `canon=ateliers` | Canon des Ateliers (ordinary/neater/luxury) |
| `canon=grid` | Grid-based canon (N×N divisions) |
| `canon=false` | disable canon logic; use `geometry` only |

### Margin modes

| Option | Description |
|--------|-------------|
| `margins=symmetric` | two-sided layout with alternating inner/outer margins *(book/report default)* |
| `margins=antisymmetric` | two-sided layout with marginalia inside gutter |
| `margins=right` | one-sided layout with right-side marginalia *(article default)* |
| `margins=left` | one-sided layout with left-side marginalia |

### Canon-specific parameters

| Option | Description |
|--------|-------------|
| `vdhN=<int>` | division factor for Honnecourt canon (3, 6, 9, 12, 15) |
| `ateliersstyle=<style>` | style variant: ordinary, neater, luxury |
| `gridN=<int>` | number of grid divisions (≥3) |
| `gridinner=<cells>` | grid cells for inner margin |
| `gridouter=<cells>` | grid cells for outer margin |
| `gridtop=<cells>` | grid cells for top margin |
| `gridbottom=<cells>` | grid cells for bottom margin |

### Layout, debugging

- `gutterval=<length>` — set binding gutter width;
- `guttermode=geometry|satzspiegel` — choose gutter adjustment mode;
- `showframe` — visualize layout frame;
- `landscape` — landscape orientation;
- `paper=<size>` — pass paper size to `geometry`.

---

## Provided commands

| Command | Description |
|---------|-------------|
| `\pagecanoninfo` | displays current canon and layout parameters |
| `\pagecanonmargins` | returns current margin mode |
| `\pagecanonsetup{...}` | reapply or modify layout mid-document |
| `\marginandtext` | textblock + margin + separator width |
| `\marginandsep` | margin + separator width |
| `\fullwidthoverhang` | distance extending into margin area |

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

### Key principles

1. scale-equivariant functions from page dimensions to margins;
2. coordinate existing packages rather than replace them;
3. margin semantics declared, not inferred;
4. provide mechanisms, not policies.

### About

- **Algebraic implementations** of historical geometric constructions;
- **Grid canon** exposes the implicit modular structure of classical canons;
- **Margin mode semantics** `symmetric`/`antisymmetric`/`right`/`left` explicit and class-aware;
- **Gutter philosophies** two distinct approaches (geometry; satzspiegel);
- **Exported dimensions** downstream packages get `\marginandtext`, `\fullwidthoverhang`, etc..

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
- `article`, `book`, `report` (full support);
- `memoir`, KOMA-Script classes (warnings issued; avoid mixing layout systems);
- Not `tufte-book`, `tufte-handout` (use their native features instead).

**Integration:**
- Works with `sidenotes` package (canons-margins patches it);
- Compatible with standard `figure`, `table`, caption packages;
- Coordinates with `geometry` package options.

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
[dquigleydev@gmail.com](mailto:dquigleydev@gmail.com)  
[GitHub](https://github.com/deltaquebec)  
[Website](https://dquigley.dev)

---

## Acknowledgments

This project draws conceptual inspiration from:

- **Jan Tschichold**
- **Robert Bringhurst**
- **Edward Tufte**

Special thanks to:
- the `geometry`,`memoir`, `KOMA-script`, and `tufte-latex` package maintainers for providing solid foundations;
- the LaTeX community for feedback and testing;
- all contributors who have helped improve these packages.

---

## See also

- [tufte-latex](https://github.com/Tufte-LaTeX/tufte-latex) complete Tufte document classes
- [memoir](https://ctan.org/pkg/memoir) comprehensive book production class
- [KOMA-Script](https://ctan.org/pkg/koma-script) European book design tradition
- [typearea](https://ctan.org/pkg/typearea) KOMA's layout calculator

---

**Version**: 1.2.0 (core), 1.2.0 (margins), 1.2.0 (fullwidth)  
**Last updated**: December 2025  
**Status**: Active development
