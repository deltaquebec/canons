# page-canons: classical page layout for LaTeX

**Deterministic, historically-grounded page layouts with in-house marginalia**

The **page-canons** package implements classical and classical-inspired page construction canons as explicit mathematical rules, providing reproducible layouts based on historical book design. A single package now supplies page geometry, margin notes, sidenotes, and fullwidth environments with one external dependency: `geometry`.

[Overleaf](https://www.overleaf.com/read/ftstdrznqvqb#222e96)

## What changed in 3.x

Versions 1.x shipped three packages (`canons`, `canons-margins`, `canons-fullwidth`) coordinating roughly a dozen external dependencies (`marginnote`, `marginfix`, `sidenotes`, `perpage`, `caption`, `adjustbox`, `ifoddpage`, `changepage`, `xpatch`, `kvoptions`, `pgfkeys`, `xcolor`, ...). Version 3.x has foled everything into one `.sty` with in-house implementations of odd/even-page detection, keyval parsing, margin notes, sidenotes, per-page counters, and the fullwidth environment. If `sidenotes` is loaded, canons defers to it for styling hooks; otherwise, canons supplies its own.

New in 3.9.4: support for bleed and trim.

Do not ask what happened to version 2.x....

## Requirements

- **geometry** (the only declared external package dependency);
- two compilation passes for accurate sidenote/margin-note vertical positioning (position labels are written to `.aux`).

## Features

- **Five canons**: Van de Graaf; Villard de Honnecourt (parametric $N\in\{3,6,9,12,15\}$); Tufte; Canon des Ateliers (three styles); Grid ($N\times N$ modular);
- **Four margin modes**: `symmetric`; `antisymmetric`; `right`; `left`;
- **Gutter support** with two calculation modes: `geometry` (textwidth-invariant) and `satzspiegel` (recomputed on leaf width);
- **In-house marginalia** with collision avoidance, font isolation (`\normalfont` at the head of every note), explicit voffset, and four numbering modes (`global`, `persection`, `perchapter`, `perpage`);
- **Unified and split configuration** of size, justification, and line spread across margin notes and sidenotes;
- **Fullwidth environment** that extends into the outer margin and shifts sides correctly in two-sided modes;
- **PDF/UA-2 tagging hooks** (marginalia tagged as `Aside`) when `\DocumentMetadata` is used;
- **Exported lengths** for margin-aware figures and rules: `\marginandtext`; `\marginandsep`; `\textandsep`; `\fullwidthoverhang`; `\overflowingheadlen`;
- **Runtime reconfiguration** via `\pagecanonsetup{...}`;
- **Class-aware defaults**: `article` defaults to `margins=right`; `book`/`report` to `margins=symmetric`.

## Installation

```bash
git clone https://github.com/deltaquebec/canons.git
cp canons/src/page-canons.sty ~/texmf/tex/latex/canons/
texhash ~/texmf
```

Or place `page-canons.sty` in your project directory.

## Quick start

```latex
\DocumentMetadata{lang=en-US, pdfversion=2.0}
\documentclass{book}
\usepackage[canon=vdg, margins=symmetric, gutterval=8mm]{page-canons}

\begin{document}

Main text with canonical proportions.\sidenote{Numbered annotation in the outer margin.}

\begin{figure}[h]
  \begin{fullwidth}
    \includegraphics[width=\linewidth]{wide-plot.pdf}
  \end{fullwidth}
  \caption{Figure spanning text and margin.}
\end{figure}

\end{document}
```

Compile with `lualatex` twice.

### Minimal examples

```latex
% notes-heavy article
\usepackage[canon=tufte, margins=right, numbering=perpage, size=small]{page-canons}

% economical textbook
\usepackage[canon=vdh, vdhN=12, paper=a4paper]{page-canons}

% luxury display
\usepackage[canon=ateliers, ateliersstyle=luxury]{page-canons}

% custom modular grid
\usepackage[canon=grid, gridN=12, gridinner=1, gridouter=3]{page-canons}

% geometry only; marginalia suppressed
\usepackage[canon=false, nomarginalia]{page-canons}
```

## Available canons

| Canon | Key | Description |
|-------|-----|-------------|
| Van de Graaf | `vdg` | medieval manuscript proportions; 1/9 margins, 2/3 text area |
| Villard de Honnecourt | `vdh` | parametric family ($N \in \{3,6,9,12,15\}$) |
| Tufte | `tufte` | wide outer margin for extensive marginalia |
| Canon des Ateliers | `ateliers` | french tradition; ordinary / neater / luxury |
| Grid | `grid` | modern $N \times N$ modular system |
| (disabled) | `false` | `geometry` only; canon math bypassed |

## Option reference

### Canon selection

| Option | Values | Default |
|--------|--------|---------|
| `canon` | `vdg`, `vdh`, `tufte`, `ateliers`, `grid`, `false` | `vdg` |
| `vdhN` | 3, 6, 9, 12, 15 | 6 |
| `ateliersstyle` | `ordinary`, `neater`, `luxury` | `ordinary` |
| `gridN` | integer $\geq 3$ | 6 |
| `gridinner`, `gridouter`, `gridtop`, `gridbottom` | integers | 1, 2, 1, 2 |

### Layout

| Option | Values | Default |
|--------|--------|---------|
| `margins` | `symmetric`, `antisymmetric`, `right`, `left` | class-dependent |
| `gutterval` | dimension | `0mm` |
| `guttermode` | `geometry`, `satzspiegel` | `geometry` |
| `showframe`, `landscape`, `debug`, `nomarginalia` | bare booleans | off |
| `paper` | forwarded to `geometry` | — |

### Marginalia (unified)

| Option | Values | Default |
|--------|--------|---------|
| `size` | font-size name | `footnotesize` |
| `justification` | `default`, `raggedright`, `raggedleft`, `centered`, `justified` | `default` |
| `notespread` | factor | `1.05` |
| `numbering` | `global`, `persection`, `perchapter`, `perpage` | `global` |

### Marginalia (split; override unified)

| Option | Values | Default |
|--------|--------|---------|
| `marginsize` | `true` / `false` | `true` |
| `marginnotesize`, `sidenotesize` | font-size name | follows `size` |
| `marginjustify` | `true` / `false` | `true` |
| `marginnotejustify`, `sidenotejustify` | justification value | follows `justification` |

## Commands

| Command | Action |
|---------|--------|
| `\marginnote{text}` / `\marginnote{text}[voffset]` | margin note, collision-aware |
| `\sidenote{text}` / `\sidenote[n]{text}[voffset]` | numbered sidenote |
| `\sidenotemark` / `\sidenotemark[n]` | inline mark only |
| `\sidenotetext{text}[voffset]` | note body only |
| `\canonssidenotemarkformat`, `\canonssidenotelabelformat` | format hooks |
| `\pagecanonsetup{…}` | reconfigure at any point |
| `\pagecanonmargins` | expands to current margin mode |
| `\canonsswitchmargin`, `\canonsresetmargin` | toggle / reset marginpar side |

## Exported lengths

| Length | Value |
|--------|-------|
| `\marginandtext` | `\textwidth + \marginparwidth + \marginparsep` |
| `\marginandsep` | `\marginparwidth + \marginparsep` |
| `\textandsep` | `\textwidth + \marginparsep` |
| `\fullwidthoverhang` | `\marginparwidth + \marginparsep` |
| `\overflowingheadlen` | same as `\marginandtext` |

## Documentation

The repository includes a combined primer and test suite (`canons.pdf`) organized in three parts: conceptual framework; user manual; test suite with edge cases. All example pages render with `showframe` enabled so geometry effects are directly visible.

## Scope and limitations

- layout resolves once at `\AtBeginDocument`; `\pagecanonsetup` can adjust mid-document, but recomputation is global, not per-page or per-chapter;
- no baseline-grid enforcement or line-spacing management;
- incompatible with classes that manage layout internally (`memoir`, KOMA-Script, `tufte-book`); warnings are issued when such classes are detected;
- `twocolumn` emits a warning; marginalia placement is not guaranteed;
- for Honnecourt and Ateliers, vertical margins are expressed as fractions of $W$, coupling textblock aspect to paper aspect $H/W$;
- in `guttermode=geometry`, large binding allowances can collapse the outer margin (warning issued); use `guttermode=satzspiegel` to preserve proportions.

## Compatibility

**Supported classes**: `article`; `book`; `report`;
**Incompatible**: `memoir`; `scrbook`/`scrreprt`/`scrartcl`; `tufte-book`; `tufte-handout`;
**Integration**: detects `sidenotes` at load and defers styling hooks to it when present; detects `ifoddpage` and uses it if already loaded.

## Contributing

The usual good practice:

1. check existing issues before opening new ones;
2. include minimal working examples for bug reports;
3. follow existing code style;
4. update the primer for new features.

## Citation

```bibtex
@misc{canons2026,
  author = {Quigley, Daniel},
  title  = {page-canons: classical page layout for LaTeX},
  year   = {2026},
  url    = {https://github.com/deltaquebec/canons},
  version = {3.9.3},
  note   = {LPPL 1.3c}
}
```

## License

**LaTeX Project Public License 1.3c.**

## Author

**Daniel Quigley**
- [dquigleydev@gmail.com](mailto:dquigleydev@gmail.com)
- [GitHub](https://github.com/deltaquebec) 
- [Website](https://dquigley.dev)

## Acknowledgments

Conceptual inspiration from Jan Tschichold, Robert Bringhurst, and Edward Tufte. Thanks to the `geometry`, `memoir`, KOMA-Script, and `tufte-latex` maintainers for providing the foundations this package builds on, and to everyone who has reported bugs or suggested features.

## See also

- [tufte-latex](https://github.com/Tufte-LaTeX/tufte-latex) — complete Tufte document classes
- [memoir](https://ctan.org/pkg/memoir) — comprehensive book production class
- [KOMA-Script](https://ctan.org/pkg/koma-script) — european book design tradition
- [typearea](https://ctan.org/pkg/typearea) — KOMA's layout calculator

---

**Version**: 3.9.4
**Last updated**: July 2026
**Status**: Active development

---
