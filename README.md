# Assessing Fairness in Clustering: A Dual-Strategy Evaluation Framework

This study proposes an evaluation framework for fairness-aware clustering and benchmarks 7 fairness-aware clustering algorithms across 5 real-world datasets under two k-selection strategies. Strategy 1 applies a consensus k, selected from Standard K-Means via a majority vote across six methods, uniformly to all algorithms for controlled comparison. Strategy 2 allows each algorithm to select its own optimal k via combined score, revealing the best attainable performance. Results are evaluated across clustering utility, external validity, and group fairness metrics.

- **Strategy 1** applies a single consensus *k*, selected from Standard K-Means via majority vote across six k-selection heuristics, uniformly to all algorithms for controlled comparison.
- **Strategy 2** lets each algorithm's *k* be chosen by the same majority-vote consensus, revealing the best attainable performance of each method.

Results are evaluated across clustering utility, external validity, and group fairness metrics, and repeated over **30 seeds (0–29)** for statistical robustness. A supplementary **k-sensitivity study** (k = 2–10) checks how stable each metric is to the choice of k.


## Setup

```bash
pip install -r requirements.txt
```

Download the five datasets and place them under `data/`:

| Dataset | Source |
|---------|--------|
| Adult Income | https://archive.ics.uci.edu/dataset/2/adult |
| COMPAS | https://github.com/propublica/compas-analysis |
| German Credit | https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data |
| Default Credit Card | https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients |
| Law School (LSAC) | https://github.com/damtharvey/law-school-dataset |
| Diabetes 130-US | https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008 |
| Dutch Census | https://microdata.worldbank.org/index.php/catalog/2102 |
| MEPS (Panel 20, 2016) | https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_results.jsp?cboDataYear=All&cboDataTypeY=1%2CHousehold+Full+Year+File&buttonYearandDataType=Search&cboPufNumber=All&SearchTitle=Longitudinal |

The first 5 datasets form **Part A** (original datasets); Diabetes / Dutch / MEPS form **Part B** (new datasets), added to test generalization beyond the original benchmark.

Each base dataset is expanded into multiple sensitive-attribute configurations (gender / race / combined, where the attribute is available):
- Part A: **11 configurations** (adult, compas, german, credit, law, adult_race, adult_combined, compas_race, compas_combined, law_race, law_combined — german and credit have no race attribute)
- Part B: **7 configurations** (diabetes_gender, diabetes_race, diabetes_combined, dutch_gender, meps_gender, meps_race, meps_combined)
- **Total: 18 configurations** across 8 base datasets


## Algorithms

K-Means  
Fairlet Decomposition  
Balanced Fair K-means (BFKM)  
Cluster-level Centroid Fairness (CCF)  
Post-Processing Based Nearest Foreign Point (PP-NFP)  
Post-Processing Based Gini (PP-Gini)  
Rawlsian K-Means

## Execute

**Step 1 — Run experiments**

```
Strategy1_all_algorithms.ipynb
Strategy2_kmeans_fairlet_bfkm.ipynb
Strategy2_ccf_ppnfp_ppgini_rawlsian.ipynb
```

Each notebook saves results as `.pkl` and `.csv` files under `results/strategy1/` and `results/strategy2/`.

**Step 2 — Compile result tables (manual)**

From the `.csv` output of Strategy 1 and Strategy 2, compile the following four Excel files and place them in `results/normalized/`:

```
results/normalized/S1 Quality.xlsx
results/normalized/S1 Fairness.xlsx
results/normalized/S2 Quality.xlsx
results/normalized/S2 Fairness.xlsx
```

**Step 3 — Run normalization**

```
Result_normalization.ipynb
```

Reads the four Excel files above and outputs scaled (0-1) to the same `results/normalized/` folder.
