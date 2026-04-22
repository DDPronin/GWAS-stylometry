# From Genes to Tokens: GWAS-inspired stylometry

[![Conference](https://img.shields.io/badge/DH2026-Daejeon-blue)](https://dh2026.adho.org/)

This repository contains research materials for the DH2026 contribution **“From Genes to Tokens: A GWAS-inspired Approach for Interpretable Stylometric Analysis”**. The project explores a stylometric workflow inspired by **genome-wide association studies (GWAS)** and applies it to **token-frequency variation** in literary corpora.

<p align="center">
  <img src="imgs/pipeline_dmIHla2n" alt="Stylometric GWAS pipeline" width="900">
</p>

## Overview

Traditional stylometric methods often reduce texts to aggregate distance scores or dense vector representations that are difficult to interpret at the level of individual lexical features. This project proposes a complementary approach: instead of asking only whether two texts or authors are distant, it asks **which tokens contribute significantly to that contrast**.

The key analogy to GWAS is methodological. In classical GWAS, each genetic variant is tested separately for association with a phenotype. Here, each **token type** is treated as an analogous feature, and its standardized frequency is tested for association with a target author or class. This produces an interpretable map of stylistic markers supported by:

- per-token logistic regression,
- multiple-testing correction,
- Manhattan plots,
- volcano plots,
- QQ plots,
- genomic-control-style inflation diagnostics.

The goal is not to import biological claims into stylometry, but to adapt the **feature-wise inferential logic** of GWAS for literary and linguistic analysis.

## Repository structure

| Path | Description |
|------|-------------|
| `lemmatization.ipynb` | Lemmatises plain-text novels under `data/<language subset>/` using spaCy and writes processed files to `data/lemmas/<same structure>/`. |
| `GWAS_text.ipynb` | Builds the term–chunk matrix, runs per-token logistic regressions, applies multiple-testing correction, and produces diagnostic visualisations. |
| `data/` | Corpus fragments and lemma-based inputs used by the notebooks. Some large or copyright-restricted materials may be omitted in the public version. |
| `imgs/` | Exported figures and workflow illustrations used in the documentation. |

## Workflow

The analysis proceeds in several stages:

1. **Text preprocessing**  
   Literary texts are lemmatised and segmented into chunks of fixed size.

2. **Feature extraction**  
   A term–chunk matrix is constructed from token frequencies.

3. **Per-token regression**  
   For each token, a separate logistic-regression model is fitted to test its association with a target author or class.

4. **Multiple-testing correction**  
   Raw *p*-values are corrected to control false positives.

5. **Interpretation and visualisation**  
   Significant features are visualised with Manhattan and volcano plots and interpreted as potential stylometric markers.

## Quick start

### 1. Create an environment

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

For Unix-like systems:

```bash
source .venv/bin/activate
pip install -r requirements.txt
```

### 2. Install spaCy models

```bash
python -m spacy download en_core_web_sm
python -m spacy download de_core_news_sm
python -m spacy download ru_core_news_sm
```

### 3. Run the notebooks

Place the lemma files into the expected `data/lemmas/...` directory structure and run:

- `lemmatization.ipynb` for preprocessing,
- `GWAS_text.ipynb` for the statistical analysis and plots.

## Statistical notes

- **Regression model**  
  Each token is tested independently in a univariate logistic-regression framework.

- **Multiple testing**  
  The default correction is **Bonferroni**, implemented through `statsmodels.stats.multitest.multipletests`. This can be changed to **Benjamini–Hochberg** (`method="fdr_bh"`) if false discovery rate control is preferred.

- **Interpretation**  
  Significant tokens indicate statistically supported differences in usage under the selected contrast. They should be interpreted as **markers of association**, not as causal or essential features of an author’s style.

## Citation

If you reuse this workflow, please cite the DH2026 contribution when applicable and link to [DH2026](https://dh2026.adho.org/).  
The link to the conference proceedings will be added once it becomes available.  
For the Alliance of Digital Humanities Organizations conference series, see the ADHO website linked from the conference page.

## Licence

Add the appropriate licence here if you distribute the code or any corpus-derived materials publicly.
