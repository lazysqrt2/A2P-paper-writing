# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Academic paper repository for **Anything2PBL (A2P)** — a research paper targeting ACL-style NLP/AI conferences. The paper proposes a hierarchical constrained generation framework that transforms arbitrary inputs into pedagogically-calibrated PBL project repositories via a five-stage human-in-the-loop pipeline.

## Build Commands

```bash
# Compile the paper (pdflatex + bibtex full cycle)
pdflatex acl_latex.tex && bibtex acl_latex && pdflatex acl_latex.tex && pdflatex acl_latex.tex

# Quick recompile (no bib changes)
pdflatex acl_latex.tex
```

## Key Files

- `acl_latex.tex` — main paper source (currently in `\usepackage[review]{acl}` mode)
- `custom.bib` — all bibliography entries (both template examples and A2P-specific citations)
- `A2P_reference.md` — literature tracking document with per-paper usage notes and Related Work skeleton (Chinese + English)
- `formatting.md` — ACL formatting rules (page limits, fonts, citation style, anonymity)
- `acl.sty` / `acl_natbib.bst` — ACL style files (do not modify)
- `outline/` — paper outline images (1.png, 2.png, 3.png)
- `reference_paper/` — collected PDFs organized by topic (A1_engineering, A2_educational)

## Paper Structure and Conventions

The paper uses the dual-objective framing `E(O) x P(O)` (engineering correctness x pedagogical effectiveness) throughout. Key terminology:
- **Challenge-Noise Separation** — the learner-dependent boundary between productive struggle and busywork
- **Learner-aware scaffolding** — per-sub-task decisions (guided walkthrough / hint / productive struggle) conditioned on instructor-supplied learner profile
- **Five-stage HITL pipeline** — topic analysis, project design, scaffolding, code generation, validation

The paper is in double-blind review mode. Do not add author-identifying information.

## Citation and Reference Workflow

- `A2P_reference.md` is the master reference tracker. Each entry has a paper ID, one-line summary, and explicit usage note for where/how to cite it in the paper.
- References in `custom.bib` use descriptive cite keys like `qian2023chatdev`, `wood1976scaffolding`.
- Non-arxiv classical works (Vygotsky, Sweller, Wood et al.) are manually entered in `custom.bib` — they won't appear in arxiv searches.
- ACL style requires: natbib citations, DOIs when available, full author names (not initials).

## ACL Formatting Constraints

- Long paper: 8 pages content (review) / 9 pages (camera-ready), unlimited references
- A4 paper, two-column, Times Roman 11pt body text
- Abstract max 200 words
- Citations: `\cite{key}` for parenthetical, `\citet{key}` for textual (natbib)
