# Research materials: GWAS-inspired stylometry (DH2026)

[![Conference](https://img.shields.io/badge/DH2026-Daejeon-blue)](https://dh2026.adho.org/)

This repository supports research that will be presented at [DH2026](https://dh2026.adho.org/) (Daejeon, July 27–31, 2026). It holds reproducible notebooks and auxiliary assets for a **genome-wide association study (GWAS)–inspired** procedure applied to **token frequencies** in literary corpora (working title **“From Genes to Tokens”**).

## What this project does

Classical stylometry often compresses texts into opaque vector spaces. Here, each **token type** (words and punctuation treated as separate types) plays the role of a genetic marker (“SNP”): its **relative frequency** across documents is treated as a quantitative trait. A **binary outcome**—for example, chunks attributed to one author versus all others—is regressed on that frequency using **logistic regression**. The resulting coefficients and *p*-values support **Manhattan-style** and **volcano** plots, multiple-testing correction, **QQ plots**, and genomic-control-style **inflation (λ)** diagnostics, yielding an interpretable list of marker-like lexical and punctuational contrasts.

The conceptual bridge to GWAS is methodological: **many univariate tests with explicit multiple-testing control and visual diagnostics**, not a claim of biological genetics.

## Repository layout

| Path | Role |
|------|------|
| `lemmatization.ipynb` | Lemmatises plain-text novels under `data/<language subset>/` with spaCy; writes parallel files under `data/lemmas/<same structure>/`. |
| `GWAS_text.ipynb` | Builds a term–chunk matrix with `sklearn` (`CountVectorizer` counts + `TfidfVectorizer(use_idf=False)` for TF), runs per-token logistic regressions, applies Bonferroni correction (configurable to Benjamini–Hochberg), and produces diagnostic plots. |
| `data/` | Corpus fragments (lemma layers used by the analysis notebook). Large or rights-restricted files may be omitted from a public mirror; structure is preserved. |
| `imgs/` | Exported figures (e.g. Manhattan plots) for documentation or reuse. |

## Quick start

1. **Python environment** (3.10+ recommended):

   ```bash
   python -m venv .venv
   .venv\Scripts\activate   # Windows
   pip install -r requirements.txt
   ```

2. **spaCy models** (for `lemmatization.ipynb`):

   ```bash
   python -m spacy download en_core_web_sm
   python -m spacy download de_core_news_sm
   python -m spacy download ru_core_news_sm
   ```

3. Run notebooks top-to-bottom after placing lemma files under `data/lemmas/...` as expected by `GWAS_text.ipynb` (default pattern: `data/lemmas/English_25_3`).

## Notes on statistics

- **Multiple testing:** The notebook defaults to **Bonferroni** (`statsmodels.stats.multitest.multipletests`). The introduction cell explains how to switch to **`method="fdr_bh"`** if your analysis plan uses false discovery rate control instead.
- **Interpretation:** Significant associations point to **usage differences** conditioned on the chosen contrast (author, genre slice, etc.); they do not by themselves imply causality or immutable stylistic “genes.”

## Citation

If you reuse this workflow, cite the DH2026 contribution when applicable and link to [DH2026](https://dh2026.adho.org/). For the Alliance of Digital Humanities Organizations conference series, see the ADHO website linked from the conference page.

## Licence

Specify licence here if you distribute corpus-derived files or code publicly.
