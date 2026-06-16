# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## Project Overview

ACL-format academic paper for the "Anything2PBL" project, built on the official ACL style files. The paper is compiled with pdfLaTeX.

## Build Commands

```bash
# Full build (pdfLaTeX + BibTeX)
pdflatex acl_latex.tex && bibtex acl_latex && pdflatex acl_latex.tex && pdflatex acl_latex.tex

# Quick recompile (no bibliography changes)
pdflatex acl_latex.tex

# Using latexmk (if available)
latexmk -pdf acl_latex.tex
```

For non-Latin scripts, use `acl_lualatex.tex` with `lualatex` instead.

## Editable vs Read-Only Files

**Edit these:**
- `acl_latex.tex` — main paper source
- `custom.bib` — bibliography entries

**Do not modify:**
- `acl.sty` — ACL style package
- `acl_natbib.bst` — bibliography style

## Key Conventions

- Document class: `\documentclass[11pt]{article}` with `\usepackage[review]{acl}` (switch to `\usepackage{acl}` for camera-ready)
- Review mode enforces anonymity: no author names, no acknowledgments, no self-identifying references
- Page limits: 8 pages content (review) / 9 pages (final) for long papers, plus unlimited references
- Citations use `natbib`: `\citet{key}` for textual, `\citep{key}` for parenthetical, `\citeposs{key}` for possessive
- Paper size is A4 (21cm × 29.7cm), two-column, Times Roman font
