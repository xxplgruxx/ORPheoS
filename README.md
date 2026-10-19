# ORPheoS – psychometric analysis code

Analysis code for:

> Rotermund, P. L., Hildebrandt, H., Witt, K., Kastrup, A., Thiel, C. M., Roheger, M., & Hildebrandt, A. *Towards remote post-stroke cognitive monitoring: psychometric foundations of the ORPheoS smartphone item bank.* npj Digital Medicine (under review).

ORPheoS (Oldenburg Test Battery for Remote Digital Phenotyping of Post-Stroke Cognition) is a smartphone-based cognitive item bank for repeated assessment after stroke. This repository contains the R script that reproduces every analysis, table and figure reported in the manuscript and its Supplementary Information from the curated baseline data set (234 stroke patients, 280 controls).

Archived version: [![DOI](https://zenodo.org/badge/1425570016.svg)](https://doi.org/10.5281/zenodo.23474622)

## Contents

| File | Description |
|---|---|
| `EMA4Stroke_ORPheoS_Analysis.R` | Complete analysis pipeline (scoring, item-bank properties, DIF, reliability, validity, bifactor model, figures and tables) |
| `sessionInfo.txt` | R and package versions used for the reported results |
| `LICENSE` | MIT licence |

## Data availability

The participant data are not publicly available due to data protection regulations (EU General Data Protection Regulation) and the terms of participant consent, but are available from the corresponding authors upon reasonable request. For the same reason, the preprocessing script that creates the curated data set from the raw study data (participant exclusions, harmonisation of demographic and clinical variables, pseudonymisation) is not included.

The analysis script expects one file, `ORPheoS_Baseline_Curated.feather`, with one row per analysed participant. It contains pseudonymised study IDs, group and control recruitment phase, demographic and clinical variables, item responses of all five tasks, and the SART-ED trials in wide format. A data dictionary is provided together with the data on request.

## Requirements

- R ≥ 4.4 (versions used for the reported results: see `sessionInfo.txt`)
- CRAN packages: `readr`, `dplyr`, `tidyr`, `stringr`, `purrr`, `tibble`, `arrow`, `ggplot2`, `GGally`, `mirt`, `TAM`, `psych`, `GPArotation`, `Gifi`, `lavaan`, `lme4`, `effsize`, `rlang`, `rsvg`
- Optional: `DiagrammeR` and `DiagrammeRsvg` (participant flow diagram; without them the diagram is written as Graphviz DOT source)

```r
install.packages(c("readr", "dplyr", "tidyr", "stringr", "purrr", "tibble",
                   "arrow", "ggplot2", "GGally", "mirt", "TAM", "psych",
                   "GPArotation", "Gifi", "lavaan", "lme4", "effsize",
                   "rlang", "rsvg", "DiagrammeR", "DiagrammeRsvg"))
```

The script stops with a list of missing packages if any are not installed.

## Usage

1. Set `data_dir` in Section 0.1 of the script to the folder containing `ORPheoS_Baseline_Curated.feather`.
2. Run the script from top to bottom (e.g. `source("EMA4Stroke_ORPheoS_Analysis.R")`).

All output is written to the subfolder `output/` of `data_dir`. A full run takes considerably longer than the rest of the pipeline when the DIF analysis, the latent-mean robustness models and the item-half interchangeability analysis are enabled. Each can be switched off in Section 0.2 (`RUN_DIF_ANALYSIS`, `RUN_LATENT_MEAN_ROBUSTNESS`, `RUN_INTERCHANGEABILITY`); this skips only the corresponding supplementary table. The random seed is fixed (`set.seed(20260821)`) so that results are reproducible.

## Structure of the script

Sections follow the order of the manuscript:

| Section | Content | Manuscript element |
|---|---|---|
| 0 | Configuration, packages, helper functions | – |
| 1 | Data import (curated data set) | – |
| 2 | Task scoring: GRT, DRT, PAL, CI, SART-ED (Rasch-family IRT models, iterative item-fit trimming, split-half parcels) | Methods; Supplementary Table 4 |
| 3 | Analysed sample, participant flow, completers vs. non-completers | Supplementary Figure 1; Supplementary Tables 1–3 |
| 4 | Item-bank properties: model comparisons, targeting, test information, local dependence, interchangeability of item subsets | Supplementary Tables 5–6; Supplementary Figures 3–4 |
| 5 | Differential item functioning | Supplementary Tables 7–8 |
| 6 | Reliability and standard error of measurement | Supplementary Table 2 |
| 7 | Known-groups validity and robustness checks | Figure 3; Supplementary Tables 9–15 |
| 8 | Convergent and divergent validity | Figure 2; Supplementary Table 16 |
| 9 | Exploratory criterion validity (MoCA) | Supplementary Table 17 |
| 10 | Structural validity: S-1 bifactor model | Figure 4; Supplementary Table 18 |
| 11 | Export of all reported tables | – |

## Output

- `Figure*` and `SupplFigure*`: figures as vector PDF (submission format) and 600-dpi PNG, sized to journal specifications (183 mm width); path diagrams additionally as SVG.
- `SupplTable*.csv`: one or more CSV files per supplementary table, named after the table they belong to.
- `Manuscript_Reporting_Tables.html`: all reported tables in one document.
- `sessionInfo.txt`: R and package versions of the run.

## Citation

If you use this code, please cite the article (reference will be added upon publication) and the archived code:

> Rotermund, P. L., & Hildebrandt, A. (2026). *ORPheoS psychometric analysis code* (Version 1.0.0) [Computer software]. Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX

## Contact

Paul Leonard Rotermund (paul.rotermund@uni-oldenburg.de)
Andrea Hildebrandt (andrea.hildebrandt@uni-oldenburg.de)
Psychological Methods and Statistics, Department of Psychology, Carl von Ossietzky Universität Oldenburg, Germany

## Funding

This work was supported by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation), Project-ID 456732630 – RTG 2783 "Neuromodulation of Motor and Cognitive Function in Brain Health and Disease".

## Licence

The code is released under the MIT licence (see `LICENSE`).
